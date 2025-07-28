# 🧅 Security Onion (VLAN 30)

## 🔧 Network Configuration

- **VLAN**: 30  
- **Interface**: `ens18`  
- **IP Address**: 192.168.30.? (static or DHCP)  
- **Gateway**: 192.168.30.1  
- **DNS**: 192.168.20.2 (Pi-hole)

---

## 🔍 Network Verification Commands

| Test                        | Command                                 | Expected Output                         |
|-----------------------------|------------------------------------------|-----------------------------------------|
| Show IP address             | `ip a`                                   | IP: `192.168.20.103`                    |
| Show route                  | `ip r`                                   | Default via `192.168.20.1`              |
| Ping Gateway                | `ping -c 4 192.168.30.1`                 | Replies received                        |
| Ping DNS Server             | `ping -c 4 192.168.20.2`                 | Replies received                        |
| Ping Meta                   | `ping -c 4 192.168.20.101`               | Successful response from Meta           |
| DNS Resolution              | `dig google.com` or `nslookup google.com`| Successful DNS result                   |

---

## 📸 Suggested Screenshot Checklist

- `ip a` and `ip r` output  
- `ping` to gateway, DNS, and Meta  
- DNS test using `dig` or `nslookup`  
