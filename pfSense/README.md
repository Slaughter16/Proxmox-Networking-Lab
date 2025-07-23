# 🧩 Step 3: Configure VLANs in pfSense

This folder documents the configuration of VLANs within pfSense as part of the lab network.

## 🎯 Objective
Segment the virtual lab network into three VLANs and route traffic securely using pfSense.

### VLAN Structure:
| VLAN ID | Name     | Subnet             |
|---------|----------|--------------------|
| 10      | Clients  | 192.168.10.0/24    |
| 20      | Servers  | 192.168.20.0/24    |
| 30      | Security | 192.168.30.0/24    |

## 🔐 Log into pfSense Web GUI from Debian Admin Machine

- URL: 'https://[pfSense LAN IP]'
- Default login (if unchanged):
  - **User:** 'admin'
  - **Pass:** 'pfsense'
  
![Login to pfSense](1_login_pfsense.png)

## pfSense Dashboard
![pfSense Dashboard](2_dashboard.png)

## 🔧 Create VLAN Interfaces
Go to `Interfaces > Assignments > VLANs`  
Then click **+Add** for each VLAN.

![Before_VLAN_Interfaces Added](3_Before_VLAN.png)

### VLAN 10 – Clients
- **Parent Interface:** vmbr1 NIC (e.g., `vtnet1`)
- **VLAN Tag:** `10`
- **Description:** `VLAN10_Client`
- **Always remember click "Save" and "Apply" changes"**

![VLAN 10](4_vlan10_add.png)

---

### VLAN 20 – Servers
- **VLAN Tag:** `20`
- **Description:** `VLAN20_Servers`

![VLAN 20](5_vlan20_add.png)

---

### VLAN 30 – Security
- **VLAN Tag:** `30`
- **Description:** `VLAN30_Security`

![VLAN 30](6_vlan30_add.png)

---

### 🔗 Review All VLANs

After creating all VLANs, your list should look like this:

![All VLANs](7_all_VLANS_listed.png)

---
## 🧬 Assign VLAN Interfaces
Now go to: `Interfaces > Assignments`  
Assign each VLAN to a new interface (e.g., LAN10, LAN20, LAN30).

![Interface>Assignments](8_Int_Assign)

Click **+ Add** to assing each new VLAN interface 

![Add Interface](9_Add_Int)
