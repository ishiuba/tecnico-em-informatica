# Sobre Redes e IPv4

## 1 - Quais são as funções do protocolo IPv4?

**R:** Identificar um host (equipamento) em uma LAN. Também identifica um host na internet. 

**Dica:** Toda vez que o seu modem se conecta à internet, o seu provedor de acesso à internet te empresta temporariamente um IP público. 

---

## 2 - Como o IPv4 é representado em números decimais?

**R:** O IPv4 é representado em 4 partes separadas por pontos, com a estrutura: `___.___.___.___`

Onde cada parte pode conter o valor de 0 a 255 (256 possibilidades), ou seja, de `0.0.0.0` até `255.255.255.255` em qualquer combinação possível dentro deste intervalo. 

**Dica:** Lembre-se que existem categorias de endereços de IPv4 privados, públicos e reservados.

---

## 3 - Como o IPv4 é representado em números binários?

**R:** Vide planilha anexa (conversão de binário para decimal e vice-versa).

---

## 4 - Função e formato da máscara de sub-rede

**R:** A máscara de subrede tem a função de identificar, no endereço IP, qual parte identifica a rede e qual parte identifica o host. Lembre-se que o IP tem a função de diferenciar um host em uma rede. A conversão de binário para decimal está na planilha anexa. 

O endereço IP sempre começa identificando a rede e em seguida, o host.

**Quando em binário:**
- `1` = rede
- `0` = host

**Máscaras de sub-rede mais comuns:**
- `255.0.0.0` → <u>parte sublinhada identifica rede</u> e **negrito host**
- `255.255.0.0` → <u>parte sublinhada identifica rede</u> e **negrito host**
- `255.255.255.0` → <u>parte sublinhada identifica rede</u> e **negrito host**

---

## 5 - Como são identificadas redes iguais e redes diferentes?

**R:** A IA te disse que é necessário fazer um AND do endereço de IP com a máscara de sub-rede, e está correto: é a maneira que o host identifica qual rede está conectado. 

Geralmente temos mais facilidade de identificar o número da rede através da representação decimal e com a máscara de sub-rede, identificar a rede. 

- Se a porção do endereço de rede são **diferentes**, são **redes diferentes**. 
- Se o número da máscara de sub-rede das duas redes são **diferente**, também são **redes diferentes**. 
- Somente quando a porção da rede do endereço IP e a máscara de sub-rede forem **iguais** para concluir que a rede é a **mesma**.

---

## 6 - Como identificar o endereço de uma rede?

**Exemplo:**
```
IP:     192.168.55.187    ← parte sublinhada é rede, negrito é host
Máscara 255.255.255.0
```

Utilizando a máscara de subrede conseguimos identificar que a última parte do endereço IP (`___.___.___. xxx`) endereça os hosts. Esta parte tem 8 bits e pode ir de 0 até 255. 

- O primeiro endereço de IP deste exemplo (`192.168.55.0`) identifica a **rede**
- O último (`192.168.55.255`) é o **endereço de broadcast**, que serve para contatar todos os hosts desta rede.

---

## 7 - Como identificar os endereços de hosts (do primeiro ao último)?

**R:** Partindo da resposta da pergunta anterior (6), sabemos que o primeiro e último endereço são reservados para a rede e broadcast. Sendo assim, do segundo até o penúltimo endereço possíveis são usados para os hosts. 

**Usando o exemplo anterior:**
- `192.168.55.1` ← 1 é o **primeiro endereço de host**
- `192.168.55.254` ← 254 é o **último endereço de host**

---

## 8 - Explique os tipos de comunicação: unicast, multicast e broadcast

**R:**
- **Unicast** → comunicação de 1 para 1
- **Multicast** → comunicação de 1 para vários 
- **Broadcast** → comunicação de 1 para todos na rede

**Dica:** Lembre-se do WhatsApp

---

## 9 - Como identificar o endereço de broadcast de uma LAN e qual sua função?

**R:** Existem 2 tipos de broadcast: 

- **Broadcast de rede:** é o último endereço da rede e serve para enviar uma comunicação para todos os hosts daquela rede. 
- **Broadcast geral:** é último endereço IPv4 possível: `255.255.255.255` e serve para enviar uma comunicação para todos os hosts de todas as redes. Geralmente só é usando quando um computador precisa identificar um servidor DHCP. 

---

## 10 - Como criar sub-redes?

**R:** Através de VLSM. Assunto para próximas matérias. 

---

## 11 - Como interligar redes diferentes?

**R:** Através do equipamento de rede **roteador**. A função dele é interligar redes distintas.

---

## 📚 Referências

- [Planilha de Conversão Binário/Decimal](https://drive.google.com/file/d/101eOKe3DG-WBcWzahyDUonaWFsJ8Lg2W/view?usp=classroom_web&authuser=2)
