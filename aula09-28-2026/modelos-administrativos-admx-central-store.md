# Modelos Administrativos (.admx/.adml), Central Store e Atualização Windows Server 2025

## Introdução

Os **Modelos Administrativos** (Administrative Templates) fornecem a interface descritiva baseada em XML usada pelo Editor de Política de Grupo para configurar as chaves de registro do Windows. Eles definem quais opções aparecem na seção *Modelos Administrativos* do console de gerenciamento, permitindo controlar recursos do sistema operacional, navegadores, componentes de rede e aplicativos da Microsoft.

---

## 📚 Referências e Downloads Oficiais

- [Criar e Gerenciar o Repositório Central (Central Store) de ADMX - Microsoft Learn](https://learn.microsoft.com/pt-br/troubleshoot/windows-client/group-policy/create-and-manage-central-store)
- [Download: Modelos Administrativos (.admx) para Windows 10/11 - Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=104003)
- [Download: Modelos Administrativos (.admx) para Windows 11 (2024 Update / 24H2) - Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=108430)
- [Download: Modelos Administrativos (.admx) para Windows Server 2025 - Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=108846)

---

## Estrutura dos Arquivos: `.admx` vs `.adml`

Desde o Windows Vista e Windows Server 2008, a Microsoft substituiu o formato legado `.adm` pela arquitetura dividida em dois tipos de arquivos baseados em XML:

| Arquivo | Função Técnica | Localização |
|---|---|---|
| **`.admx`** | **Arquivo de Definição:** Contém as regras técnicas, localizações no registro (`HKLM` ou `HKCU`), valores de chave e tipos de dados. É neutro em relação a idioma. | Raiz da pasta `PolicyDefinitions` |
| **`.adml`** | **Arquivo de Recurso de Idioma:** Fornece os textos legíveis por humanos, títulos, rótulos de botões e explicações detalhadas em cada idioma específico. | Subpastas de idioma (ex.: `PolicyDefinitions\pt-BR` ou `PolicyDefinitions\en-US`) |

> **Importante:** Todo arquivo `.admx` deve ter um arquivo `.adml` correspondente com o mesmo nome exato dentro da pasta do respectivo idioma (exemplo: `WindowsUpdate.admx` na raiz e `WindowsUpdate.adml` dentro de `pt-BR`).

---

## O Repositório Central (Central Store) no Active Directory

### O Problema do Repositório Local
Por padrão, o Editor de Política de Grupo lê os arquivos `.admx` da pasta local do Windows em `%SystemRoot%\PolicyDefinitions` (`C:\Windows\PolicyDefinitions`). Isso causa dois problemas graves:
1. **Inconsistência de Versões:** Se um administrador usa Windows 10 e outro usa Windows 11 ou Server 2025 para editar a mesma GPO, opções novas podem sumir ou gerar erros de análise (*parsing errors*).
2. **Desperdício e Lentidão no SYSVOL:** No formato antigo, cada GPO armazenava cópias inteiras dos modelos dentro de si, consumindo centenas de megabytes replicados entre todos os Controladores de Domínio.

### A Solução: Central Store no SYSVOL
A **Central Store** é uma pasta compartilhada centralizada no domínio que substitui o armazenamento local. Quando criada, **todas as estações de trabalho e servidores que editam GPOs passam a consultar automaticamente esse local único**.

#### Caminho da Central Store:
```text
\\<nome-do-dominio>\SYSVOL\<nome-do-dominio>\policies\PolicyDefinitions
```
*Exemplo prático:* `\\contoso.local\SYSVOL\contoso.local\policies\PolicyDefinitions`

#### Estrutura de Diretórios na Central Store:
```text
PolicyDefinitions\
├── en-US\                     <-- Arquivos .adml (Inglês)
├── pt-BR\                     <-- Arquivos .adml (Português Brasil)
├── ActiveDirectory.admx
├── BitLocker.admx
├── DNS.admx
├── WindowsFirewall.admx
└── WindowsUpdate.admx
```

---

## Passo a Passo para Criar e Configurar a Central Store

1. Conecte-se como Administrador do Domínio em um Controlador de Domínio (ou máquina com Ferramentas de Administração de Servidor Remoto - RSAT).
2. Abra o Explorador de Arquivos e acesse o caminho compartilhado:
   `\\<FQDN_do_Dominio>\SYSVOL\<FQDN_do_Dominio>\policies\`
3. Crie uma nova pasta com o nome exato: **`PolicyDefinitions`**.
4. Copie todos os arquivos `.admx` e as pastas de idioma (`pt-BR`, `en-US`) do seu computador com a versão mais recente do sistema operacional (localizados em `C:\Windows\PolicyDefinitions`) para a pasta recém-criada no SYSVOL.
5. Abra o **GPMC (`gpmc.msc`)**, edite qualquer GPO e navegue até *Modelos Administrativos*.
6. Confirme se a mensagem exibida no nó indica:
   > *"Modelos Administrativos: definições de política (arquivos ADMX) recuperadas do repositório central."*

---

## Atualização de Modelos Administrativos (Windows 11 24H2 e Windows Server 2025)

À medida que novas versões de sistemas operacionais e recursos são lançados, a Microsoft disponibiliza instaladores `.msi` contendo os novos arquivos `.admx` e `.adml`.

### Por que atualizar para Windows Server 2025?
O Windows Server 2025 e o Windows 11 (atualização 24H2) adicionam novos parâmetros críticos de segurança e gerenciamento, incluindo:
- **Proteções avançadas contra ataques de autenticação NTLM e novas opções Kerberos.**
- **Diretivas aprimoradas para criptografia SMB e firewall.**
- **Novas configurações de segurança de credenciais (Credential Guard / LSA).**
- **Políticas de controle de criptografia e gerenciamento de certificados.**

### Como Aplicar os Novos Modelos:
1. Baixe os pacotes `.msi` oficiais da Microsoft:
   - Pacote do **Windows 11 2024 Update (24H2)**.
   - Pacote do **Windows Server 2025**.
2. Execute a instalação em uma máquina de gerenciamento. Os arquivos serão extraídos (por padrão em `C:\Program Files (x86)\Microsoft Group Policy\Windows Server 2025\PolicyDefinitions`).
3. Copie os novos arquivos `.admx` e as respectivas subpastas de idiomas (`.adml`) sobrescrevendo os arquivos correspondentes na pasta **Central Store** (`PolicyDefinitions` no SYSVOL).
4. A replicação do Active Directory (DFSR) propagará automaticamente os novos modelos para todos os outros Controladores de Domínio da rede.
