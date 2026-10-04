# Active Directory Domain Services (AD DS)

## Introdução

O **Active Directory Domain Services (AD DS)** é o serviço de diretório centralizado da Microsoft para sistemas operacionais Windows Server. Ele fornece uma base de dados distribuída e hierárquica que armazena informações sobre os recursos da rede local (usuários, grupos, computadores, servidores, impressoras e compartilhamentos), provendo serviços de autenticação, autorização e gerenciamento centralizado.

Em ambientes corporativos e de manutenção de redes locais (UC006), o AD DS é a espinha dorsal para controle de acesso, aplicação de políticas de segurança e inventário de ativos.

---

## 📚 Referências

- [Roteiro de Aprendizagem: Serviços de Domínio Active Directory - Microsoft Learn](https://learn.microsoft.com/pt-br/training/paths/active-directory-domain-services/?authuser=0)

---

## Estrutura Lógica do AD DS

A estrutura lógica define como os recursos são organizados e como as políticas administrativas são delegadas, independentemente da localização física dos servidores:

### 1. Objetos e Atributos
- **Objetos:** Representam entidades individuais na rede (ex.: um usuário, um computador ou uma impressora).
- **Atributos:** Características que descrevem o objeto (ex.: nome, e-mail, telefone, SID, senha criptografada).
- **Esquema (Schema):** Define o conjunto de regras que determinam os tipos de objetos e atributos permitidos na base de dados.

### 2. Unidades Organizacionais (OUs - Organizational Units)
- Contêineres lógicos dentro de um domínio usados para agrupar usuários, computadores e outros objetos.
- Permitem **delegação administrativa** (conceder permissões a um suporte técnico para redefinir senhas apenas em uma OU específica).
- São o menor nível de contêiner ao qual **Políticas de Grupo (GPOs)** podem ser diretamente vinculadas.

### 3. Domínios (Domains)
- Unidade estrutural fundamental do AD DS.
- Representa um limite administrativo e de replicação para objetos que compartilham uma política de segurança comum.
- Identificado por um nome FQDN (Fully Qualified Domain Name), ex.: `empresa.local` ou `corp.contoso.com`.

### 4. Árvores (Trees) e Florestas (Forests)
- **Árvore de Domínios:** Coleção de um ou mais domínios que compartilham um namespace DNS contíguo (ex.: `filial.empresa.local` e `empresa.local`).
- **Floresta:** O limite máximo de segurança e autoridade no AD DS. Uma floresta compartilha um único Esquema, um único Catálogo Global e relações de confiança transitivas Kerberos entre todos os domínios membros.

---

## Estrutura Física do AD DS

A estrutura física reflete como o tráfego de rede e a replicação de dados ocorrem na infraestrutura real:

### 1. Controladores de Domínio (Domain Controllers - DCs)
- Servidores que executam a função AD DS e armazenam uma réplica do banco de dados do diretório (`ntds.dit`).
- Autenticam logons de usuários, resolvem permissões e processam alterações de diretório.
- Suportam replicação multi-mestre (alterações feitas em um DC são propagadas para os demais).

### 2. Sites e Sub-redes (Sites and Subnets)
- Um **Site** representa uma localização física geográfica bem conectada (ex.: Matriz Curitiba, Filial Londrina).
- Associa intervalos de IP (sub-redes) a sites específicos.
- **Objetivo:** Otimizar o tráfego de replicação entre links lentos (WAN) e garantir que as estações de trabalho autentiquem no DC fisicamente mais próximo.

---

## Componentes Críticos de Infraestrutura

### Relação Mandatória com o DNS (Domain Name System)
O AD DS não funciona sem o serviço de DNS. O DNS é utilizado para localização dinâmica de serviços através de registros SRV:
- Permite que uma estação cliente descubra quem são os Controladores de Domínio ativos (`_ldap._tcp.dc._msdcs.dominio.local`) e servidores Kerberos (`_kerberos._tcp.dominio.local`).

### Catálogo Global (Global Catalog - GC)
- Um Controlador de Domínio configurado como GC mantém uma réplica completa de todos os objetos do seu domínio e uma réplica parcial de atributos dos objetos de todos os outros domínios da floresta.
- Essencial para buscas universais e validação de pertencimento a grupos durante o logon.

### Funções FSMO (Flexible Single Master Operations)
Embora a maior parte da replicação seja multi-mestre, cinco funções críticas requerem um único mestre responsável:

| Nível | Função FSMO | Responsabilidade |
|---|---|---|
| **Floresta** | Schema Master | Controla alterações no esquema do AD DS. |
| **Floresta** | Domain Naming Master | Controla a adição ou remoção de domínios na floresta. |
| **Domínio** | RID Master | Aloca blocos de RIDs (Relative IDs) para criação de novos SIDs. |
| **Domínio** | PDC Emulator | Sincroniza o relógio da rede (NTP), gerencia alterações de senha e compatibilidade legada. |
| **Domínio** | Infrastructure Master | Atualiza referências entre objetos de diferentes domínios. |

---

## Protocolos de Autenticação

- **Kerberos v5:** Protocolo padrão de autenticação do Active Directory. Utiliza tickets cifrados (TGT e TGS) e criptografia simétrica/assimétrica, eliminando a transmissão de senhas em texto puro na rede.
- **NTLM (NT LAN Manager):** Protocolo legado mantido para compatibilidade reversa com sistemas antigos (desaconselhado em redes modernas por vulnerabilidades de repetição e hash).
- **LDAP / LDAPS (portas 389 / 636):** Protocolo de consulta e manipulação dos registros do diretório.
