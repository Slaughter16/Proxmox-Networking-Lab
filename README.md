# Proxmox Networking Lab

This project documents the setup of a virtualized home lab using **Proxmox**, **pfSense**, **Windows 2019 Server**, **Windows 10 Client**, **Security Onion**, **Debian Admin Machine**, **Kali Linux**, **Pi-hole**, and **Metasploitable2**. It covers VLAN segmentation, DNS troubleshooting, DHCP configuration, and Firewall configurations.

---

## 🧱 Lab Topology

- Proxmox VE Host with `vmbr0` and `vmbr1` linux bridges 
- pfSense as firewall/router
- Pi-hole as DNS server
- VLAN10 - Clients (Win 10, Debian Admin Machine)
- VLAN20 - Server (Windows 2019 Server, Pi-hole, Metasploit)
- VLAN30 - Security (Kali, Security Onion)

---

## ✅ Setup Phases

### 1. pfSense Initial Setup
- Created VLAN interfaces
- Assigned VLANs: 10, 20, 30
- Configured interfaces with static IPs
- [View Screenshots](images/pfSenseSetup/README.md)

### 2. DHCP & Firewall Rules
- Enabled DHCP for each VLAN
- Applied "allow all" firewall rules for testing
- Verified IP assignments

### 3. Windows Connectivity Fixes
- Enabled ICMP Echo Request (ping) on Win Client and Server
- Fixed Windows Firewall advanced settings
- [See VLAN10 Screenshots](images/VLAN10/README.md)

### 4. DNS Configuration
- Configured DNS Forwarder in pfSense
- Fixed DNS resolution via Pi-hole
- Verified via ping and nslookup
- [See DNS Fixes](images/DNSFixes/README.md)

### 5. Ping Tests and Troubleshooting
- Used pfSense Diagnostics → Ping
- Kali and Meta tested connectivity to all VLANs
- Resolved ICMP issues with firewall profiles

---

## 🧠 Notes

- All tests were done with **ICMP**, **DHCP**, and **DNS**
- Screenshots have detailed file and rule views
