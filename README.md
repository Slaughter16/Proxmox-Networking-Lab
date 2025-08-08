# 🧪 Proxmox Networking & Security Lab
**Enterprise Simulation: VLAN Segmentation | DNS Configuration | Firewall Rules | OpenVPN | Windows & Linux Systems**

![Proxmox Logo](./images/proxmox-logo.png)  

A virtual home lab designed to simulate an enterprise network environment using:

> **Proxmox VE**, **pfSense**, **Windows Server 2019**, **Windows 10**, **Security Onion**, **Kali Linux**, **Debian Admin**, **Pi-hole**, and **Metasploitable2**

---
## 📚 Table of Contents

- [🖥️ Proxmox Dashboard](#proxmox-dashboard)
- [🌐 Network Topology Diagram](#-network-topology-diagram)
- [🧱 Lab Topology Overview](#-lab-topology-overview)
- [🖥️ Virtual Machines](#-virtual-machines)
- [🌐 VLAN Configuration](#-vlan-configuration)
- [🔧 Key Features](#-key-features)
- [📝 Documentation](#-documentation)
- [🔐 VLAN Segmentation & Firewall Rules](#-vlan-segmentation--firewall-rules)
- [🌐 DNS Filtering with Pi-hole](#-dns-filtering-with-pi-hole)
- [🔐 VPN Access (OpenVPN)](#-vpn-access-openvpn)
- [🎯 Skills Demonstrated](#-skills-demonstrated)
- [🧩 Custom Security Enhancements](#-custom-security-enhancements)
- [📇 Contact](#-contact)



---

### 🔍 Lab Highlights

- 🔐 VLAN segmentation and inter-VLAN firewall rules
- 🌐 DNS redirection and filtering with Pi-hole
- 🧰 IDS-ready architecture using Security Onion
- ⚙️ Multi-VM configuration for security monitoring and testing environments

---

## 🖥️ Proxmox Dashboard

*Primary hypervisor interface hosting all virtual machines.*

![Proxmox Dashboard](./images/Proxmox-Dashboard.png)

---

## 🌐 Network Topology Diagram

*Visual overview of VLANs, pfSense trunking, and host placement.*

![Network Topology Diagram](./images/Network-Topology.png)

> 🔧 Created with [draw.io]

---

## 🧱 Lab Topology Overview

- **Proxmox VE Host** with VLAN-aware bridges:
  - `vmbr0` – WAN
  - `vmbr1` – LAN
- **pfSense** – VLAN router/firewall and DHCP
- **Pi-hole** – DNS filtering and ad blocking
- **VLANs:**
  - **VLAN 10 (Client)** – Workstations & Admin
  - **VLAN 20 (Server)** – Core services & infrastructure
  - **VLAN 30 (Security)** – Security tools & monitoring  

---

## 🖥️ Virtual Machines

| VM Name             | Role                            | OS / Description                     |
|---------------------|----------------------------------|--------------------------------------|
| Proxmox             | Lab Hypervisor                   | Proxmox VE                           |
| pfSense             | VLAN Routing & Firewall          | pfSense CE                           |
| Windows 10 Client   | End-user Testing Environment     | Windows 10 Pro                       |
| Windows Server 2019 | Active Directory / File Sharing  | Windows Server 2019                  |
| Debian Admin        | Network Admin Workstation        | Debian Linux                         |
| Kali Linux          | Penetration Testing Tools        | Kali Rolling                         |
| Meta (CentOS)       | Vulnerable VM for Exploitation   | Metasploitable 2                     |
| Pi-hole             | DNS Sinkhole & Ad Blocker        | Pi-hole in Ubuntu Container          |
| Security Onion      | Intrusion Detection / Monitoring | Security Onion (SO2)                 |

---

## 🌐 VLAN Configuration

| **VLAN ID** | **Name / Purpose** | **Subnet**        | **Assigned VMs and IP Addresses**                                       |
|------------:|--------------------|-------------------|-------------------------------------------------------------------------|
| 10          | **Client**         | 192.168.10.0/24   | 🖥️ Windows 10 Client – `192.168.10.100`  <br> 🧑‍💼 Debian Admin Station – `192.168.10.101`|
| 20          | **Server**         | 192.168.20.0/24   | 🗂️ Windows Server 2019 – `192.168.20.102`  <br> 💻 Meta VM – `192.168.20.101` <br> 🍍 Pi-hole – `192.168.20.2` |
| 30          | **Security**       | 192.168.30.0/24   | 🛡️ Kali Linux – `192.168.30.100`  <br> 📡 Security Onion – `192.168.30.101`|

---

## 🔧 Key Features

- VLAN segmentation and inter-VLAN routing via pfSense
- Role-based firewall rules using pfSense
- Central DNS filtering using Pi-hole with NAT redirection
- Configured to support simulated attacker and victim VMs for security testing
- IDS monitoring with Security Onion
- Full Linux & Windows interoperability for testing

---

## 📝 Documentation

Each VM and configuration is documented in its own folder:

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
- [`OpenVPN`](./OpenVPN/README.md)

> 📸 **Each folder contains:** Screenshots, configs, logs, firewall rules, DNS settings, and test results.

---

## 🔐 VLAN Segmentation & Firewall Rules

- pfSense is configured as a VLAN trunk to manage traffic across VLAN 10 (Client), VLAN 20 (Server), and VLAN 30 (Security)
- Inter-VLAN communication is controlled via **stateful firewall rules**, ensuring least privilege
- VLANs are assigned based on VM role, with unique IP ranges and DHCP scopes

---

## 🌐 DNS Filtering with Pi-hole

- Pi-hole is deployed in VLAN 20 (`192.168.20.2`) as the authoritative DNS server
- pfSense uses **NAT Port Forwarding** to redirect all VLAN DNS traffic to Pi-hole
- Dashboards provide visibility into queries and blocked domains
- DNSSEC disabled to avoid validation issues during testing
- Pi-hole configured with custom blocklists and upstream DNS (e.g., `1.1.1.1`, `8.8.8.8`)

---

## 🎯 Skills Demonstrated

- Virtualization and host networking using **Proxmox VE**
- Advanced VLAN design and trunking
- Firewall and NAT configuration in **pfSense**
- DNS security filtering via **Pi-hole**
- Security monitoring with **Security Onion**
- Windows and Linux network integration
- System documentation and troubleshooting methodology

---

## 🔐 VPN Access (OpenVPN)

- **OpenVPN server** configured in pfSense
- Remote VPN access restricted to **VLAN 10** (192.168.10.0/24)
- User certificate created and exported via pfSense Certificate Manager
- Successfully connected from an external VM (Windows Server) using **OpenVPN client**
- Verified access to internal resources:
  - ✅ Debian Admin Workstation – `192.168.10.101`

> 📸 **[See OpenVPN setup screenshots](./OpenVPN/README.md)**

---

## 🧩 Custom Security Enhancements

- Applied restrictive inter-VLAN firewall rules
- Configured DNS NAT redirection to Pi-hole for all VLANs
- Enabled remote VPN access using OpenVPN with user certs
- Segmented attacker (Kali) from server VLAN (Meta)

---

## 📇 Contact

🔗 [LinkedIn: John Slaughter](https://www.linkedin.com/in/john-slaughter-08a872262/)
