# Desativar auto-login no Windows Server 2025

Abrir CMD como Admin e execute a alteração no registro

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon /t REG_SZ /d 0 /f
```

Este comando serve para desativar o logon automático no Windows de forma direta e rápida, usando o Prompt de Comando (CMD).

**A resposta curta é:** ele força o valor da chave `AutoAdminLogon` a ser `0` (falso/desativado), o que obriga o Windows Server 2025 a pedir usuário e senha na próxima inicialização.

**Detalhamento do Comando**

Cada parte desse comando tem uma função específica para o sistema operacional:

- **reg add**: É a ferramenta nativa do Windows usada para adicionar ou modificar chaves e valores no Registro do sistema através da linha de comando.
- **"HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"**: Especifica o caminho exato dentro do registro onde a configuração está guardada.
- **HKLM** é a abreviação de **HKEY_LOCAL_MACHINE**, a colmeia do registro que armazena as configurações globais da máquina (válidas para todos os usuários).
- **/v AutoAdminLogon**: O parâmetro `/v` (de value) especifica o nome do valor que você quer modificar. Neste caso, a variável que controla se o logon automático está ligado ou desligado.
- **/t REG_SZ**: O parâmetro `/t` (de type) define o tipo de dado desse valor. `REG_SZ` significa que é uma string de texto simples.
- **/d 0**: O parâmetro `/d` (de data) define o conteúdo/dados que serão gravados. O número `0` significa Desativado. (Se fosse `1`, estaria ativando o logon automático).
- **/f**: O parâmetro `/f` (de force) força a alteração sem pedir confirmação. Se a chave já existir (e ela existe, criada pelo VMware), o Windows vai sobrescrevê-la silenciosamente sem exibir um aviso de "Tem certeza que deseja substituir?".
