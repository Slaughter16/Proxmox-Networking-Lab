# Proxmox Networking Lab

This project documents the setup of a virtualized home lab using Proxmox, pfSense, Windows Server 2019, Windows 10 Client, Security Onion, Debian Admin Station, Kali Linux, Pi-hole, and Metasploitable2. It demonstrates network segmentation, firewalling, DNS filtering, and basic security monitoring using VLANs.

---

## 🧱 Lab Topology Overview

- **Proxmox VE Host** using `vmbr0` (WAN) and `vmbr1` (LAN)
- **pfSense** as firewall/router with VLAN trunking and DHCP
- **Pi-hole** for DNS filtering and ad-blocking
- VLANs for Clients, Servers, and Security Zones
- Multiple VMs representing typical enterprise roles

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

## 📶 VLAN Configuration

| **VLAN ID** | **Name / Purpose** | **Subnet**        | **Assigned VMs and IP Addresses**                                       |
|------------:|--------------------|-------------------|-------------------------------------------------------------------------|
| 10          | **Client**         | 192.168.10.0/24   | 🖥️ Windows 10 Client – `192.168.10.100`  <br> 🧑‍💼 Debian Admin Station – `192.168.10.X` *(fill in IP)* |
| 20          | **Server**         | 192.168.20.0/24   | 🗂️ Windows Server 2019 – `192.168.20.102`  <br> 💻 Meta VM – `192.168.20.101` <br> 🍍 Pi-hole – `192.168.20.2` |
| 30          | **Security**       | 192.168.30.0/24   | 🛡️ Kali Linux – `192.168.30.100`  <br> 📡 Security Onion – `192.168.30.X` *(fill in IP)* |


Include a visual map or VLAN table here if you want.


## 🔧 Key Features

- Simulated enterprise-grade VLAN segmentation
- DNS interception and redirection via Pi-hole
- Firewall rule testing using pfSense
- Troubleshoot DNS problems / Windows & Linux Configurations
