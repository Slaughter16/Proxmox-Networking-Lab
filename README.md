# Proxmox Networking Lab

This project documents the setup of a virtualized home lab using Proxmox, pfSense, Windows Server 2019, Windows 10 Client, Security Onion, Debian Admin Station, Kali Linux, Pi-hole, and Metasploitable2. It demonstrates network segmentation, firewalling, DNS filtering, and basic security monitoring using VLANs.

---

## 🧱 Lab Topology Overview

- **Proxmox VE** with `vmbr0` (WAN) and `vmbr1` (LAN)
- **pfSense** as router/firewall using VLAN trunking
- **Pi-hole** for DNS filtering and ad blocking
- Simulated VLANs for Clients, Servers, and Security Zones
- Multiple VMs representing real-world roles in a segmented network

---

## 🖥️ Virtual Machines

| VM Name             | Role                            | OS / Description                     |
|---------------------|----------------------------------|--------------------------------------|
| Proxmox             | Lab Hypervisor                   | Proxmox VE                           |
| pfSense             | VLAN Routing & Firewall          | pfSense CE                           |
| Windows 10 Client   | End-user Testing Environment     | Windows 10 Pro                       |
| Windows Server 2019 | Active Directory / File Sharing  | Windows Server 2019 Std              |
| Debian Admin        | Network Admin Workstation        | Debian Linux                         |
| Kali Linux          | Penetration Testing Tools        | Kali Rolling                         |
| Meta (CentOS)       | Vulnerable VM for Exploitation   | Metasploitable 2                     |
| Pi-hole             | DNS Sinkhole & Ad Blocker        | Pi-hole on Debian                    |
| Security Onion      | Intrusion Detection / Monitoring | Security Onion (SO2)                 |

---

## 🌐 VLAN Configuration

| **VLAN ID** | **Name / Purpose** | **Subnet**        | **Assigned VMs and IP Addresses**                                       |
|------------:|--------------------|-------------------|-------------------------------------------------------------------------|
| 10          | **Client**         | 192.168.10.0/24   | 🖥️ Windows 10 Client – `192.168.10.100`  <br> 🧑‍💼 Debian Admin Station – `192.168.10.101`|
| 20          | **Server**         | 192.168.20.0/24   | 🗂️ Windows Server 2019 – `192.168.20.102`  <br> 💻 Meta VM – `192.168.20.101` <br> 🍍 Pi-hole – `192.168.20.2` |
| 30          | **Security**       | 192.168.30.0/24   | 🛡️ Kali Linux – `192.168.30.100`  <br> 📡 Security Onion – `192.168.30.101`|


Include a visual map or VLAN table here if you want.


## 🔧 Key Features

- VLAN segmentation and inter-VLAN routing via pfSense
- DNS filtering and ad blocking using Pi-hole
- Active Directory setup with GPO and DNS roles
- Simulated attacker and victim VMs for security testing
- IDS monitoring with Security Onion
- Network troubleshooting across Windows and Linux hosts

---

## 📝 Documentation

Each VM and service is documented in its own subdirectory:
- [`Proxmox`](./Proxmox/README.md)
- [`pfSense`](./pfSense/README.md)
- [`Pi-hole`](./Pi-hole/README.md)
- [`Windows 10 Client`](./Win10_Client/README.md)
- [`Windows Server 2019`](./WinServer2019/README.md)
- [`Debian Admin`](./Debian_Admin/README.md)
- [`Kali Linux`](./Kali_Linux/README.md)
- [`Meta`](./Meta/README.md)
- [`Security Onion`](./SecurityOnion/README.md)
- [`Troubleshooting`](./Troubleshoot/README.md)

---

## 📷 Optional Enhancements

- Add **screenshots** of:
  - pfSense VLAN and rule config
  - Pi-hole admin panel with blocked queries
  - Security Onion alerts dashboard
  - Kali attacks and packet captures
- Create a **network diagram** with draw.io or Lucidchart and include it

---

## 🔐 VLAN Segmentation & Firewall Rules

- pfSense is configured as a VLAN trunk to manage traffic across VLAN 10 (Client), VLAN 20 (Server), and VLAN 30 (Security)
- Inter-VLAN communication is controlled via **stateful firewall rules**, ensuring least privilege
- Example Rule: Only allow RDP from VLAN 10 to Windows Server on VLAN 20; deny all other traffic by default
- VLANs are assigned based on VM role, with unique IP ranges and DHCP scopes

## 🌐 DNS Filtering with Pi-hole
- Pi-hole deployed in the Server VLAN (192.168.20.2) as the default DNS resolver
- DNS traffic from all VLANs is redirected to Pi-hole using pfSense NAT port redirection
- Logs and dashboards show DNS query sources and blocked domains
- Custom blocklists and whitelists configured for fine-grained DNS control

---

## 🎯 Skills Demonstrated

- Virtualization (Proxmox)
- Networking (VLANs, pfSense, DHCP, DNS)
- System Administration (Windows/Linux)
- Network Security Monitoring (IDS)
- Penetration Testing Basics (Kali, Metasploitable)
- Documentation & Troubleshooting
