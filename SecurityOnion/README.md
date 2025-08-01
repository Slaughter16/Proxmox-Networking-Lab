# 🧅 Security Onion (VLAN 30)

## 🔧 Network Configuration

- **VLAN**: 30  
- **Interface**: `ens18`  
- **IP Address**: 192.168.30.101 (DHCP)  
- **Gateway**: 192.168.30.1  
- **DNS**: 192.168.20.2 (Pi-hole)

---

## 🔍 Network Verification Commands

| Test                        | Command                                 | Expected Output                         |
|-----------------------------|------------------------------------------|-----------------------------------------|
| Show IP address             | `ip a`                                   | IP: `192.168.20.101`                    |
| Show route                  | `ip r`                                   | Default via `192.168.20.1`              |
| Ping Gateway                | `ping -c 4 192.168.30.1`                 | Replies received                        |
| Ping DNS Server             | `ping -c 4 192.168.20.2`                 | Replies received                        |
| Ping Meta                   | `ping -c 4 192.168.20.101`               | Successful response from Meta           |
| DNS Resolution              | `dig google.com` or `nslookup google.com`| Successful DNS result                   |

---

## 📸 Suggested Screenshot Checklist

- `ip a` and `ip r` output

![SecO](./screenshots/1_SecOIPa.png)
![SecO](./screenshots/2_SecIPr.png)

- `ping` to gateway, DNS, and Meta

![SecO](./screenshots/3_PingSec.png)

- DNS test using `dig` or `nslookup`  

![SecO](./screenshots/4_SecO_DNS.png)
![SecO](./screenshots/5_SecO_DNS.png)

---

## Security Onion: Integrated Tools

Security Onion offers several powerful tools pre-configured for log collection, analysis, and forensic triage. Below are screenshots from various modules included in the Elastic stack and supporting toolset.

### Kibana
Kibana is the main UI for visualizing and querying logs.
![Kibana Dashboard](./screenshots/kibana.png)

### Elastic Fleet & Agents
Fleet tracks connected agents and their health.
![Fleet Agents](./screenshots/fleet_agents.png)
![Fleet Policies](./screenshots/fleet_policies.png)

### Osquery Manager
Used for live queries and endpoint inspection.
*Note: No queries have been executed in this lab instance.*
![Osquery](./screenshots/osquery.png)

### Wazuh
Wazuh integration for host intrusion detection. Currently shows zero logs — confirming no endpoint agent is reporting.
![Wazuh](./screenshots/wazuh.png)

### CyberChef
The "Cyber Swiss Army Knife" for data decoding and manipulation.
![CyberChef](./screenshots/cyberchef.png)

### ATT&CK Navigator
Visual map of adversary techniques using MITRE ATT&CK framework.
![MITRE ATT&CK Navigator](./screenshots/navigator.png)

### InfluxDB
Database for time-series data, used for telemetry and metrics.
![InfluxDB](./screenshots/influxdb.png)
