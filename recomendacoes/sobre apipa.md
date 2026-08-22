# Guia Técnico sobre APIPA (Automatic Private IP Addressing)

## 📌 Sobre este Documento

Este documento apresenta um panorama completo, aprofundado e didático sobre o **APIPA (Endereçamento IP Privado Automático)**. 

Ao ler este material, você aprenderá:
- O conceito fundamental do APIPA, sua finalidade, faixas de endereço, limitações e a diferença crucial em relação ao Link-Local do IPv6.
- O ciclo **DORA** do protocolo DHCP e como o **Microsoft Windows** gerencia o fallback para APIPA na ausência de resposta.
- Procedimentos práticos no Windows: verificação via linha de comando e desativação através do Registro.
- O impacto do APIPA em infraestruturas corporativas e a metodologia de diagnóstico baseada em casos do **Cisco TAC (Technical Assistance Center)**.
- Seis cenários reais de falhas de rede explicados passo a passo (Firewalls com Proxy ARP, escopos DHCP duplicados, Cisco SDA, adaptadores com envio de MACs aleatórios, MTU mismatch com EAP-TLS e IP Device Tracking).

---

## 1. O que é APIPA (Automatic Private IP Addressing)?

O **APIPA** (padronizado pela IETF na **RFC 3927** sob o nome de *Dynamic Configuration of IPv4 Link-Local Addresses*) é um recurso de contingência do protocolo IPv4. Ele permite que um dispositivo de rede atribua automaticamente a si mesmo um endereço IP válido para comunicação local quando não há um servidor DHCP disponível e nenhum IP manual foi configurado.

### Características Principais
* **Faixa Reservada pela IANA:** `169.254.0.0` até `169.254.255.255` (bloco de rede `169.254.0.0/16`).
* **Máscara de Sub-rede Padrão:** `255.255.0.0` (/16).
* **Endereçamento Não Roteável:** Pacotes contendo endereços `169.254.x.x` não são encaminhados por roteadores.
* **Escopo Estritamente Local (*Link-Local*):** A comunicação é limitada a dispositivos conectados ao mesmo segmento físico ou lógico de rede (mesmo domínio de broadcast / mesma VLAN).
* **Sem Acesso Direto à Internet:** Dispositivos com APIPA não possuem rota de saída nem resolução de DNS público, a menos que utilizem um servidor proxy de aplicação.

> 💡 **Nota Didática: Diferença entre IPv4 APIPA e IPv6 Link-Local (`fe80::/10`)**
> - **No IPv4 (APIPA):** É um mecanismo de **fallback/emergência**. Ele só é acionado quando o processo de obtenção de IP via DHCP falha.
> - **No IPv6 (Link-Local):** É um mecanismo **obrigatório e permanente**. Toda interface com IPv6 ativo gera automaticamente um endereço iniciado em `fe80::` (via SLAAC/EUI-64), coexistindo normalmente com o DHCPv6 e com endereços públicos globais para viabilizar funções essenciais como a descoberta de vizinhos (NDP) e mensagens de controle de roteadores.

---

## 2. Funcionamento do DHCP e Comportamento no Microsoft Windows

Para compreender o motivo de um computador assumir um endereço APIPA, é indispensável entender o ciclo de vida da atribuição dinâmica de endereços.

### 2.1. O Processo DHCP (Ciclo DORA)
Quando uma placa de rede configurada para IP automático se conecta ao meio físico, ela tenta negociar as configurações de rede com um servidor DHCP através de 4 etapas conhecidas pela sigla **DORA**:

```
[Cliente]                                     [Servidor DHCP]
   │                                                 │
   │ ─── 1. DISCOVER (Broadcast: "Preciso de IP") ──>│
   │ <── 2. OFFER (Unicast/Bcast: "Tenho o IP X") ───│
   │ ─── 3. REQUEST (Broadcast: "Quero usar o IP X")>│
   │ <── 4. ACKNOWLEDGE (Confirmação da concessão) ──│
```

1. **Discover (D):** O cliente envia um pacote em broadcast procurando servidores DHCP na rede local.
2. **Offer (O):** Um ou mais servidores respondem oferecendo um endereço IP, máscara, gateway e DNS.
3. **Request (R):** O cliente responde aceitando formalmente uma das ofertas recebidas.
4. **Acknowledge / ACK (A):** O servidor confirma a concessão (*lease*) e registra a alocação.

**Onde o APIPA entra?** Se o ciclo DORA for interrompido em qualquer uma dessas fases (por ausência de resposta ao *Discover*, perda da mensagem de *Offer* ou recusa de IP), o Windows assume o controle e ativa o APIPA.

---

### 2.2. Como o Windows Decide Ativar o APIPA

1. **Host Inicializado sem Concessão Anterior:**
   - O Windows envia repetidas mensagens de `DHCP Discover`.
   - Se nenhum servidor responder dentro do tempo limite, o sistema gera aleatoriamente um endereço `169.254.x.y` com máscara `255.255.0.0`.
   - Uma notificação de conectividade limitada é exibida ao usuário e o sistema continua emitindo mensagens `DHCP Discover` a cada **3 minutos** em segundo plano.

2. **Host Inicializado com Concessão Prévia:**
   - O computador tenta renovar o IP antigo com o servidor DHCP.
   - Se o servidor DHCP não responder, o Windows tenta se comunicar via ARP/Ping com o **Gateway Padrão** (*Default Gateway*) registrado anteriormente.
   - **Se o Gateway responder:** O Windows assume que ainda está na mesma rede corporativa e mantém temporariamente o IP anterior.
   - **Se o Gateway não responder:** O Windows assume que mudou de rede ou que a conectividade falhou, recorrendo imediatamente ao APIPA e tentando novo contato com DHCP a cada **3 minutos**.

3. **Expiração do Tempo de Concessão (*Lease Expired*):**
   - Caso o tempo de validade do IP termine sem que o host consiga renová-lo, o IP é revogado e o host assume APIPA.
   - O sistema envia 4 mensagens de descoberta e reitera as tentativas a cada **5 minutos**.

---

### 2.3. Verificação e Desativação no Windows

#### Como verificar o status via Prompt de Comando:
```cmd
ipconfig /all
```
Se a linha **"Configuração Automática Habilitada"** estiver marcada como **"Sim"** e o endereço IPv4 estiver dentro da faixa `169.254.x.y`, o host está em modo APIPA.

#### Como desabilitar o APIPA mantendo o cliente DHCP ativo:
Em ambientes corporativos roteados onde não se deseja que máquinas fiquem com endereços link-local:
1. Abra o Editor do Registro (`regedit`).
2. Navegue até a chave:
   ```text
   HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\<GUID_do_Adaptador>
   ```
3. Crie ou altere o valor `DWORD (32 bits)` com o nome:
   - **Nome:** `IPAutoconfigurationEnabled`
   - **Valor:** `0` (Desabilitado) ou `1` (Habilitado / Padrão).
4. Reinicie o adaptador ou o computador.

---

## 3. Diagnóstico e Resolução de Falhas na Rede (Visão Cisco Systems)

Em redes corporativas estruturadas com switches gerenciáveis, roteadores e firewalls, a ocorrência de endereços APIPA é um sintoma claro de falha na infraestrutura de rede ou na segurança de borda.

### 3.1. O Mecanismo de Sonda ARP (ARP Probe) e o DHCP Decline

Uma das causas mais comuns de queda em APIPA em redes com DHCP ativo ocorre durante a fase de verificação de duplicidade:

```
[Cliente]                                     [Rede / Switch / Firewall]
   │                                                      │
   │ 1. Conclui ciclo DORA e recebe a oferta de IP        │
   │ 2. Envia ARP Probe: "Alguém possui o IP 10.1.1.50?" ─>│
   │                                                      │
   │ <─── 3. Resposta ARP indevida (ex: Proxy ARP ativo) ─│
   │                                                      │
   │ 4. "Conflito detectado! Este IP já está em uso!"     │
   │ 5. Envia DHCP DECLINE ao servidor DHCP ─────────────>│
   │ 6. Recorre ao APIPA (169.254.x.y)                    │
```

- **Passo a Passo:**
  1. Após receber uma concessão de IP, o cliente não o aplica imediatamente.
  2. Ele emite uma sondagem ARP (**ARP Probe**) em broadcast para checar se algum outro dispositivo já está usando aquele IP.
  3. Se houver resposta (seja por um dispositivo real ou por um equipamento de segurança respondendo indevidamente), o cliente rejeita o endereço enviando uma mensagem **`DHCP Decline`** ao servidor.
  4. Sem um endereço alternativo disponível, o cliente entra em **APIPA**.

---

### 3.2. Seis Cenários Reais de Troubleshooting (Cisco TAC)

#### 🔹 Cenário 1: Proxy ARP no Firewall (ex: Cisco ASA / Firepower FTD)
* **Descrição do Problema:** Usuários em uma VLAN caem intermitentemente em APIPA. O firewall acumula várias entradas ARP associadas ao mesmo endereço MAC.
* **Causa Raiz:** A interface interna do Firewall está com o recurso Proxy ARP ativado. Quando o cliente dispara o *ARP Probe*, o firewall responde em nome do IP ofertado. O cliente deduz que há duplicidade e emite `DHCP Decline`.
* **Plano de Ação / Solução:** Desabilitar o Proxy ARP na interface interna do firewall:
  ```cisco
  sysopt noproxyarp inside
  ```

---

#### 🔹 Cenário 2: Escopos DHCP Duplicados ou Sobrepostos
* **Descrição do Problema:** Clientes recebem ofertas de IP, mas recusam imediatamente e assumem APIPA.
* **Causa Raiz:** Dois servidores DHCP ativos ou dois escopos distintos na mesma infraestrutura contêm a mesma faixa de IPs, tentando conceder o mesmo endereço para máquinas distintas simultaneamente.
* **Plano de Ação / Solução:** Auditar o servidor DHCP e redefinir os escopos para garantir exclusividade nos pools de endereçamento.

---

#### 🔹 Cenário 3: Configuração Cisco SDA (Software-Defined Access) com Catalyst 9300
* **Descrição do Problema:** Dispositivos sem fio associados a Access Points (APs) em VLANs puramente L2 não conseguem obter IP via DHCP e caem em APIPA.
* **Causa Raiz:** Por padrão, o túnel de acesso LISP na arquitetura SDA descarta pacotes de broadcast (`accessTunnelBroadcastDrop`), impedindo que a oferta DHCP do tipo broadcast chegue até o cliente sem fio.
* **Plano de Ação / Solução:** Habilitar a capacidade de encaminhamento (*flooding*) de broadcast na instância LISP do switch:
  ```cisco
  router lisp instance-id <id>
   flood access-tunnel
  ```

---

#### 🔹 Cenário 4: Defeito na Placa de Rede (Inundação de MACs / Bug de Adaptador)
* **Descrição do Problema:** A tabela de endereços MAC do switch apresenta descartes (`Drop`) e o número de sessões de autenticação 802.1X atinge limites extremos (ex: > 2.000 ou 10.000 sessões), travando novas conexões.
* **Causa Raiz:** Uma placa de rede de usuário com defeito elétrico, driver corrompido ou firmware defeituoso entra em um estado de mal funcionamento que gera e injeta ininterruptamente pacotes malformados com endereços MAC de origem gerados aleatoriamente (*MAC spoofing acidental*), saturando a memória e a tabela dot1x do switch.
* **Plano de Ação / Solução:** Identificar e isolar a porta física conectada ao adaptador defeituoso e configurar proteção de modo de host no switch:
  ```cisco
  authentication host-mode multi-domain
  ```
  *(Ou configurar Port Security limitando o número máximo de MACs por porta).*

---

#### 🔹 Cenário 5: Incompatibilidade de MTU (MTU Mismatch) no Tráfego EAP-TLS
* **Descrição do Problema:** Clientes corporativos falham na autenticação 802.1X via Cisco ISE e recebem IP APIPA.
* **Causa Raiz:** Pacotes de autenticação RADIUS/EAP-TLS (que transportam certificados digitais de autenticação volumosos) possuem tamanho superior ao MTU padrão permitido. Se o sistema global do switch estiver configurado com MTU menor (ex: `1998 bytes` - valor intermediário de plataforma) enquanto a interface de saída estiver com tamanho para Jumbo Frames (ex: `9198 bytes`), ocorre incompatibilidade de MTU (*MTU mismatch*), gerando fragmentação e descarte do pacote de autenticação. Sem autenticar no 802.1X, o tráfego DHCP é bloqueado.
* **Plano de Ação / Solução:** Padronizar a MTU em todo o trajeto dos pacotes (ex: 1500 bytes para Ethernet padrão) e reiniciar o switch para sincronizar os buffers:
  ```cisco
  system mtu 1500
  ```

---

#### 🔹 Cenário 6: Política de IPDT Guard (IP Device Tracking) e Failover de VMs
* **Descrição do Problema:** Máquinas virtuais ou servidores em cluster redundante de Alta Disponibilidade (HA) perdem conectividade e assumem APIPA logo após a troca de nó ativo (*failover*).
* **Causa Raiz:** A política de rastreamento de dispositivos (`device-tracking policy`) configurada com o nível de segurança `security-level guard` nos switches Catalyst descarta as respostas de sondagem ARP após o failover, impedindo o host de validar sua presença na rede.
* **Plano de Ação / Solução:** Alterar o nível de segurança da política de rastreamento para o modo `glean`:
  ```cisco
  device-tracking policy IPDT_POLICY
   security-level glean
  ```
  *(Nota técnica: Defeito de software documentado pela Cisco e corrigido a partir do Cisco IOS-XE 17.15.1).*

---

## 4. Resumo Prático para Administradores de Redes e Suporte

| Sintoma Observado | Provável Causa | Ação Recomendada |
| :--- | :--- | :--- |
| **Apenas 1 máquina com IP `169.254.x.x`** | Cabo de rede defeituoso, Wi-Fi com sinal fraco, driver de rede corrompido ou recusa pontual de DHCP. | Executar `ipconfig /renew`, inspecionar cabeamento, atualizar drivers da placa de rede. |
| **Todas as máquinas de uma VLAN com `169.254.x.x`** | Servidor DHCP inativo, escopo sem IPs livres ou ausência de `ip helper-address` (DHCP Relay) no roteador/SVI. | Validar serviço DHCP, conferir capacidade do pool e verificar o comando `ip helper-address` no gateway. |
| **Máquina recebe oferta de IP mas gera `DHCP Decline`** | Conflito de endereço IP ou dispositivo de rede respondendo indevidamente ao ARP Probe (ex: Firewall com Proxy ARP). | Analisar logs de conflito no DHCP, desativar proxy-arp no firewall e verificar sobreposição de escopos. |
| **Falha em rede corporativa com 802.1X / SDA** | Mismatch de MTU na autenticação EAP, bloqueio de broadcast no túnel SDA ou tabela dot1x saturada. | Equalizar MTU fim a fim, aplicar `flood access-tunnel` no LISP e ativar proteção de portas (*multi-domain*). |

---

## 5. Fontes e Referências

1. **Microsoft Learn**  
   - *Artigo:* [Como usar o endereçamento TCP/IP automático sem um servidor DHCP](https://learn.microsoft.com/pt-br/windows-server/troubleshoot/how-to-use-automatic-tcpip-addressing-without-a-dh)  
   - *Conteúdo de Referência:* Mecanismos de inicialização do cliente Windows, temporizadores de descoberta (3 e 5 min), chaves de Registro (`IPAutoconfigurationEnabled`).

2. **Cisco Systems - Documentação de Suporte e Troubleshooting**  
   - *Artigo:* [Identificar e Solucionar Falhas de Endereço APIPA na Rede](https://www.cisco.com/c/pt_br/support/docs/troubleshooting/222255-troubleshoot-apipa-address-failure-in-th.html)  
   - *Conteúdo de Referência:* Causas de fallback para APIPA em switches Catalyst, firewalls ASA/FTD, redes Cisco SDA, MTU Mismatch, Proxy ARP e IP Device Tracking (IPDT).

3. **IETF (Internet Engineering Task Force)**  
   - *RFC 3927:* Dynamic Configuration of IPv4 Link-Local Addresses.  
   - *RFC 4862:* IPv6 Stateless Address Autoconfiguration (SLAAC) & Link-Local Specifications.
