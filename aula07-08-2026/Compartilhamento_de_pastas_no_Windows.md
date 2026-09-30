# Compartilhamento de pastas no Windows

## Pré-requisitos para compartilhamento de pastas no Windows

- Definir um Hostname (nome do computador na rede)
- Identificar o Perfil de Rede e Firewall (Domínio, Publico e Privado)
- Verificar as Configurações avançadas de rede no perfil de rede que você está:
    - Compartilhamento de arquivos e pastas (on/off)
    - Descoberta de rede (on/off)
- Ter uma conta de usuário com senha (mandatório)
- Realizar a Configuração da Pasta Compartilhada
    - Guia Compartilhamento (permissão de compartilhamento)
    - Guia Segurança (permissão no sistema de arquivos)

## Verificações adicionais

Ainda devemos verificar:

- Caso esteja usando VM, qual tipo de rede configurada na placa de rede da VM (geralmente usamos NAT)
- Se o host físico consegue pingar na VM. Ex: `ping <hostname-da-VM>`
- Se o usuário e senha está definida na VM. Ao tentar acessar o compartilhamento, informar o usuário com os símbolos `.\` antes do nome do usuário, ex: `.\Senac`
- Se na VM foi instalado o 'VM Tools' ou 'Adicionais para convidado'
- Se as configurações de compartilhamento estão corretas:
    - Configurações avançadas de rede (no Windows)
    - Configurações de compartilhamento (na Pasta)
    - Configurações de segurança (na Pasta)

## Comandos úteis para CMD

- `hostname` → mostra o nome do computador na rede
- `ipconfig` → mostra as configurações básicas de rede de todos os adaptadores de rede do computador (físicos e virtuais)
- `ipconfig /all` → mostra todas as configurações de rede de todos os adaptadores de rede do computador (físicos e virtuais)
- `ping <hostname>` → testa conectividade com um host. Ex: `ping desktop-vm`
- `ping <IP>` → testa conectividade com um host. Ex: `ping 172.17.3.215`

### Dica: forçar uso do IPv4 no ping

Caso queira forçar o uso do IPv4, informe o parâmetro `-4`:

```cmd
ping -4 <hostname>
ping -4 <IP>
```
