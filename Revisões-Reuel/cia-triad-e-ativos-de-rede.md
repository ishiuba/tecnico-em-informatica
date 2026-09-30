Redes de computadores são estruturas físicas e lógicas que permitem hosts* se comunicarem e alcançar outros equipamentos de outras redes, incluindo a internet.

O hardware de redes são "equipamentos intermediários de rede" que são:
- Switch: interliga hosts através de cabos ethernet
- Roteador: interliga diferentes redes (LAN, WAN e LANs com endereços de rede diferentes). Na configuração de rede é chamado de "Gateway" Exemplo:
        LAN 1: 192.168.0.0 / 255.255.255.0
        LAN 2: 172.17.3.0 / 255.255.255.0
        WAN 1: Ligga com IP público dinâmico
- Conversor de mídia: converte o sinal de um tipo de mídia (fibra ótica) para outro tipo de mídia (ethernet)
- Access Point (AP): Cria um sinal de Wi-Fi e permite que equipamentos sem fio utilizem os serviços de rede LAN (DHCP, DNS, Internet, Servidores...). APs sempre dependem de uma rede ethernet para funcionar.
- Repetidor de Sinal Wi-Fi: estende o sinal de Wi-Fi para que tenha maior alcance. Dica: também existe repetidor de sinal para cabos ethernet e fibra ótica.
- Modem: O modem moderno (ONT ou ONU) é um equipamento com várias funções: conversor de mídia (fibra <--> ethernet), roteador, access point, switch e seu firmware tem servidor DHCP e possivelmente outros recursos.
- Cabos Ethernet: CAT5e, CAT6, CAT6a e CAT8. Dica: CAT7 não é homologado. CCA é uma liga metálica de alumínio e cobre usado para criar cabos ethernet mais baratos, leves e de menor qualidade. 

Toda comunicação de rede, seja com ou sem fio é medida ou divulgada em Mbps (megabits por segundo) ou Gbps (gigabits por segundo). Quando um dado é armazenado no seu HD ou SSD, a unidade de gravação ou leitura é realizada em MB/seg (megabytes por segundo).
1 bit = 0 ou 1
1 byte = 01010101 (um conjunto de 8 bits)
Para converter Mbps para MB/seg, devemos dividir o valor de Mbps por 8 para obter o valor em MB/seg.
Ex: 
800Mbps / 8 = 100MB/seg
400Mbps / 8 = 50MB/seg
1.2Gbps = 1200Mbps / 8 = 150MB/seg

Outros conceitos importantes:
PoE: Power over Ethernet - transmite energia através do cabo ethernet. Veja figura anexa para mais detalhes. 
Hosts: Servidores, Computadores, Notebook, Celular, TV, Console, Câmera IP, etc...

DHCP é um protocolo de distribuição de configurações de rede, que serve para automatizar a configuração dos hosts. Um servidor DHCP é um host ou equipamento de rede que tem o serviço DHCP habilitado e configurado para entregar as configurações a quem lhe solicitar.
Configurações:
- IP de início e IP de fim
- Máscara de sub-rede
- Gateway
- DNS1
- DNS2
- outros (opcionais)

O empréstimo do IP para um cliente se dá atrelando o endereço MAC da placa de rede com o endereço cedido. Ex:
Endereço MAC         IP cedido pelo servidor DHCP
60-C7-27-13-23-91 <-->  IP 192.168.1.201

Wi-Fi
802.11a - Opera na frequência de 5 GHz, com velocidade de até 54 Mbps.
802.11b - Opera na frequência de 2,4 GHz, com velocidade de até 11 Mbps.
802.11g - Opera na frequência de 2,4 GHz, com velocidade de até 54 Mbps.
802.11n (Wi-Fi 4) Opera nas frequências de 2,4 GHz e 5 GHz, com velocidade de até 600 Mbps.
802.11ac (Wi-Fi 5) Opera na frequência principal de 5 GHz, com velocidade superior a 1 Gbps.
802.11ax (Wi-Fi 6 e 6E): Opera nas frequências de 2,4 GHz e 5 GHz. O Wi-Fi 6E adiciona a banda de 6 GHz, com velocidade de até 9,6/10 Gbps.
802.11be (Wi-Fi 7): Opera simultaneamente nas frequências de 2,4 GHz, 5 GHz e 6 GHz, com velocidades que podem chegar até 40 Gbps.
