# Proxmox Homelab - Disaster Recovery & Setup

Guia de sobrevivência para recriar o ambiente caso precise formatar do zero.

## Mapeamento e Estrutura de Discos
* **NVMe (local-lvm):** PVE Host, VM 101 (Debian 13) e LXC 100 (aaPanel /www).
* **HDD 1TB (storage-1tb):** Armazenamento de dados secundários e backups pesados.

## Lições Aprendidas & Soluções de Erros
1. **aaPanel sem rede no LXC:**
   * Caso o `apt` trave, aplicar DNS manual: `echo -e "nameserver 1.1.1.1\nnameserver 8.8.8.8" > /etc/resolv.conf`.
   * O LXC deve ser **privilegiado** (`unprivileged: 0`) para evitar falhas em regras do firewall nativo.
2. **Login Social do Google no aaPanel:**
   * **NÃO ATIVAR** sem HTTPS/Reverse Proxy ativo. O serviço `bt` trava.
   * Para destravar via terminal LXC: `/www/server/panel/bt 16` e `/www/server/panel/bt 1`.

## Subir Ambiente via Ansible
```bash
ansible-playbook -i inventory.ini playbooks/setup_pve_infrastructure.yml
```
