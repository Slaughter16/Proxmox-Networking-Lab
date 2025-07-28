# Proxmox Networking Lab

This project documents the setup of a virtualized home lab using **Proxmox**, **pfSense**, **Windows 2019 Server**, **Windows 10 Client**, **Security Onion**, **Debian Admin Machine**, **Kali Linux**, **Pi-hole**, and **Metasploitable2**. It covers VLAN segmentation, DNS troubleshooting, DHCP configuration, and Firewall configurations.

---

## 🧱 Lab Topology

- Proxmox VE Host with `vmbr0` and `vmbr1` linux bridges 
- pfSense as firewall/router (VM)
- Pi-hole as DNS server (LXC Ubunutu Container)
- VLAN10 - Clients (Win 10, Debian Admin Machine)
- VLAN20 - Server (Windows 2019 Server, Pi-hole, Metasploit)
- VLAN30 - Security (Kali, Security Onion)

---

## VM Documentation

- [Proxmox](./Proxmox/README.md)
- [pfSense](./pfSense/README.md)
- [Pi-hole](./Pi-hole/README.md)
- [Troubleshooting](./Troubleshoot/README.md)
- [Windows 10 Client](./Win10_Client/README.md)
- [Windows Server 2019](./WinServer2019/README.md)
- [Kali Linux](./Kali_Linux/README.md)
- [Meta (CentOS)](./Meta/README.md)
- [Debian Admin Station](./Debian_Admin/README.md)
- [Security Onion](./SecurityOnion/README.md)

## Network Overview

Include a visual map or VLAN table here if you want.
