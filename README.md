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

## 📶 VLAN Configuration

| **VLAN ID** | **Name / Purpose** | **Subnet**        | **Assigned VMs and IP Addresses**                                       |
|------------:|--------------------|-------------------|-------------------------------------------------------------------------|
| 10          | **Client**         | 192.168.10.0/24   | 🖥️ Windows 10 Client – `192.168.10.100`  <br> 🧑‍💼 Debian Admin Station – `192.168.10.X` *(fill in IP)* |
| 20          | **Server**         | 192.168.20.0/24   | 🗂️ Windows Server 2019 – `192.168.20.102`  <br> 💻 Meta VM – `192.168.20.101` <br> 🍍 Pi-hole – `192.168.20.2` |
| 30          | **Security**       | 192.168.30.0/24   | 🛡️ Kali Linux – `192.168.30.100`  <br> 📡 Security Onion – `192.168.30.X` *(fill in IP)* |


Include a visual map or VLAN table here if you want.
