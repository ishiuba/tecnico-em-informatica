# Boas Práticas de Segurança no Windows

## Por que usar uma conta comum ao invés de conta administrador?

Uma das melhores práticas de segurança digital é usar uma conta de usuário comum no dia a dia, mesmo que o computador seja seu. Essa abordagem traz proteção em múltiplos níveis e reduz significativamente os riscos de segurança.

---

## 1. Proteção contra Malwares e Vírus

### Conta Administrador
Quando você está logado como administrador, qualquer vírus que você baixe acidentalmente herda seus privilégios de "superpotência". O malware pode:
- Instalar-se silenciosamente nas pastas do sistema
- Alterar configurações do Windows
- Executar-se sem avisos

### Conta Comum
Com uma conta de usuário padrão, o Windows adiciona uma camada de proteção:
- Se um vírus tentar executar, o sistema o bloqueia imediatamente
- Uma tela de aviso aparece pedindo a senha do administrador
- Como o vírus não tem a senha, sua execução é impedida

**Resultado:** Proteção automática contra código malicioso que tenta elevar seus privilégios.

---

## 2. Proteção contra Erros Próprios (ou de Terceiros)

### Conta Administrador
- É fácil deletar pastas importantes do sistema acidentalmente
- Um clique errado pode desconfigurar um serviço essencial
- Programas de terceiros podem alterar o comportamento do Windows sem restrições

### Conta Comum
- O sistema fica "blindado" contra alterações críticas
- Você não consegue modificar arquivos que afetam outros usuários
- Se alguém mais usa o PC nessa conta (criança, amigo), o dano possível é limitado
- O Windows força confirmação para qualquer ação que necessite privilégios elevados

**Resultado:** Segurança em camadas que impede acidentes que podem danificar o sistema inteiro.

---

## 3. Ransomwares: A Ameaça Mais Perigosa Hoje

### O que é um Ransomware?

Um ransomware (ransom = resgate + malware = software malicioso) é um vírus que **criptografa seus arquivos e cobra resgate** para devolvê-los. Diferente de vírus comuns que roubam dados, ele os bloqueia e pede dinheiro (geralmente em Bitcoin) pela desbloqueio.

É considerado atualmente a maior ameaça digital para empresas e usuários comuns.

### Cenário 1: Infectado enquanto administrador

Imagine o ransomware como um invasor com uma "chave mestra" do seu castelo:

**Bloqueio Total**
- Criptografa todas as suas fotos, documentos e vídeos
- Bloqueia files de todos os usuários do computador
- Invade pendrives, HDs externos e SSDs conectados

**Destruição das Defesas**
- Desativa o Windows Defender e outros antivírus
- Deleta "Pontos de Restauração do Sistema" (backup de emergência)
- Remove toda possibilidade de recuperação rápida

**Resultado:** Computador completamente inutilizável, com dados de todos os usuários criptografados.

### Cenário 2: Infectado enquanto usuário comum

Agora o "invasor" está trancado em uma sala com apenas os arquivos daquela conta:

**Barreira de Entrada**
- Para instalar-se e criar serviços ocultos, o ransomware precisa de privilégios administrativos
- O Windows bloqueia e pede a senha do administrador
- Sem a senha, o vírus não consegue prosseguir

**Acesso Limitado**
- Não consegue tocar em arquivos de outros usuários
- Não pode acessar pastas do sistema
- Fica confinado apenas aos dados locais daquela conta

**Antivírus Protegido**
- O vírus não tem poder para desativar o Windows Defender
- O antivírus continua rodando com privilégios maiores que o do malware
- Consegue detectar e eliminar o ransomware em tempo real

**Resultado:** Danos limitados. Apenas os arquivos da conta infectada correm risco, e ainda com proteção ativa do antivírus.

---

## É possível quebrar a criptografia do Ransomware?

**Não.** 

Os ransomwares modernos usam criptografia de nível militar (AES-256). A matemática é tão robusta que tentar adivinhar a chave levaria séculos, mesmo com computadores extremamente potentes.

**Por isso, a estratégia correta é a prevenção:**
- Usar conta comum para navegação diária
- Manter backups em nuvem ou HDs desconectados
- Manter o antivírus atualizado
- Evitar baixar arquivos de fontes desconhecidas

---

## Resumo Prático

| Aspecto | Conta Administrador | Conta Comum |
|--------|-------------------|------------|
| **Malware** | Herda permissões totais | Bloqueado ou confinado |
| **Erros acidentais** | Risco alto ao sistema todo | Danos limitados à conta |
| **Ransomware** | Acesso total a todos os dados | Confinado a uma conta |
| **Antivírus** | Pode ser desativado | Protegido e ativo |
| **Recuperação** | Difícil ou impossível | Muito mais fácil |

---

## Recomendação Final

Usar o PC como usuário comum é como dirigir com cinto de segurança e airbag ligados. Dá um pouco mais de trabalho (digitar a senha do administrador quando necessário), mas a proteção é incomparavelmente maior.

**Em ambientes corporativos e empresas sérias, ninguém trabalha como administrador no dia a dia. É a regra número um de segurança em tecnologia.**

---

## Referências

> ⚠️ **Nota importante:** Nem sempre IA está certa. As fontes abaixo permitem que você verifique de forma independente as informações apresentadas.

- [Implementing Least Privilege Administrative Models](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models)
- [Principle of Least Privilege](https://www.cloudflare.com/pt-br/learning/access-management/principle-of-least-privilege/)
- [Protect your PC from ransomware](https://support.microsoft.com/pt-br/security/protect-your-pc-from-ransomware)
- [Zero Trust Maturity Model](https://duo.com/learn/zero-trust-maturity-model)
