# Políticas de Grupo: Política Local (LGPO) e GPO de Domínio

## Introdução

A **Política de Grupo (Group Policy)** é uma infraestrutura de gerenciamento e configuração integrada aos sistemas operacionais Windows (Windows 10, 11 e Windows Server). Ela permite que administradores de rede e técnicos de suporte configurem e apliquem parâmetros de segurança, restrições de software, scripts de inicialização/logon, personalizações de ambiente e configurações de rede de forma padronizada.

---

## 📚 Referências

- [Visão Geral da Política de Grupo (Group Policy Overview) - Microsoft Learn](https://learn.microsoft.com/pt-br/troubleshoot/windows-client/group-policy/group-policy-overview)

---

## Tipos de Política de Grupo

### 1. Política de Grupo Local (Local Group Policy - LGPO)
- **Escopo:** Aplica-se exclusivamente ao computador local onde é configurada.
- **Ferramenta de Acesso:** `gpedit.msc` (Editor de Política de Grupo Local).
- **Disponibilidade:** Presente nas edições Pro, Enterprise e Education do Windows (não disponível nativamente na versão Home).
- **Utilização:** Muito usada em computadores autônomos (*workgroup*), quiosques ou para definir uma linha de base antes da máquina ingressar em um domínio corporativo.

### 2. Objetos de Política de Grupo de Domínio (GPO - Group Policy Objects)
- **Escopo:** Armazenadas no Active Directory e distribuídas via rede para todos os computadores e usuários membros do domínio.
- **Ferramenta de Acesso:** `gpmc.msc` (Console de Gerenciamento de Política de Grupo / GPMC).
- **Armazenamento:**
  - **GPC (Group Policy Container):** Armazenado no Active Directory (atributos, GUID, versão e status).
  - **GPT (Group Policy Template):** Armazenado no compartilhamento compartilhado SYSVOL (`\\dominio\SYSVOL\dominio\Policies\{GUID}`) com os arquivos de configuração reais, scripts e definições de registro.

---

## Estrutura de Configuração

Tanto no `gpedit.msc` quanto no `gpmc.msc`, as diretivas são divididas em duas seções fundamentais:

```text
Editor de Política de Grupo
├── Configuração do Computador (Computer Configuration)
│   ├── Configurações de Software
│   ├── Configurações do Windows (Scripts de Inicialização/Encerramento, Segurança, Firewall)
│   └── Modelos Administrativos (Políticas baseadas em Registro do Sistema / HKLM)
└── Configuração do Usuário (User Configuration)
    ├── Configurações de Software
    ├── Configurações do Windows (Scripts de Logon/Logoff, Redirecionamento de Pastas)
    └── Modelos Administrativos (Políticas baseadas em Registro do Usuário / HKCU)
```

| Categoria | Momento de Aplicação | Alvo das Configurações | Exemplos Comuns |
|---|---|---|---|
| **Configuração do Computador** | Na inicialização do sistema operacional (*Boot*) | Todas as contas que usarem a máquina (`HKEY_LOCAL_MACHINE`) | Firewall do Windows, desativação de portas USB, BitLocker, atualizações do Windows Update |
| **Configuração do Usuário** | No momento do logon do usuário | Apenas a sessão daquele usuário (`HKEY_CURRENT_USER`) | Papel de parede padrão, bloqueio de Painel de Controle, restrição de execução de executáveis |

---

## Ordem de Processamento e Precedência (Regra LSDOU)

Quando um computador faz parte de um domínio Active Directory, múltiplas políticas podem ser aplicadas. O Windows processa as diretivas na seguinte ordem cronológica:

1. **L - Local:** Política de Grupo Local da máquina.
2. **S - Site:** Políticas vinculadas ao Site físico do Active Directory.
3. **D - Domain:** Políticas vinculadas ao Domínio (ex.: *Default Domain Policy*).
4. **OU - Organizational Unit:** Políticas vinculadas às Unidades Organizacionais (processadas hierarquicamente da OU pai para a OU filha mais próxima do objeto).

> **Princípio da Precedência:** A política aplicada **por último** sobrescreve as anteriores em caso de conflito de configurações. Portanto, a configuração de uma **OU filha** tem precedência sobre a de um Domínio, que por sua vez sobrescreve a Política Local.

### Exceções à Regra:
- **Imposto (Enforced / No Override):** Uma GPO de nível superior configurada como *Enforced* não pode ser sobrescrita por níveis inferiores.
- **Bloquear Herança (Block Inheritance):** Uma OU pode bloquear a herança de políticas superiores (exceto se a GPO superior tiver a opção *Enforced* ativa).

---

## Comandos Essenciais para Manutenção e Diagnóstico

Na rotina de suporte técnico e administração de redes locais, os seguintes comandos via prompt (`cmd`) ou PowerShell são fundamentais:

| Comando | Função Técnica |
|---|---|
| `gpupdate` | Atualiza em segundo plano as políticas que sofreram alterações. |
| `gpupdate /force` | Força a reaplicação imediata de **todas** as políticas (computador e usuário), mesmo que não tenham mudado. |
| `gpupdate /force /boot` | Força a atualização e reinicia o computador se houver diretivas pendentes de inicialização (ex.: instalação de software). |
| `gpresult /r` | Exibe no terminal o resumo das GPOs aplicadas, grupos de segurança e status do escopo. |
| `gpresult /h relatorio.html` | Exporta um relatório HTML gráfico detalhado com o status de cada configuração e possíveis erros de aplicação. |
| `rsop.msc` | Abre a interface gráfica do *Resultant Set of Policy* para inspecionar as políticas efetivas na máquina. |
