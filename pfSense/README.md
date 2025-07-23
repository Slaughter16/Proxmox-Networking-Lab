# 🧩 Step 3: Configure VLANs in pfSense

This document outlines how to configure VLANs in pfSense to segment your Proxmox virtual lab network into isolated zones.

## 🎯 Objective
Segment the virtual lab network into three VLANs and route traffic securely using pfSense.

### VLAN Structure:
| VLAN ID | Name     | Subnet             |
|---------|----------|--------------------|
| 10      | Clients  | 192.168.10.0/24    |
| 20      | Servers  | 192.168.20.0/24    |
| 30      | Security | 192.168.30.0/24    |

## 🔐 Log into pfSense
Access the pfSense web interface from your **Debian Admin VM** (tagged to VLAN 10):

- **URL:** `https://[pfSense LAN IP]`
- **Default Credentials:**
  - **Username:** `admin`
  - **Password:** `pfsense`
  -(As you can see there are more characters in the password box as i made up my own)
![Login to pfSense](1_login_pfsense.png)

## pfSense Dashboard

Once logged in, you will see the dashboard.

![pfSense Dashboard](2_dashboard.png)

---

## 🔧 Create VLAN Interfaces

1. Navigate to: `Interfaces > Assignments > VLANs`
2. Click **➕ Add** for each VLAN.

---

![Before_VLAN_Interfaces Added](3_Before_VLAN.png)

### ➕ VLAN 10 – Clients

- **Parent Interface:** vmbr1 NIC (e.g., `vtnet1`)
- **VLAN Tag:** `10`
- **Description:** `VLAN10_Client`
  
✅ Click **Save**, then **Apply Changes**.

![VLAN 10](4_vlan10_add.png)

---

### ➕ VLAN 20 – Servers- 

- **VLAN Tag:** `20`
- **Description:** `VLAN20_Servers`

![VLAN 20](5_vlan20_add.png)

---

### ➕ VLAN 30 – Security
- **VLAN Tag:** `30`
- **Description:** `VLAN30_Security`

![VLAN 30](6_vlan30_add.png)

---

## 📋 Review All VLANs

After all are added, the VLAN list should appear like this:

![All VLANs](7_all_VLANS_listed.png)

---

## 🧬 Assign VLAN Interfaces

1. Go to `Interfaces > Assignments`
2. Click **+ Add** to assign each new VLAN interface.
   
![Interface>Assignments](8_Int_Assign.png)
![Add Interface](9_Add_Int.png)

---

### ⚙️ Configure LAN10 Interface (VLAN 10)
1. Click the new interface name (e.g., OPT1 → rename to **LAN10**).
2. Enable the interface.
3. Set **IPv4 Configuration Type** to `Static IPv4`.
4. Enter:
   - **IP Address:** `192.168.10.1`
   - **Subnet Mask:** `/24`
💾 Save and **Apply Changes**.
![Config VLAN10 Int](10_VLAN10_Int.png)
![Config VLAN10 Int](11_VLAN10_Int.png)
