# 🤖 Meta VM (VLAN 20)

## 🔧 Network Configuration

- **VLAN**: 20  
- **Interface**: `ens18`  
- **IP Address**: 192.168.20.101 (via static config or DHCP)  
- **Gateway**: 192.168.20.1  
- **DNS**: 192.168.20.2 (Pi-hole)

---

## 🔍 Network Verification Commands

| Test                        | Command                                 | Expected Output                          |
|-----------------------------|------------------------------------------|------------------------------------------|
| Check IP address            | `ip a`                                   | Shows IP: `192.168.20.101`               |
| Check default route         | `ip r`                                   | Shows route via `192.168.20.1`           |
| Check DNS resolution        | `dig google.com` or `nslookup google.com`| Successful DNS reply from Pi-hole        |
| Ping Gateway                | `ping -c 4 192.168.20.1`                 | Replies received                         |
| Ping DNS                   | `ping -c 4 192.168.20.2`                 | Replies received                         |
| Ping Kali                  | `ping -c 4 192.168.30.100`               | Replies received from Kali               |

---

## 📸 Suggested Screenshot Checklist

- `ip a` and `ip r` output  
- `ping` to gateway, DNS, and Kali  
- `dig` or `nslookup` showing DNS resolution  
