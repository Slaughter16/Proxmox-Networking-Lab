# 🧩 Pi-hole DNS Server Configuration (VLAN 20)

This guide documents how to fix and configure the Pi-hole container/VM to serve as the DNS server for **VLAN 20** and other VLANs in the Proxmox lab.

## 📌 Problem

Pi-hole VM was originally assigned the wrong IP address: `192.168.1.2` (outside target VLAN).  
We wanted Pi-hole to use `192.168.20.2` to serve as the DNS server for All the VLANs but targeted for VLAN 20 — the same subnet as the Windows client and Debian admin VM.

## 🔍 Initial Troubleshooting

- Ran `ip a` on the Pi-hole console.
- Verified the interface in use was `eth0`.
- Saw the current IP was incorrect (`192.168.1.2`).
  
![Pihole IP address before change](1_IP.png)

---


## 🧪 Temporary IP Fix (Manual Command-Line Change)

Manually changed IP address (not via /etc/network or Netplan, but directly):

- **sudo dhcpcd eth0**
- **sudo ip addr add 192.168.20.2/24 dev eth0**
- **sudo ip route add default via 192.168.20.1**
  
![Config_Temp_IP](2_Config_IP.png)

---

### 💾 Make IP Assignment Permanent

To make the Pi-hole IP assignment persistent after reboot, manually edit the network interface configuration file:

### 📝 Edit the interfaces file:

- **sudo nano /etc/network/interfaces**

![Edit_Int](3_Edit_Int.png)

### ✏️ Add the following configuration:

```ini
auto eth0
iface eth0 inet static
  address 192.168.20.2
  netmask 255.255.255.0
  gateway 192.168.20.1
```

![Config_Perm_IP](4_Perm_IP.png) 

- **Confirm change with 'ip a'**

![Confirm Change](5_Confirm.png)

### ✅ Confirm Connectivity to Pi-hole Dashboard  

Access the Pi-hole Dashboard from the Debian Admin Machine (VLAN10) using the Pi-hole IP: `192.168.20.2`

![Confirm_IP_Connectivity from Debian](6_Pihole_Dashboard.png)

---

### 🔄 Ensure Pi-hole Can Answer Redirected Traffic

To allow Pi-hole to properly resolve redirected DNS queries (those not originally intended for Pi-hole), follow these steps:

1. Open the Pi-hole Admin Dashboard.
2. Navigate to **Settings** → **DNS**.
3. Under **Interface listening behavior**, select:
   > **Listen on all interfaces, permit all origins**

This setting allows Pi-hole to accept DNS queries even if they are redirected from other DNS servers (e.g., `8.8.8.8`, `1.1.1.1`, etc.).
