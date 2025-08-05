# 🖥️ Windows Server (VLAN 20)

## 🔧 Network Configuration

- **VLAN**: 20  
- **IP Address**: 192.168.20.102 (via DHCP)  
- **DHCP Enabled**: Yes  
- **Default Gateway**: 192.168.20.1  
- **DNS Server**: 192.168.20.2 (Pi-hole)  

---

## ✅ Steps to Enable DHCP

1. Open **Control Panel**

![DHCP](./screenshots/1_ControlPanel.png)

2. Navigate to **Network and Internet** → **Network Status and Tasks**

![DHCP](./screenshots/2_Network_Internet.png)

3. Click on **Change adapter settings**

![DHCP](./screenshots/3_Adapter.png)

4. Right-click the **Ethernet adapter** and select **Properties**

![DHCP](./screenshots/4_Properties.png)

5. Select **Internet Protocol Version 4 (TCP/IPv4)** → Click **Properties**

![DHCP](./screenshots/5_IPv4.png)
6. Choose:
   - `Obtain an IP address automatically`
   - `Obtain DNS server address automatically`
   - Click **OK** and close all dialog boxes.

![DHCP](./screenshots/6_DHCP.png)

---

## 🔓 Enable ICMP Echo Requests (For Pinging)

To ensure the server can be pinged by other machines:

1. Open **Windows Defender Firewall then into Advanced Settings**

![ICMP](./screenshots/7_Firewall.png)
![ICMP](./screenshots/8_Firewall.png)
3. Go to **Inbound Rules**  
![ICMP](./screenshots/9_Rules.png)
4. Enable the following rule:
   - `File and Printer Sharing (Echo Request - ICMPv4-In)`
![ICMP](./screenshots/10_Rules.png)
![ICMP](./screenshots/11_Rules.png)
![ICMP](./screenshots/12_Rules.png)
5. Apply the rule to:
   - `Domain`, `Private`, and `Public` profiles
   - Under the **Advanced** tab
![ICMP](./screenshots/13_Profile.png)
![ICMP](./screenshots/14_Profile.png)
---

## 🔍 Network Verification

| Test                        | Command                          | Expected Output                        |
|-----------------------------|----------------------------------|----------------------------------------|
| IP Configuration            | `ipconfig`                       | Shows IP: `192.168.20.102`             |
| Ping Gateway                | `ping 192.168.20.1`              | Successful replies                     |
| Ping DNS (Pi-hole)         | `ping 192.168.20.2`              | Successful replies                     |
| Ping Another VM (Kali)      | `ping 192.168.30.100`            | Successful replies if firewall allows  |
| DNS Resolution Test        | `nslookup google.com`            | Should resolve via Pi-hole             |
| Routing Table              | `route print`                    | Shows routes for VLAN 20 subnet        |

---

## 📸 Suggested Screenshot Checklist

- `ipconfig /all , ping tests to gateway (192.168.20.1) , ping to DNS (192.168.20.2)' output
![WinServer](./screenshots/15_Ping.png)

- 'Ping to DNS (192.168.20.2) , ping to another VM (Kali: 192.168.30.100) and Successful `nslookup`'   
 ![WinServer](./screenshots/16_Ping.png)

- 'route print' output verify sends traffic to other networks 0.0.0.0 (eg: Internet) and specific router for local VLAN 192.168.20.0 On-link: means it knows to use ARP on that subnet.
 ![WinServer](./screenshots/17_Ping.png)

 

