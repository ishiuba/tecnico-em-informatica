# Desativar auto-login Windows Server 2025

Abrir CMD como Administrador e execute o comando abaixo para desativar o logon automático no Windows Server 2025:

```powershell
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon /t REG_SZ /d 0 /f
```

Resumo: esse comando força o valor da chave AutoAdminLogon para 0 (desativado), fazendo com que o Windows solicite usuário e senha na próxima inicialização.

Detalhamento do comando

- `reg add`: ferramenta nativa do Windows para adicionar ou modificar chaves e valores no Registro via linha de comando.
- `"HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"`: caminho no Registro onde a configuração de logon está armazenada.
  - `HKLM` = HKEY_LOCAL_MACHINE, que contém configurações válidas para todos os usuários da máquina.
- `/v AutoAdminLogon`: especifica o nome do valor (value) que será alterado — controla o logon automático.
- `/t REG_SZ`: define o tipo de dado como string (REG_SZ).
- `/d 0`: define o dado/valor para `0` (desativado). Se fosse `1`, estaria ativando o logon automático.
- `/f`: força a alteração sem pedir confirmação (sobrescreve silenciosamente se o valor já existir).

Observações

- Use com cuidado em servidores de produção: verifique que você tem acesso físico ou credenciais de administrador para realizar o login após a alteração.
- Em ambientes gerenciados (ex.: VMs provisionadas por VMware, imagens automatizadas), a chave pode ser reaplicada por scripts de inicialização — verifique políticas e automações locais.
- Para reativar o logon automático, defina o valor para `1` e confirme que os outros valores relacionados ao Winlogon (ex.: `DefaultUserName`, `DefaultPassword`) estejam corretamente configurados (atenção: armazenar senhas em texto claro no Registro é inseguro).
