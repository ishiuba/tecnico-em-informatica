### O protocolo IP serve para endereçar um computador em uma Rede.

Existem duas versões do protocolo IP: IPv4 e IPv6.

Neste momento vamos focar no IPv4.

O IPv4 tem 32bits, tem 4 octetos e é representado no formato decimal no seguinte formato: xxx.yyy.zzz.www

Onde cada xxx pode ser de 0 até 255.

O endereço IP não só identifica o dispositivo, mas também identifica a rede onde aquela máquina está. Para isso, necessitamos dividir o endereço IP em duas partes:

* A parte que identifica a rede no começo do endereço
* A parte que identifica os hosts (dispositivos) no final do endereço



E quem faz isso é a Máscara de Sub-rede. Os formatos mais comuns são:

255.0.0.0

255.255.0.0

255.255.255.0

Onde a parte que tem "255" identifica a rede

E a parte que tem "0" identifica os hosts (equipamentos)



Ainda existem mais algumas configurações importantes que o host recebe ao entrar na rede:

* Gateway (roteador da rede). A função do roteador é interligar redes, incluindo a 'rede' internet.
* Servidor DNS1 e Servidor DNS2. A função do protocolo DNS é traduzir domínios (ex: www.carimbo.com.br) para endereço IP.



O protocolo IP também tem uma 'divisão' entre endereços públicos (para internet) e privados (para redes locais). Os endereços privados são:

* 10.0.0.0 até 10.255.255.255
* 172.16.0.0 até 172.31.255.255
* 192.168.0.0 até 192.168.255.255



Estes tipos de endereços não se misturam: IPs públicos não existem em redes locais e endereços privados não são reconhecidos na internet.



Para visualizar as configurações de IP no Windows, abra o CMD e digite:

ipconfig    (ver configurações resumidas de IP de todos os adaptadores de rede)

ipconfig /all (ver todas as configurações de IP de todos os adaptadores de rede)

ping <endereço> (testa a conectividade de rede com o <endereço>, que pode ser um IP, um domínio ou o nome de um host)

hostname (mostra o nome do computador na rede local)

