# 🧅 Security Onion (VLAN 30)

## 🔧 Network Configuration

- **VLAN**: 30  
- **Interface**: `ens18`  
- **IP Address**: 192.168.30.101 (DHCP)  
- **Gateway**: 192.168.30.1  
- **DNS**: 192.168.20.2 (Pi-hole)

---

## 🔍 Network Verification Commands

| Test                        | Command                                   | Expected Output                          |
|----------------------------|--------------------------------------------|------------------------------------------|
| Show IP address            | `ip a`                                     | IP: `192.168.30.101`                     |
| Show routing table         | `ip r`                                     | Default via `192.168.30.1`               |
| Ping Gateway               | `ping -c 4 192.168.30.1`                   | Replies received                         |
| Ping DNS Server (Pi-hole) | `ping -c 4 192.168.20.2`                   | Replies received                         |
| Ping Meta (Web Test)       | `ping -c 4 192.168.20.101`                 | Successful response                      |
| DNS Resolution Test        | `dig google.com` or `nslookup google.com` | Successful DNS resolution                |

---

## 📸 Screenshot Checklist

### 🔌 IP and Routing Info

- `ip a` and `ip r` output

![SecO](./screenshots/1_SecOIPa.png)
![SecO](./screenshots/2_SecIPr.png)

### 🌐 Connectivity Tests

- `ping` to gateway, DNS, and Meta

![SecO](./screenshots/3_PingSec.png)

### 🌍 DNS Lookup Test

- DNS test using `dig` or `nslookup`  

![SecO](./screenshots/4_SecO_DNS.png)
![SecO](./screenshots/5_SecO_DNS.png)

---

## 🧅 Security Onion Tools Overview

Security Onion provides powerful tools for monitoring, detection, and analysis in a centralized dashboard via the Elastic Stack.

### 📊 Kibana
Kibana is the main UI for visualizing and querying logs.
![Kibana Dashboard](./screenshots/kibana.png)

### 🧭 Elastic Fleet & Agents
Monitors connected agents and their configurations.
![Fleet Agents](./screenshots/fleet_agents.png)
![Fleet Policies](./screenshots/fleet_policies.png)

### 🕵️ Osquery Manager
Enables live endpoint queries.  
*Note: No queries executed in this lab.* 
![Osquery](./screenshots/osquery.png)

### 🛡️ Wazuh
Host-based intrusion detection integration.  
*Currently showing zero logs – indicates no endpoint agent reporting.*  
![Wazuh](./screenshots/wazuh.png)

### 🔧 CyberChef
Data conversion and decoding utility, great for DFIR tasks.
![CyberChef](./screenshots/cyberchef.png)

### 🧠 MITRE ATT&CK Navigator
Framework visualizing adversary techniques and tactics.  
![MITRE ATT&CK Navigator](./screenshots/navigator.png)

### 📈 InfluxDB
Used for storing and querying time-series telemetry data.  
![InfluxDB](./screenshots/influxdb.png)

---

✅ **Lab Summary:**  
Security Onion in VLAN 30 is properly networked via DHCP, resolves DNS through Pi-hole, and reaches internal and external systems. All core analysis tools are accessible and responsive within the Elastic stack.
