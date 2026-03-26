HDD e SSD são dispositivos de armazenamento internos e tem a função de armazenar dados, mesmo sem estarem ligados à energia (não voláteis). Todos os aplicativos que você instala, como o sistema operacional e games, são armazenados no HD ou SSD.

#### Características de HDD:
- Marca e Modelo - existem boas marcas para HDD, como Seagate, Western Digital e Samsung. Marcas menos conhecidas como HGST e Fujitsu também são confiáveis. 
- Capacidade: em GB. Lembre-se que os fabricantes podem identificar a capacidade de 1GB = 1.000.000.000 de bytes, enquanto o Sistema Operacional lê 1GB = 1024MB e isso causa diferenças na capacidade total formatada e anunciada. 
- Barramento: HDDs geralmente usam barramento SATA
- Rotação: Em geral 5400RPM ou 7200RPM
- Cache: Todos os HDDs tem cache de alguns MB. Entre 8MB até 128MB. 
- Formato: 2,5" para laptop e 3.5" para desktops
- Vida útil: MTBF (Mean Time Between Failures ou Tempo médio entre falhas), medido em horas. 
- Atenção: HDD contém peças móveis e JAMAIS deve ser alterado de lugar ou movido enquanto ligado. HDDs são sensíveis a qualidade da energia elétrica que recebem e costumam durar menos com fontes ruins e 'queimam' com raios e sobretensão.

#### Características de SSD:
- Marca e Modelo - existem boas marcas, como Western Digital e Samsung. Existem marcas mainstream, como Kingston, que tem modelos melhores e modelos mais simples.
- Capacidade: em GB. Lembre-se que os fabricantes podem identificar a capacidade de 1GB = 1.000.000.000 de bytes, enquanto o Sistema Operacional (SO) lê 1GB = 1024MB e isso causa diferenças na capacidade total formatada e anunciada. 
- Formato e Barramento: 
       - Formato 2,5": Barramento SATA
       - Formato M2: Pode ter barramento SATA ou PCIe. Os que tem barramento SATA também são chamados de NGFF. Os que tem barramento PCIe são conhecidos por NVMe. Atenção, pois existem as 'keys' ou formatos diferentes da conexão M2. Veja o anexo da InfoWester.
- Vida útil: Combina MTBF e TBW (Terabytes Written ou Terabytes gravados). Os módulos de memória de um SSD tem uma capacidade limitada de vezes em que pode ser regravado. 
- Overprovisioning ou OP - É uma parte da capacidade do SSD reservado para que o controlador do SSD realize Garbage collection ou coleta de lixo, a fim de aumentar a durabilidade do SSD e também de manter a performance durante o uso contínuo. 
- Cache - Alguns tem cache físico (preferível), outros usam a RAM do computador para cache, ou seja HMB, ou Host Memory Buffer, e por fim, alguns SSD não tem cache nenhum, também chamado de DRAMLess. 
- TRIM - Trata-se do processo de coleta de lixo e balanceamento do uso dos módulos de armazenamento do SSD.
### Links úteis

[NVMe versus SATA: Qual a diferença?
](https://www.kingston.com/br/blog/pc-performance/nvme-vs-sata)

[2 tipos de SSDs M.2: SATA e NVMe](https://www.kingston.com/br/blog/pc-performance/two-types-m2-vs-ssd)

[O que é SSD M.2? (2280, 2260 ou 2242)](https://www.infowester.com/ssd-m2-nvme.php)

[Entendendo excesso de provisionamento (OP)](https://www.kingston.com/br/blog/pc-performance/overprovisioning)

[Over-provisioning](https://download.semiconductor.samsung.com/resources/others/Samsung_SSD_845DC_04_Over-provisioning.pdf)

[A importância dos processos de Coleta de lixo e TRIM no desempenho do SSD](https://www.kingston.com/br/blog/pc-performance/ssd-garbage-collection-trim-explained)
