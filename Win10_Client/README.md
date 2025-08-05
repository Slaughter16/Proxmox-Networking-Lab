# 💻 Windows 10 Client (VLAN 30)

## 🔧 Network Configuration

- **VLAN**: 30  
- **IP Address**: 192.168.30.100 (via DHCP)  
- **DHCP Enabled**: Yes  
- **Default Gateway**: 192.168.30.1  
- **DNS Server**: 192.168.20.2 (Pi-hole)

---

## ✅ Enabling DHCP on Windows 10

1. Open **Control Panel**

![DHCP](./screenshots/1_Control.png)

2. Navigate to **Network and Internet** → **Network Status and Tasks**

![DHCP](./screenshots/2_Network.png)

3. Click **Change adapter settings**  

![DHCP](./screenshots/3_Adapt.png)

4. Right-click the **Ethernet adapter** → Select **Properties**  
![DHCP](./screenshots/4_Prop.png)

5. Select **Internet Protocol Version 4 (TCP/IPv4)** → Click **Properties**
![DHCP](./screenshots/5_IP.png)
   
6. Set the following:
   - `Obtain an IP address automatically`
   - `Obtain DNS server address automatically`
   - Click **OK** and close all dialog boxes.
![DHCP](./screenshots/6_DHCPc.png)

---

## 🔓 Enable ICMP Echo Requests (Allow Ping)

1. Open **Windows Defender Firewall with Advanced Security**
![ICMP](./screenshots/7_Firewalll.png)
![ICMP](./screenshots/8_Firewalll.png)

2. Go to **Inbound Rules**
![ICMP](./screenshots/9_Ruless.png)

3. Enable the following rule:
   - **File and Printer Sharing (Echo Request - ICMPv4-In)**  
![ICMP](./screenshots/10_Rules1.png)
![ICMP](./screenshots/11_Rules2.png)
![ICMP](./screenshots/12_Rules3.png)

4. Apply the rule to all profiles:
  - **Domain**, **Private**, and **Public**  
   - Set under the **Advanced** tab
![ICMP](./screenshots/13_Profilee.png)
![ICMP](./screenshots/14_Profilee.png)

---

## 🔍 Network Verification Checklist

| Test                      | Command                 | Expected Output                          |
|---------------------------|-------------------------|------------------------------------------|
| IP Configuration          | `ipconfig /all`         | IP: `192.168.30.100` assigned via DHCP   |
| Ping Gateway              | `ping 192.168.30.1`     | Successful replies                       |
| Ping DNS (Pi-hole)        | `ping 192.168.20.2`     | Successful replies                       |
| Ping Windows Server       | `ping 192.168.20.102`   | Successful replies (if firewall allows)  |
| DNS Resolution            | `nslookup google.com`   | Resolves via Pi-hole DNS                 |
| View Routing Table        | `route print`           | Shows VLAN 30 routes and default gateway |

---

## 📸 Screenshot Checklist

- ✅ `ipconfig /all`, `ping 192.168.30.1` (Gateway)  
![WinServer](./screenshots/15_DNS.png)

- ✅ `ping 192.168.20.2` (Pi-hole), `ping 192.168.20.102` (Windows Server), `nslookup google.com`  
 ![WinServer](./screenshots/16_Success.png)

- ✅ `route print` showing default route and VLAN-specific routing (`On-link` for 192.168.30.0/24)  
 ![WinServer](./screenshots/17_Route.png)
