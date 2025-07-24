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
- **Description:** `VLAN30_Security` (mistyped but added 30 after)

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
![Config VLAN10 Int](11_VLAN10_Inte.png)

---

## 🔁 Repeat for VLAN20 and VLAN30

Follow the same steps above for:

- **LAN20 (VLAN 20)**
  - IP: `192.168.20.1/24`
    
![Config VLAN20 Int](12_VLAN20_Int.png)
![Config VLAN20 Int](13_VLAN20_Int.png)

- **LAN30 (VLAN 30)**
  - IP: `192.168.30.1/24`

![Config VLAN30 Int](14_VLAN30_Int.png)
![Config VLAN30 Int](15_VLAN30_Int.png)

---

# 🛠️ Step 4: Enable DHCP on Each VLAN

## 🔹 Navigate to `Services > DHCP Server`

![Services_DHCP Server](16_DHCP_Page.png)

---

### 📦 Enable DHCP for LAN10

- Select `LAN10` tab
- Check **Enable DHCP server on LAN10 interface**
- Set Range:  
  - **From:** `192.168.10.100`  
  - **To:** `192.168.10.200`
- Click **Save**

![DHCP LAN10](17_dhcp_lan10.png)

---

### 📦 Enable DHCP for LAN20

- Select `LAN20` tab
- Check **Enable DHCP server on LAN20 interface**
- Set Range:  
  - **From:** `192.168.20.100`  
  - **To:** `192.168.20.200`
- Click **Save**

![DHCP LAN20](18_dhcp_lan20.png)

---

### 📦 Enable DHCP for LAN30

- Select `LAN30` tab
- Check **Enable DHCP server on LAN30 interface**
- Set Range:  
  - **From:** `192.168.30.100`  
  - **To:** `192.168.30.150`
- Click **Save**

![DHCP LAN30](19_dhcp_lan30.png)

---

# 🔒 Step 5: Add Allow-All Firewall Rules (Testing Phase)

During the initial testing phase, we’ll allow all traffic between VLANs by adding permissive rules to each VLAN interface. 
Once everything is confirmed working, these rules should be tightened for proper segmentation and security.

---

## 🔧 Navigate to Firewall Rules

1. Go to `Firewall > Rules` from the pfSense menu bar  
2. You will see separate tabs for:
   - `LAN10`
   - `LAN20`
   - `LAN30`
![Firewall_Rules](20_Firewall_Rules.png)

---

## ➕ Add Rule for VLAN10

1. Click the **LAN10** tab  
2. Click **➕ Add** at the top of the rules list
![Firewall_Tabs](21_Firewall_Tabs.png)

3. Configure the rule as follows:

| 🔧 Field           | 📝 Value            |
|-------------------|---------------------|
| **Action**         | Pass                |
| **Interface**      | LAN10               |
| **Address Family** | IPv4                |
| **Protocol**       | Any                 |
| **Source**         | LAN10 net           |
| **Destination**    | any                 |
| **Description**    | Allow All VLAN10    |

📸 Screenshot:  
![Allow All VLAN10](22_Allow_Pro.png)
![Allow All VLAN10](23_Allow_VLAN10.png)
![Allow All VLAN10](24_Allow_Final10.png)

✅ Click **Save** then **Apply Changes**

---

## ➕ Add Rule for VLAN20

1. Go to the **LAN20** tab  
2. Click **➕ Add** at the top
   
![Allow All VLAN20](25_LAN20.png)

3. Set the following values:

| 🔧 Field           | 📝 Value            |
|-------------------|---------------------|
| **Action**         | Pass                |
| **Interface**      | LAN20               |
| **Address Family** | IPv4                |
| **Protocol**       | Any                 |
| **Source**         | LAN20 net           |
| **Destination**    | any                 |
| **Description**    | Allow All VLAN20    |

📸 Screenshot:  
![Allow All VLAN20](26_Allow_Pro.png)
![Allow All VLAN20](27_Allow_VLAN20.png)
![Allow All VLAN20](28_Allow_VLAN20.png)

✅ Save and **Apply Changes**

---

## ➕ Add Rule for VLAN30

1. Navigate to the **LAN30** tab  
2. Click **➕ Add** at the top
   
![Allow All VLAN20](29_LAN30.png)

3. Use the following values:

| 🔧 Field           | 📝 Value            |
|-------------------|---------------------|
| **Action**         | Pass                |
| **Interface**      | LAN30               |
| **Address Family** | IPv4                |
| **Protocol**       | Any                 |
| **Source**         | LAN30 net           |
| **Destination**    | any                 |
| **Description**    | Allow All VLAN30    |

📸 Screenshot:  
![Allow All VLAN30](30_Allow_Pro.png)
![Allow All VLAN30](31_Allow_VLAN30.png)
![Allow All VLAN30](32_Allow_VLAN30_Final.png)

✅ Save and **Apply Changes**

---

> ⚠️ **Note:** These rules are for **testing purposes only**. After confirming VLAN connectivity, apply more **restrictive policies** to isolate traffic between Clients, Servers, and Security VLANs.

---

# 🛠️ Step 7: Configure pfSense to Use Pi-hole for DNS Across VLANs

---

### 🔧 Update DHCP Settings in pfSense for Each VLAN

Log into the **pfSense Web UI** from your Debian Admin Machine.

1. Navigate to:  
   `Services ➝ DHCP Server`

2. For each VLAN (e.g., **LAN**, **VLAN 10**, **VLAN 20**, **VLAN 30** tabs):
   - Set **DNS servers** to `192.168.20.2` (your Pi-hole IP).
   - Scroll down and click **Save**.
   - Click **Apply Changes** (if prompted).

📸 **Screenshots**  
*(VLAN10)*
![DNS VLAN10](33_VLAN10.png) 
*(VLAN20)*
![DNS VLAN20](34_VLAN20.png)
*(VLAN30)*
![DNS VLAN30](35_VLAN30.png)

> 🧠 This ensures all new DHCP clients in these VLANs will use Pi-hole as their DNS server.

---

# ✅ Step 8: Things to Check Before Enabling DNS Redirection

1. Go to:  
   `System ➝ General Setup`
   
![System_General](36_System_Gen.png)

2. Under **DNS Server Settings**:
   - Set **DNS Server 1**: `192.168.20.2`
   - ✅ **Uncheck**:  
     `Allow DNS server list to be overridden by DHCP/PPP on WAN
     
![DNS_Setting](37_DNS.png)

> ⚠️ This ensures pfSense itself uses Pi-hole as its DNS resolver (optional but cleaner).

---

🚫 3. Disable DNS Resolver or Forwarder (Optional)

Only do this **if you want ALL DNS to go through Pi-hole**, and not be handled by pfSense.

- Go to:
  - `Services ➝ DNS Resolver` → **Disable**
  - *OR*
  - `Services ➝ DNS Forwarder` → **Disable** (if using this instead)

![DNS_Forward](38_DNS_Forward.png)
![DNS_Resolver](39_DNS_Resolver.png)

> ⚠️ **Important:**  
> If pfSense still needs to resolve DNS for itself, leave **one** enabled.  
> (In this setup, **DNS Resolver** was left enabled.)

---

🔁 4: Set Up DNS Redirection to Pi-hole (`192.168.20.2`)

We'll do this per VLAN using **Firewall ➝ NAT ➝ Port Forward**.

![Port_Forward](40_Port_Forward.png)

🔨 DNS Redirection Steps (Repeat per VLAN)

Click **+ Add**

Fill in the following:

| Field | Value |
|-------|-------|
| **Interface** | Select the VLAN (e.g., LAN 10) |
| **Protocol** | TCP/UDP |
| **Source Type** | Network |
| **Source Address** | e.g., `192.168.10.0/24` |
| **Source Port Range** | any |
| **Destination** | any |
| **Destination Port Range** | DNS (53) |
| **Redirect Target IP** | `192.168.20.2` (your Pi-hole) |
| **Redirect Target Port** | DNS (53) |
| **Description** | `Redirect DNS to Pi-hole VLAN10` |
