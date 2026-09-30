# Endereço IPv4 privados e públicos

Os endereços IPv4 são classificados em três categorias:
- públicos
- privados
- reservados

## Faixas de IPv4 Privado

Estas faixas de endereço IPv4 não são roteáveis na internet e servem exclusivamente para redes locais (casas, empresas, escolas, etc).

- `10.0.0.0` até `10.255.255.255`
- `172.16.0.0` até `172.31.255.255`
- `192.168.0.0` até `192.168.255.255`

## Faixas de IP Reservado (Uso Especial)

Estes endereços possuem funções técnicas específicas e não devem ser usados para navegação comum.

- `127.0.0.0` até `127.255.255.255` (O famoso 127.0.0.1 ou loopback, usado para o próprio computador conversar com ele mesmo).
- `169.254.0.0` até `169.254.255.255` (Endereço que o dispositivo adota temporariamente quando o servidor DHCP falha em entregar um IP).
- `224.0.0.0` até `239.255.255.255` (Multicast, usado para transmitir dados de um ponto para vários destinos ao mesmo tempo, como IPTV).
- `240.0.0.0` até `255.255.255.254` (Antiga Classe E, reservada para testes e pesquisas)
- `255.255.255.255` (Broadcast geral, usado para enviar uma mensagem para absolutamente todos os dispositivos da rede local).

## Faixas de IP Público

Os IPs públicos são todos aqueles que não estão listados nas categorias acima. Eles cobrem o restante do espaço de endereçamento de 1.0.0.0 até 223.255.255.255 (excluindo as exceções privadas e reservadas mencionadas). São os endereços que rodam livremente pelos servidores e roteadores de toda a internet mundial.

### Lista das Faixas de IP Público (IPv4)

- `1.0.0.0` até `9.255.255.255`
- `11.0.0.0` até `100.63.255.255` (Pula o bloco privado 10.x.x.x e para antes do CGNAT)
- `100.128.0.0` até `126.255.255.255` (Pula a faixa reservada ao CGNAT 100.64.0.0/10)
- `128.0.0.0` até `169.253.255.255` (Pula a faixa de Loopback 127.x.x.x e para antes do APIPA)
- `169.255.0.0` até `172.15.255.255` (Pula a faixa de autoconfiguração APIPA 169.254.x.x)
- `172.32.0.0` até `191.255.255.255` (Pula a faixa privada Classe B 172.16.x.x a 172.31.x.x)
- `192.0.1.0` até `192.0.1.255` (Pula o bloco de protocolos 192.0.0.0/24)
- `192.0.3.0` até `192.88.98.255` (Pula os IPs de testes 192.0.2.x)
- `192.88.100.0` até `192.167.255.255` (Pula o prefixo histórico Anycast 192.88.99.x)
- `192.169.0.0` até `198.17.255.255` (Pula a faixa privada Classe C 192.168.x.x)
- `198.20.0.0` até `203.0.112.255` (Pula o bloco de testes de benchmark 198.18.x.x e 198.19.x.x)
- `203.0.114.0` até `223.255.255.255` (Pula o bloco de testes 203.0.113.x)

A partir de `224.0.0.0` começam o Multicast e a antiga Classe E.

## Lista Completa e Linear do Espaço IPv4

| Faixa | Classificação | Descrição |
|-------|---------------|-----------|
| `0.0.0.0` a `0.255.255.255` | Reservado | Rede local atual / endereço de origem padrão |
| `1.0.0.0` a `9.255.255.255` | Público | --- |
| `10.0.0.0` a `10.255.255.255` | Privado | Classe A |
| `11.0.0.0` a `100.63.255.255` | Público | --- |
| `100.64.0.0` a `100.127.255.255` | Reservado | CGNAT - Provedores de internet |
| `100.128.0.0` a `126.255.255.255` | Público | --- |
| `127.0.0.0` a `127.255.255.255` | Reservado | Loopback / Localhost |
| `128.0.0.0` a `169.253.255.255` | Público | --- |
| `169.254.0.0` a `169.254.255.255` | Reservado | APIPA / Autoconfiguração |
| `169.255.0.0` a `172.15.255.255` | Público | --- |
| `172.16.0.0` a `172.31.255.255` | Privado | Classe B |
| `172.32.0.0` a `191.255.255.255` | Público | --- |
| `192.0.0.0` a `192.0.0.255` | Reservado | IETF - Protocolos internos |
| `192.0.1.0` a `192.0.1.255` | Público | --- |
| `192.0.2.0` a `192.0.2.255` | Reservado | TEST-NET-1 - Documentação e exemplos |
| `192.0.3.0` a `192.88.98.255` | Público | --- |
| `192.88.99.0` a `192.88.99.255` | Reservado | Antigo mapeamento IPv6 de Anycast |
| `192.88.100.0` a `192.167.255.255` | Público | --- |
| `192.168.0.0` a `192.168.255.255` | Privado | Classe C - Roteadores domésticos |
| `192.169.0.0` a `198.17.255.255` | Público | --- |
| `198.18.0.0` a `198.19.255.255` | Reservado | Testes de desempenho de redes |
| `198.20.0.0` a `203.0.112.255` | Público | --- |
| `203.0.113.0` a `203.0.113.255` | Reservado | TEST-NET-2 - Documentação e exemplos |
| `203.0.114.0` a `223.255.255.255` | Público | --- |
| `224.0.0.0` a `239.255.255.255` | Reservado | Multicast / IPTV |
| `240.0.0.0` a `255.255.255.254` | Reservado | Uso futuro / Pesquisas / Antiga Classe E |
| `255.255.255.255` | Reservado | Broadcast de rede limitado |
