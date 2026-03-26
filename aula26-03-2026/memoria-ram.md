Memória RAM é onde o sistema operacional e os aplicativos funcionam em tempo de execução (enquanto estão abertos). Pode ser considerada a 'mesa de trabalho' do processador, pois para que um software seja executado, ele deve ser copiado para a RAM. Quando você abre um programa, os dados são copiados do armazenamento interno (HDD ou SSD) para a memória RAM, a fim de que o programa seja executado. Desta forma, todos os programas abertos neste exato momento estão funcionando na memória RAM. Ao fechar um App/programa, os dados importantes são salvos no HDD/SSD e o espaço da memória RAM é liberada. Se você gosta de jogar, abrir muitas abas no navegador ou vários programas simultaneamente, mais memória RAM será exigida do seu dispositivo. 
> Dica: Sem RAM um dispositivo liga, mas não dá tela. Geralmente o dispositivo emite avisos sonoros (longos beeps iguais e sequenciais) para informar que a RAM não foi identificada. Daí a importância de usar speakers na placa mãe dos desktops. 

#### Existem 2 testes interessantes para ver o funcionamento da RAM:
1) Ligue o computador e no Windows, abra o Gerenciador de Tarefas. Escolha a aba Desempenho e em seguida, Memória. Observe o gráfico e o tanto de RAM consumida pelos Apps e Sistema Operacional (SO).
2) Agora execute o navegador e comece a abrir sites em cada aba. Abra vários sites diferentes nas abas. No Gerenciador de Tarefas, vá na aba Processos, identifique o seu navegador e encontre na coluna Memória a quantidade de RAM utilizada. Em seguida, feche o browser para ver a RAM ser liberada. 

#### Principais características:
- Formato: DIMM (para desktop) ou SODIMM (para notebook)
- Capacidade de armazenamento - medido em GB
- Geração da memória (ou versão) - DDR2, DDR3, DDR4, DDR5. Cada geração não é compatível com a anterior ou próxima. Isso é definido pelo notch do módulo, que impede a instalação errada. 
- Velocidade - medido em MT/s ou Mhz, é a velocidade em que a RAM consegue receber ou enviar informações para o processador.  Cada geração tem suas especificações de velocidades mínimas e máximas, definidas pela JEDEC. Em cada módulo, há um chip SDP que armazena quais são as velocidades possíveis de operação para aquele módulo. Já o XMP é um overclock de fábrica, onde a velocidade da RAM é aumentada para obter mais desempenho. Tanto o SDP quanto XMP são lidos pela placa mãe para identificar as velocidades dos módulos instalados. 
Ex: DDR4 tem as seguintes velocidades:
- 2133Mhz
- 2400Mhz
- 2666Mhz
- 3000Mhz
- 3200Mhz e outras ainda maiores, fora da especificação original. 
Dica: O que acontece se instalar um módulo 2400 e outro 3200? A placa mãe irá limitar pela velocidade do módulo mais lento. 

- Latência - tempo de espera entre a solicitação de um dado e a entrega dele. É medido em ciclos de clock e quanto menor, melhor. Para cada velocidade de RAM existe seus timmings de latência padrão. 
- Canais de memória - Cada módulo de RAM tem 64bits de largura de banda. Você pode instalar apenas um módulo de RAM que o dispositivo irá funcionar. Mas se instalar 2 módulos de RAM em dual channel, a largura de banda para os módulos dobra, sai de 64bits e vai para 128bits. Isso não dobra a velocidade da RAM, mas acrescenta uma % de desempenho. Veja os vídeos comparativos. 
Dica: veja que placa mãe com 4 slots DIMM geralmente tem 2 cores nos slots, justamente para diferenciar os pares de DIMM que podem ser ligados em Dual Channel.

### Links úteis
[TUDO QUE VOCÊ DEVE SABER SOBRE MEMÓRIA RAM - MW Informática](https://www.youtube.com/watch?v=tOjtfpMmuFs&authuser=0)

[QUAD CHANNEL DE MEMÓRIA RAM MUDA MUITO DO SIMPLES DUAL CHANNEL? - MW Informática](https://www.youtube.com/watch?v=wYDgC5nmKjk&authuser=0)