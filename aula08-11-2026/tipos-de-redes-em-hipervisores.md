# Tipos de redes em Hypervisores (e VMs)

Três tipos de redes são disponíveis para as VMs (Virtual Machines) em hypervisores:
- **Bridged**: uma rede que a VM atua direto na rede física, funcionando como um computador físico conectado à rede;
- **Host only**: uma rede onde somente as VMs e o seu host* se comunicam; 
- **NAT**: aqui a VM usa os serviços da rede através do host. O host fornece à VM acesso à internet e também os outros serviços que estiverem disponíveis na rede (servidor de arquivos, BD, etc...) como se ele mesmo estivesse utilizando.

Já segmentos de LAN (lan segments) é oferecido como uma rede layer 2 que somente as VMs utilizam para comunicar-se, sem a presença do host. 

*host é a máquina onde o hypervisor está em execução e que empresta recursos (CPU, RAM, armazenamento e rede) para que as VMs funcionem.

---

## 📚 Referências

- [Understanding Networking Types in Hosted Hypervisors](https://knowledge.broadcom.com/external/article/309842/understanding-networking-types-in-hosted.html)
