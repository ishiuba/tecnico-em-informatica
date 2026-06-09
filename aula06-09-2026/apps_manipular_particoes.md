Existem algumas maneiras de gerenciar as partições de um HD/SSD, confira:
1. Usando o Gerenciador de Discos do Windows. 
Obs: Com o Gerenciador de Disco do Windows, nem todas as partições poderão ser listadas (e removidas), como as de sistema. Geralmente são pequenas partições antes e depois da principal. 

*Sendo assim, como remover estas partições de sistema?*

2. Gparted - o Gparted pode ser bootado através de pendrive com sua ISO dedicada. Outra opção é bootar um Ubuntu via pendrive, escolher a opção LIVE (demonstração) e ao concluir o boot, usar o Gparted. Outro modo e´ baixar e utilizar a ISO oficial. Usar o GParted para manipular partições em um computador com Windows instalado e funcionando, você deve tomar alguns cuidados, por conta da inicialização rápida. Confira ao final da atividade*.

3. Diskpart - este app do Windows não tem interface gráfica e deve ser acessado e usado via prompt de comando. É muito usado durante a instalação do Windows para alterar o esquema de partição, de MBR para GPT e vice versa. Veja o material anexo.
Dica: Use o prompt de comando como administrador para usar o diskpart.

4. E você, se recorda de outra maneira de remover as partições de sistema? Informe nos comentários.

> Usar o GParted para manipular partições em um computador com Windows instalado e funcionando, você deve tomar alguns cuidados antes:
>
1. No Windows, aperte Windows + R para abrir o 'executar', digitar control e clicar em ok. Isso irá abrir o painel de controle. 
No painel de controle, abrir Sistema e Segurança > Opções de Energia > Escolher a função dos botões de energia. Clicar em "Alterar Configurações não disponíveis no momento".
Na parte de baixo da interface, nas Configurações de desligamento, desmarque a opção: Ligar inicialização rápido (recomendado).

2. Reinicie o computador.

3. Confira se a opção está desmarcada.

4. Desligue a máquina. 
Dica: crie um atalho customizado de Desligar (shutdown /s /t 0)

5. Agora vc pode alterar as partições desta instalação do Windows usando o GParted. Mesmo assim, entenda que existem riscos nesta operação, portanto, faça backup antes de alterar as partições.

[Converter um disco em MBR ou GPT](https://learn.microsoft.com/pt-br/windows-server/storage/disk-management/change-an-mbr-disk-into-a-gpt-disk?authuser=0)

[NIUBI Partition Editor](https://www.hdd-tool.com/download.html?authuser=0)

[Partition Magic Manager](https://macrorit.com/partition-magic-manager/server-edition.html?authuser=0)

[Gparted](https://gparted.org/download.php?authuser=0)
