# 🧩 Step 3: Configure VLANs in pfSense

This document outlines how to configure VLANs in pfSense to segment your Proxmox virtual lab network into isolated zones. VLANs allow segmentation between client workstations (VLAN10), production services (VLAN20), and security/monitoring tools (VLAN30). This improves both security and network organization in the virtual lab.

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
  -(A custom password was used in this setup)
![Login to pfSense](./screenshots/1_login_pfsense.png)

## pfSense Dashboard

Once logged in, you will see the dashboard.

![pfSense Dashboard](./screenshots/2_dashboard.png)

---

## 🔧 Create VLAN Interfaces

1. Navigate to: `Interfaces > Assignments > VLANs`
2. Click **➕ Add** for each VLAN.

---

![Before_VLAN_Interfaces Added](./screenshots/3_Before_VLAN.png)

### ➕ VLAN 10 – Clients

- **Parent Interface:** vmbr1 NIC (e.g., `vtnet1`)
- **VLAN Tag:** `10`
- **Description:** `VLAN10_Client`
  
✅ Click **Save**, then **Apply Changes**.

![VLAN 10](./screenshots/4_vlan10_add.png)

---

### ➕ VLAN 20 – Servers- 

- **VLAN Tag:** `20`
- **Description:** `VLAN20_Servers`

![VLAN 20](./screenshots/5_vlan20_add.png)

---

### ➕ VLAN 30 – Security
- **VLAN Tag:** `30`
- **Description:** `VLAN30_Security` (Originally mistyped, but VLAN 30 was correctly added later)

![VLAN 30](./screenshots/6_vlan30_add.png)

---

## 📋 Review All VLANs

After all are added, the VLAN list should appear like this:

![All VLANs](./screenshots/7_all_VLANS_listed.png)

---

## 🧬 Assign VLAN Interfaces

1. Go to `Interfaces > Assignments`
2. Click **+ Add** to assign each new VLAN interface.
   
![Interface>Assignments](./screenshots/8_Int_Assign.png)
![Add Interface](./screenshots/9_Add_Int.png)

---

### ⚙️ Configure LAN10 Interface (VLAN 10)
1. Click the new interface name (e.g., OPT1 → rename to **LAN10**).
2. Enable the interface.
3. Set **IPv4 Configuration Type** to `Static IPv4`.
4. Enter:
   - **IP Address:** `192.168.10.1`
   - **Subnet Mask:** `/24`

💾 Save and **Apply Changes**.

![Config VLAN10 Int](./screenshots/10_VLAN10_Int.png)
![Config VLAN10 Int](./screenshots/11_VLAN10_Inte.png)

---

## 🔁 Repeat for VLAN20 and VLAN30

Follow the same steps above for:

- **LAN20 (VLAN 20)**
  - IP: `192.168.20.1/24`
    
![Config VLAN20 Int](./screenshots/12_VLAN20_Int.png)
![Config VLAN20 Int](./screenshots/13_VLAN20_Int.png)

- **LAN30 (VLAN 30)**
  - IP: `192.168.30.1/24`

![Config VLAN30 Int](./screenshots/14_VLAN30_Int.png)
![Config VLAN30 Int](./screenshots/15_VLAN30_Int.png)

---

# 🛠️ Step 4: Enable DHCP on Each VLAN

## 🔹 Navigate to `Services > DHCP Server`

![Services_DHCP Server](./screenshots/16_DHCP_Page.png)

---

### 📦 Enable DHCP for LAN10

- Select `LAN10` tab
- Check **Enable DHCP server on LAN10 interface**
- Set Range:  
  - **From:** `192.168.10.100`  
  - **To:** `192.168.10.200`
- Click **Save**

![DHCP LAN10](./screenshots/17_dhcp_lan10.png)

---

### 📦 Enable DHCP for LAN20

- Select `LAN20` tab
- Check **Enable DHCP server on LAN20 interface**
- Set Range:  
  - **From:** `192.168.20.100`  
  - **To:** `192.168.20.200`
- Click **Save**

![DHCP LAN20](./screenshots/18_dhcp_lan20.png)

---

### 📦 Enable DHCP for LAN30

- Select `LAN30` tab
- Check **Enable DHCP server on LAN30 interface**
- Set Range:  
  - **From:** `192.168.30.100`  
  - **To:** `192.168.30.150`
- Click **Save**

![DHCP LAN30](./screenshots/19_dhcp_lan30.png)

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
![Firewall_Rules](./screenshots/20_Firewall_Rules.png)

---

## ➕ Add Rule for VLAN10

1. Click the **LAN10** tab  
2. Click **➕ Add** at the top of the rules list
![Firewall_Tabs](./screenshots/21_Firewall_Tabs.png)

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
![Allow All VLAN10](./screenshots/22_Allow_Pro.png)
![Allow All VLAN10](./screenshots/23_Allow_VLAN10.png)
![Allow All VLAN10](./screenshots/24_Allow_Final10.png)

✅ Click **Save** then **Apply Changes**

---

## ➕ Add Rule for VLAN20

1. Go to the **LAN20** tab  
2. Click **➕ Add** at the top
   
![Allow All VLAN20](./screenshots/25_LAN20.png)

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
![Allow All VLAN20](./screenshots/26_Allow_Pro.png)
![Allow All VLAN20](./screenshots/27_Allow_VLAN20.png)
![Allow All VLAN20](./screenshots/28_Allow_VLAN20.png)

✅ Save and **Apply Changes**

---

## ➕ Add Rule for VLAN30

1. Navigate to the **LAN30** tab  
2. Click **➕ Add** at the top
   
![Allow All VLAN20](./screenshots/29_LAN30.png)

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
![Allow All VLAN30](./screenshots/30_Allow_Pro.png)
![Allow All VLAN30](./screenshots/31_Allow_VLAN30.png)
![Allow All VLAN30](./screenshots/32_Allow_VLAN30_Final.png)

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
![DNS VLAN10](./screenshots/33_VLAN10.png) 
*(VLAN20)*
![DNS VLAN20](./screenshots/34_VLAN20.png)
*(VLAN30)*
![DNS VLAN30](./screenshots/35_VLAN30.png)

> 🧠 This ensures all new DHCP clients in these VLANs will use Pi-hole as their DNS server.

---

# ✅ Step 8: Things to Check Before Enabling DNS Redirection

1. Go to:  
   `System ➝ General Setup`
   
![System_General](./screenshots/36_System_Gen.png)

2. Under **DNS Server Settings**:
   - Set **DNS Server 1**: `192.168.20.2`
   - ✅ **Uncheck**:  
     `Allow DNS server list to be overridden by DHCP/PPP on WAN
     
![DNS_Setting](./screenshots/37_DNS.png)

> ⚠️ This ensures pfSense itself uses Pi-hole as its DNS resolver (optional but cleaner).

---

🚫 3. Disable DNS Resolver or Forwarder (Optional)

Only do this **if you want ALL DNS to go through Pi-hole**, and not be handled by pfSense.

- Go to:
  - `Services ➝ DNS Resolver` → **Disable**
  - *OR*
  - `Services ➝ DNS Forwarder` → **Disable** (if using this instead)

![DNS_Forward](./screenshots/38_DNS_Forward.png)
![DNS_Resolver](./screenshots/39_DNS_Resolver.png)

> ⚠️ **Important:**  
> If pfSense still needs to resolve DNS for itself, leave **one** enabled.  
> (In this setup, **DNS Resolver** was left enabled.)

---

# ✅ Step 9: Set Up DNS Redirection to Pi-hole (`192.168.20.2`)

We'll do this per VLAN using **Firewall ➝ NAT ➝ Port Forward**.

![Port_Forward](./screenshots/40_Port_Forward.png)

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

Options:
   - ✅ NAT Reflection: **Disable** (default)
   - ✅ Filter Rule Association: **Add associated filter rule**
   - ✅ Check the box: **Redirect target port**

![VLAN10_NAT_PortFwd](./screenshots/41_VLAN10.png)
![VLAN10_NAT_PortFwd](./screenshots/42_VLAN10.png)
Click **Save** → **Apply Changes**

🔁 **Repeat** for **VLAN 20** and **VLAN 30**  
Just change the **Interface** and **Source Address** accordingly:

- VLAN 20: `192.168.20.0/24`
![VLAN20_NAT_PortFwd](./screenshots/43_VLAN20.png)
![VLAN20_NAT_PortFwd](./screenshots/44_VLAN20.png)
- VLAN 30: `192.168.30.0/24`
![VLAN30_NAT_PortFwd](./screenshots/45_VLAN30.png)
![VLAN30_NAT_PortFwd](./screenshots/46_VLAN30.png)
![VLAN_NAT_PortFwd](./screenshots/47_VLAN.png)
---

✅ **Result:** All DNS traffic in each VLAN 'should' be intercepted and redirected to Pi-hole (`192.168.20.2`), even if clients try to use external DNS servers (e.g., `8.8.8.8` or `1.1.1.1`).

---

# Step 10: Verify DHCP Leases

The table below shows the DHCP lease assignments for each virtual machine, along with their associated VLANs and IP addresses as configured in pfSense:

| VM Name             | VLAN   | IP Address       |
|---------------------|--------|------------------|
| Win10 Client        | VLAN 10| 192.168.10.100   |
| Debian Admin Station| VLAN 10| 192.168.10.101   |
| WinServer           | VLAN 20| 192.168.20.102   |
| Meta                | VLAN 20| 192.168.20.101   |
| Kali Linux          | VLAN 30| 192.168.30.100   |
| Security Onion      | VLAN 30| 192.168.30.101   |

![DHCP_Leases](./screenshots/48_DHCP_Leases.png)
