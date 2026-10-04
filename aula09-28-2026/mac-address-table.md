# Tabela de Endereços MAC (MAC Address Table) e Switches

## Introdução

Em redes locais de computadores (LANs), os **switches** operam como o ponto central de conectividade cabeada (Ethernet), atuando predominantemente na **Camada 2 (Enlace de Dados)** do Modelo OSI e na camada de **Acesso à Rede** do Modelo TCP/IP.

O componente essencial que viabiliza o encaminhamento inteligente de dados em um switch é a **Tabela de Endereços MAC** (também conhecida tecnicamente como *CAM Table - Content Addressable Memory Table*).

---

## 📚 Referências

- [Planilha Prática: MAC Address Table Switch V1.1 (Google Drive)](https://drive.google.com/file/d/1uAgmhghQlKejYAK2R0ltXg-ZE7uS_POr/view)

---

## Comparação nos Modelos de Rede

| Modelo OSI (7 Camadas) | Modelo TCP/IP (4/5 Camadas) | Função e Protocolos Relacionados | Dispositivo Típico |
|---|---|---|---|
| **7. Aplicação**<br>**6. Apresentação**<br>**5. Sessão** | **Aplicação** | HTTPS, DNS, DHCP, SSH, SMTP, POP3, IMAP, SSL/TLS | Hosts / Servidores |
| **4. Transporte** | **Transporte** | Controle de fluxo, portas e integridade (TCP, UDP) | Gateways / Firewalls |
| **3. Rede** | **Internet** | Roteamento lógico e endereçamento IP (IPv4, IPv6, ICMP) | Roteador / Switch L3 |
| **2. Enlace de Dados** | **Acesso à Rede** | Endereçamento físico, enquadramento Ethernet e Wi-Fi | **Switch (L2)** / Access Point |
| **1. Física** | **Acesso à Rede / Física** | Sinais elétricos, ópticos e ondas de rádio (Bits 0 e 1) | Cabos, conectores, Hubs |

---

## Estrutura do Quadro Ethernet (Ethernet Frame)

Para enviar informações pela rede local, os dados gerados pelas camadas superiores são encapsulados em um **quadro Ethernet**:

```text
+-----------------------+--------------------+------------+--------------+
| MAC Destino (6 bytes) | MAC Origem (6 bytes)| Pacote IP  | Dados / FCS  |
+-----------------------+--------------------+------------+--------------+
```

- **MAC de Destino (Destination MAC):** Endereço físico da interface de rede (NIC) do destinatário.
- **MAC de Origem (Source MAC):** Endereço físico da interface do remetente.
- **Tipo / Protocolo / Pacote IP:** Identifica o protocolo da camada superior (ex.: IPv4 `0x0800`, IPv6 `0x86DD`, ARP `0x0806`).
- **Dados (Payload):** O conteúdo do pacote IP.
- **FCS (Frame Check Sequence / CRC):** Mecanismo de verificação de integridade no recebimento.

---

## Funcionamento da Tabela MAC (Ciclo de Vida)

Diferente de um *Hub* (que apenas replica sinais elétricos para todas as portas indiscriminadamente), o switch aprende dinamicamente a topologia da rede local através do seguinte processo:

### 1. Aprendizado (Learning)
Quando um host conectado à **Porta 1** transmite um quadro:
- O switch inspeciona o **MAC de Origem** do quadro recebido.
- Se o endereço ainda não estiver registrado, o switch cria uma entrada na tabela associando o endereço MAC à **Porta 1**.
- Cada entrada possui um temporizador (*Aging Timer* - tipicamente 300 segundos / 5 minutos). Se o dispositivo continuar transmitindo, o tempo é renovado. Caso fique inativo, a entrada é removida para liberar memória.

### 2. Consulta e Encaminhamento (Forwarding / Filtering)
O switch então inspeciona o **MAC de Destino**:
- **Se o MAC de destino já estiver na tabela:** O switch realiza o **encaminhamento direto (*forwarding*)** apenas para a porta específica associada. Nenhuma outra porta recebe aquele tráfego (*filtering*), garantindo eficiência e isolando domínios de colisão.
- **Se o MAC de destino NÃO estiver na tabela:** Ocorre a **inundação de unicast desconhecido (*Unknown Unicast Flooding*)**. O quadro é enviado para todas as portas ativas, **exceto** a porta que originou a mensagem.
- **Se for endereço de Broadcast (`FF:FF:FF:FF:FF:FF`) ou Multicast:** O quadro é replicado para todas as portas participantes daquela VLAN/domínio de broadcast.

---

## Exemplo Prático com Switch de 8 Portas

Simulação de encaminhamento em um switch com 8 portas:

| Porta | Endereço MAC Associado | Status / Tipo |
|---|---|---|
| **Porta 1** | `AA-AA-AA-AA-AA-01` | Host A (Estação de Trabalho) |
| **Porta 2** | `AA-AA-AA-AA-AA-02` | Host B (Estação de Trabalho) |
| **Porta 3** | `AA-AA-AA-AA-AA-03` | Servidor de Arquivos |
| **Porta 4** | `AA-AA-AA-AA-AA-04` | Impressora de Rede |
| **Porta 5** | *(Vazio / Desconhecido)* | Aguardando primeiro quadro |
| **Porta 6** | `AA-AA-AA-AA-AA-06` | Roteador / Gateway Padrão |
| **Porta 7** | *(Vazio / Desconhecido)* | Porta livre |
| **Porta 8** | *(Vazio / Desconhecido)* | Porta livre |

> **Cenário de Teste:**
> 1. Host A (`AA-AA-...-01` na Porta 1) quer enviar dados para o Servidor (`AA-AA-...-03` na Porta 3).
> 2. O switch lê a origem (`Porta 1`), confirma o registro de Host A.
> 3. O switch busca o destino (`Porta 3`), encontra o endereço e envia o quadro **exclusivamente pela Porta 3**.
> 4. As portas 2, 4, 5, 6, 7 e 8 não sofrem interrupção nem recebem cópia desse tráfego.
