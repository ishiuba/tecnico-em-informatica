Processador é o hardware que realiza os cálculos e processamento dos dados, a fim de que o dispositivo consiga rodar o sistema operacional e seus aplicativos. 

#### Principais características:
- Cores ou núcleos - onde ocorrem os cálculos e processamentos. 
- Clock do core/núcleo - a velocidade interna do core, medido em Ghz. Pense no clock como na rotação de um motor. Geralmente é mantido baixo, por questões de economia; mas quando é necessário, o clock aumenta para dar conta da demanda. Cada processador tem seus clocks máximos.
- Thread - funciona como um processador lógico. Não é um componente físico. Foi uma maneira dos fabricantes de processadores utilizarem de maneira mais otimizada a capacidade do pipeline do processador. Processadores podem ou não ser multi-threading. Quando tem essa tecnologia, cada core pode ter até 2 threads. Ex: 4 cores / 8 threads
- Cache - memória temporária de alto desempenho. Serve para armazenar dados temporários e/ou resultados de instruções calculadas pelo processador. Processadores tem 3 níveis (layers) de cache: L1, L2 e L3. O cache layer 1 (L1) tem poucos KB de capacidade, mas uma altíssima velocidade, comparado ao clock máximo do processador. Cada core tem o seu cache L1 exclusivo, não compartilhado. O cache layer 2 (L2) tem de alguns KB até alguns MB. Tem velocidade menor que o cache L1, porém maior capacidade. Cada core tem seu cache L2 exclusivo, não compartilhado. Por fim, o cache layer 3 (L3) tem alguns MB de capacidade e menor velocidade que L2, e é compartilhado entre todos os cores do processador. 
- Conjuntos de instruções - tipos de cálculos que o processador é capaz de realizar. Geralmente são conjuntos de várias instruções. Você pode verificar os conjuntos de instruções do seu processador através do CPU-Z.
- Socket - refere-se ao tipo e tamanho do encaixe utilizado para ligar o processador à placa mãe. Cada fabricante tem seus sockets e não há compatibilidade entre sockets diferentes. 
- TDP - Thermal Design Power é uma medida em Watts que define a capacidade de calor a ser dissipado pelo cooler, a fim de manter o processador dentro da temperatura adequada de funcionamento. 
- Litografia - é a tecnologia que mede o tamanho em que os transistores do processador foi criado. Litografia baixa significa que o hardware irá consumir menos energia, além de esquentar menos. Ou seja, quanto menor, melhor. Sua medida é em nanômetros (nm).

### Links úteis

[O que é um CPU Thread?](https://www.tomshardware.com/reviews/cpu-computing-thread-definition,5765.html)

[O que é processador: núcleos, threads, clock, cache e TDP](https://www.infowester.com/processadores.php)