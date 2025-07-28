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

- [pfSense](./pfsense/README.md)
- [Pi-hole](./pihole/README.md)
- [Troubleshooting](./troubleshoot/README.md)
- [Windows 10 Client](./win10-client/README.md)
- [Windows Server 2019](./winserver-2019/README.md)
- [Kali Linux](./kali-linux/README.md)
- [Meta (CentOS)](./meta/README.md)
- [Debian Admin Station](./debian-admin/README.md)
- [Security Onion](./security-onion/README.md)

## Network Overview

Include a visual map or VLAN table here if you want.
