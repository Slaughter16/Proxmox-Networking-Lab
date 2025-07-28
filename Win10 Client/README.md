# Windows 10 Client Verification

This folder contains verification steps and screenshots confirming the Windows 10 Client's proper network configuration and connectivity within the lab environment.

## 1. Enable DHCP

To enable dynamic IP assignment via DHCP:

1. Open **Control Panel** → **Network and Internet** → **Network and Sharing Center**.
2. Click **Change adapter settings**.
3. Right-click the Ethernet adapter → **Properties**.
4. Select **Internet Protocol Version 4 (TCP/IPv4)** → click **Properties**.
5. Choose:
   - **Obtain an IP address automatically**
   - **Obtain DNS server address automatically**
6. Click **OK** and close all dialog boxes.

---

## 2. Enable ICMP Ping Response

By default, Windows 10 blocks incoming ICMP (ping) requests. To allow the system to be pinged:

1. Open **Windows Defender Firewall with Advanced Security**.
2. Go to **Inbound Rules**.
3. Enable **File and Printer Sharing (Echo Request - ICMPv4-In)**.
4. Right-click → **Properties**.
5. Under the **Advanced** tab, make sure the rule applies to **Domain**, **Private**, and **Public** profiles.
6. Click **Apply** and **OK**.

---

## 3. Network Details

| Detail              | Value               |
|---------------------|---------------------|
| VLAN                | VLAN 10             |
| Assigned IP Address | 192.168.10.100      |
| Gateway             | 192.168.10.1        |
| DNS Server          | 192.168.20.2        |

---

## 4. Command Verifications

### `ipconfig`
