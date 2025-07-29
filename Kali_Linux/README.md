# 🐱 Kali Linux (VLAN 30)

## 🔧 Network Configuration

- **VLAN**: 30  
- **Interface**: `eth0`  
- **IP Address**: 192.168.30.100 (via DHCP)  
- **Gateway**: 192.168.30.1  
- **DNS**: 192.168.20.2 (Pi-hole)

---

## 🔍 Network Verification Commands

| Test                        | Command                                 | Expected Output                         |
|-----------------------------|------------------------------------------|-----------------------------------------|
| Check IP address            | `ip a` or `ip addr show`                | Shows IP: `192.168.30.100`              |
| Check default route         | `ip route` or `ip r`                    | Shows default via `192.168.30.1`        |
| Check DNS resolution        | `nslookup google.com` or `dig google.com`| Successful resolution via Pi-hole       |
| Ping Gateway                | `ping -c 4 192.168.30.1`                | Replies received                        |
| Ping DNS (Pi-hole)         | `ping -c 4 192.168.20.2`                | Replies received                        |
| Ping Meta VM               | `ping -c 4 192.168.20.101`              | Replies from Meta                       |

---

## 📸 Suggested Screenshot Checklist

- `ip a` and `ip route` output

- `ping` to gateway, DNS, and Meta

- `nslookup` showing DNS resolution  
