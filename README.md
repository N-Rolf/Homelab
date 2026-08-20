# Homelab
A single physical server being built out, phase by phase, into a small enterprise-style environment — storage, networking with VLANs, Active Directory, a SIEM, a ticketing system, and monitoring. Built to demonstrate practical IT skills for help desk / sysadmin / network roles.

## Table of Contents
- [Apps](link) - an overview of currently installed apps and services
- [Overview](https://github.com/N-Rolf/Homelab/tree/main/docs/overview) - Hardware, hypervisor, and initial setup
- [Media Server](https://github.com/N-Rolf/Homelab/tree/main/docs/storage-and-media) - Samba, Jellyfin
- [Cloud](link) - NextCloud
- [Docker](link) - Gitea, Immich, Vaultwarden, Portainer
- [Networking](link) - Hardware, opnSense, VLAN, VPN, Firewall
- [Windows AD](link) - Windows server
- [Security](link) - Security, Wazuh
- [IT Operations](link) - Ticketing, backups
- [Monitoring](link) - Grafana


## Status

| Item | Focus | Status |
|---|---|---|
| Server Prep | Proxmox install, BIOS, storage layout | ✅ Done |
| Storage & Media | Samba, Jellyfin | ✅ Done |
| Cloud | NextCloud | ⬜ Not started |
| Docker Services | Gitea, Immich, Vaultwarden, Portainer | 🟡 In progress |
| Networking | VLANs, OPNsense, VPN, Firewall | ⬜ Not started, Awaiting Hardware |
| Windows Server | AD, GPO's | ⬜ Not started |
| Security | Wazuh | ⬜ Not started |
| IT | ticketing, backups | ⬜ Not started |
| Grafana | Grafana | ⬜ Not started |


## Architecture

[Diagram](https://raw.githubusercontent.com/N-Rolf/Homelab/main/images/networkDiagram01.jpg)

**Current hardware:** Dell OptiPlex 7060 SFF — Intel i7-8700 (6C/12T), 32GB RAM, 512GB NVMe (Proxmox boot/VM disk) + 8TB Seagate IronWolf (bulk storage). 

---

