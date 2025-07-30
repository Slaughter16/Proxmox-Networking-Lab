# 💻 Windows 10 Client (VLAN 30)

## 🔧 Network Configuration

- **VLAN**: 30  
- **IP Address**: 192.168.30.100 (via DHCP)  
- **DHCP Enabled**: Yes  
- **Default Gateway**: 192.168.30.1  
- **DNS Server**: 192.168.20.2 (Pi-hole)

---

## ✅ Steps to Enable DHCP

1. Open **Control Panel**

![DHCP](./screenshots/1_Control.png)

2. Navigate to **Network and Internet** → **Network Status and Tasks**

![DHCP](./screenshots/2_Network.png)

3. Click on **Change adapter settings**

![DHCP](./screenshots/3_Adapt.png)

4. Right-click the **Ethernet adapter** and select **Properties**
![DHCP](./screenshots/4_Prop.png)

5. Select **Internet Protocol Version 4 (TCP/IPv4)** → Click **Properties**
![DHCP](./screenshots/5_IP.png)
   
6. Choose:
   - `Obtain an IP address automatically`
   - `Obtain DNS server address automatically`
   - Click **OK** and close all dialog boxes.
![DHCP](./screenshots/6_DHCPc.png)

---

## 🔓 Enable ICMP Echo Requests (For Pinging)

To allow this client to **be pinged by others**:

1. Open **Windows Defender Firewall with Advanced Security**
![ICMP](./screenshots/7_Firewalll.png)
![ICMP](./screenshots/8_Firewalll.png)

3. Go to **Inbound Rules**
![ICMP](./screenshots/9_Ruless.png)

5. Enable the following rule:
   - `File and Printer Sharing (Echo Request - ICMPv4-In)`
![ICMP](./screenshots/10_Rules1.png)
![ICMP](./screenshots/11_Rules2.png)
![ICMP](./screenshots/12_Rules3.png)

6. Apply the rule to:
   - `Domain`, `Private`, and `Public` profiles  
   - Under the **Advanced** tab
![ICMP](./screenshots/13_Profilee.png)
![ICMP](./screenshots/14_Profilee.png)
---

## 🔍 Network Verification

| Test                        | Command                          | Expected Output                        |
|-----------------------------|----------------------------------|----------------------------------------|
| IP Configuration            | `ipconfig /all`                       | Shows IP: `192.168.30.100`             |
| Ping Gateway                | `ping 192.168.30.1`              | Successful replies                     |
| Ping DNS (Pi-hole)         | `ping 192.168.20.2`              | Successful replies                     |
| Ping Windows Server         | `ping 192.168.20.102`            | Successful replies if firewall allows  |
| DNS Resolution Test        | `nslookup google.com`            | Should resolve via Pi-hole             |
| Routing Table              | `route print`                    | Shows routes for VLAN 30 subnet        |

---

## 📸 Suggested Screenshot Checklist

- `ipconfig /all , ping tests to gateway (192.168.30.1) , ping to Gateway (192.168.30.1)' output
![WinServer](./screenshots/15_DNS.png)

- 'Ping to DNS (192.168.20.2) , ping to another VM (Kali: 192.168.20.102) and Successful `nslookup`'   
 ![WinServer](./screenshots/16_Success.png)

- 'route print' output verify sends traffic to other networks 0.0.0.0 (eg: Internet) and specific router for local VLAN 192.168.30.0 On-link: means it knows to use ARP on that subnet.
 ![WinServer](./screenshots/17_Route.png)
