# Desativar auto-login no Windows Server 2025

Abra o Prompt de Comando (CMD) como Administrador e execute o comando abaixo para desativar o logon automático:

reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon /t REG_SZ /d 0 /f

Resumo rápido
- O comando força o valor da chave AutoAdminLogon para 0 (desativado), o que faz com que o Windows peça usuário e senha na próxima inicialização.

Detalhamento do comando
- reg add: ferramenta do Windows para adicionar ou modificar entradas no Registro via linha de comando.
- "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon": caminho da chave no registro (HKLM = HKEY_LOCAL_MACHINE).
- /v AutoAdminLogon: especifica o nome do valor que será alterado.
- /t REG_SZ: tipo do dado (string).
- /d 0: dados a gravar — 0 = desativado (1 = ativado).
- /f: força a alteração sem pedir confirmação.

Comandos úteis
- Verificar o valor atual:
  reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon

- Reativar o logon automático (se necessário):
  reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon /t REG_SZ /d 1 /f

Advertências e boas práticas
- Requer privilégios de Administrador. Faça backup do registro antes (ex.: reg export "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" backup.reg).
- Em ambientes de domínio, prefira configurar via Política de Grupo (GPO) em vez de editar o registro localmente.
- Teste alterações em uma máquina virtual antes de aplicar em servidores de produção.
- Alterar o Registro pode afetar o comportamento de login; certifique-se de que credenciais e políticas locais estejam consistentes.

Data: 10-05-2026
Aula: UC006 - Planejar e executar a manutenção de redes locais de computadores
