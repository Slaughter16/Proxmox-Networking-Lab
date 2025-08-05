# 🛡️ OpenVPN Setup on pfSense — Step-by-Step Guide

This guide walks through setting up an OpenVPN server on **pfSense** and connecting a Windows client. Each section is meant to be documented with screenshots alongside the steps.

## Table of Contents

1. 🏛️ [Create a Certificate Authority (CA)](#-1-create-a-certificate-authority-ca)  
2. 🏷️ [Create the Server Certificate](#-2-create-the-server-certificate)  
3. 👤 [Create a User Certificate](#-3-create-a-user-certificate)  
4. 🧙 [Run the OpenVPN Wizard](#-4-run-the-openvpn-wizard)  
5. 💾 [Export the OpenVPN Client Configuration](#-5-export-the-openvpn-client-configuration)  
6. 🖥️ [Windows OpenVPN Client Setup with pfSense Export](#-6-windows-openvpn-client-setup-with-pfsense-export)  
   - ⬇️ [Step 1: Download OpenVPN Installer from pfSense](#step-1-download-openvpn-installer-from-pfsense)  
   - 🛠️ [Step 2: Install OpenVPN on Windows](#step-2-install-openvpn-on-windows)  
   - 🔌 [Step 3: Connect to pfSense VPN](#step-3-connect-to-pfsense-vpn)  
   - 📡 [Step 4: Test Internal Network Access (Ping Test)](#step-4-test-internal-network-access-ping-test)  
7. 🛠️ [Fix: Missing Users in Export List](#fix-missing-users-in-export-list)  
   - 👤 [Step 1: Create a User with Linked Certificate](#step-1-create-a-user-with-linked-certificate)  
   - 🔄 [Step 2: Return to Client Export](#step-2-return-to-client-export)  
8. 🧹 [Uninstall or Clean Up](#uninstall-or-clean-up)  

---

## 📍 1. Create a Certificate Authority (CA)

Navigate to:  
**`System > Certificates > Authorities`**

1. Click ➕ **Add**

![Cert](./screenshots/1_Cert_Sys.png)
![Cert](./screenshots/2_Cert_Auth.png)

2. Set:
   - **Descriptive Name:** `OpenVPN-CA`
   - **Method:** `Create an internal Certificate Authority`
   - **Key Length:** `2048` or `4096`
   - **Digest Algorithm:** `SHA256`
   - Fill out country, state, etc.

3. Click **Save**

![Cert](./screenshots/3_OpenVPN.png)
![Cert](./screenshots/4_OpenVPN.png)
![Cert](./screenshots/5_OpenVPN.png)

---

## 📍 2. Create the Server Certificate

Navigate to:  
**`System > Certificates > Certificates`**

1. Click ➕ **Add/Sign**

![Cert](./screenshots/6_OpenVPN.png)

2. Configure:
   - **Method:** `Create an internal certificate`
   - **Descriptive Name:** `OpenVPN-Server`
   - **Certificate Authority:** `OpenVPN-CA`
   - **Type:** `Server Certificate`
   - **Common Name:** `OpenVPN-Server`

3. Click **Save**

![Cert](./screenshots/7_OpenVPN.png)
![Cert](./screenshots/8_OpenVPN.png)

---

## 📍 3. Create a User Certificate

Still under **Certificates > Certificates**:

1. Click ➕ **Add/Sign**

2. Set:
   - **Method:** `Create an internal certificate`
   - **Descriptive Name:** `OpenVPN-User1`
   - **Certificate Authority:** `OpenVPN-CA`
   - **Type:** `User Certificate`
   - **Common Name:** `user1`

3. Click **Save**

![Cert](./screenshots/9_OpenVPN.png)
![Cert](./screenshots/10_OpenVPN.png)
![Cert](./screenshots/11_OpenVPN.png)

---

## 📍 4. Run the OpenVPN Wizard

Navigate to:  
**`VPN > OpenVPN > Wizards`**

![Cert](./screenshots/12_OpenVPN.png)
![Cert](./screenshots/13_OpenVPN.png)

Follow these steps:

**Type:** `Local User Access`
   
![Cert](./screenshots/14_OpenVPN.png)

**CA:** Select `OpenVPN-CA`
![Cert](./screenshots/15_OpenVPN.png)

**Server Certificate:** `OpenVPN-Server`
**Interface:** `WAN`
**Protocol:** `UDP`, Port `1194`
**Tunnel Network:** `10.8.0.0/24`
**Local Network:** `192.168.10.0/24` (or your VLAN10 subnet)

![Cert](./screenshots/16_OpenVPN.png)
![Cert](./screenshots/17_OpenVPN.png)
![Cert](./screenshots/18_OpenVPN.png)
![Cert](./screenshots/19_OpenVPN.png)

**Client Settings:** (Optional DNS options)
**Firewall Rules:** ✔️ `Auto-create`

![Cert](./screenshots/20_OpenVPN.png)
![Cert](./screenshots/21_OpenVPN.png)

Click **Finish**

![Cert](./screenshots/22_OpenVPN.png)
![Cert](./screenshots/23_OpenVPN.png)

---

## 📍 5. Export the OpenVPN Client Configuration

Go to:  
**`VPN > OpenVPN > Client Export`**

> 🔸 If you don't see this menu, install the package:
> `System > Package Manager > Available Packages`

![Cert](./screenshots/25_OpenVPN.png)
![Cert](./screenshots/26_OpenVPN.png)


Search for `openvpn-client-export`, then click **Install**

![Cert](./screenshots/27_OpenVPN.png)
![Cert](./screenshots/28_OpenVPN.png)
![Cert](./screenshots/29_OpenVPN.png)

### Once Installed:

1. Scroll to the **OpenVPN Clients** section
![Cert](./screenshots/30_OpenVPN.png)

2. Look for your user (e.g., `vpnuser`)
3. Choose export type:
   - Windows Installer (64-bit)
   - Archive (.zip)
   - Inline Config (.ovpn)

![Cert](./screenshots/37_OpenVPN.png)

---

# 🔐 6. Windows OpenVPN Client Setup with pfSense Export

### Before connecting , ping from WinServer (192.168.20.102) to DebianAdmin (192.168.10.101) failed

![Before_OpenVPN](./screenshots/52_openVPNN.png)

---

### Step 1: Download OpenVPN Installer from pfSense

- On WinServer navigate to `VPN → OpenVPN → Client Export` in pfSense.
- Select:
  - **Remote Access Server:** `openvpn-remoteaccess UDP4:1194`
  - **User Export:** `vpnuser-installI001-amd64.exe`
- Click **Keep** when prompted by browser.
  
![Download](./screenshots/38_openVPN.png)
![Download](./screenshots/39_openVPN.png)

---

### Step 2: Install OpenVPN on Windows

- Double-click the `.exe` file to launch the installer.
- Windows SmartScreen warning may appear:
  - Click **More info** → **Run anyway**  
![SmartScreen](./screenshots/40_openVPN.png)

- Click **Install Now** to begin setup.

![Install Now](./screenshots/41_openVPN.png)

- Allow installer permissions: Click **Yes**.

![Download](./screenshots/42_openVPN.png)

![Download](./screenshots/43_openVPN.png)

- When prompted, Allow `openvpn-postinstall.exe` changes.

![Download](./screenshots/44_openVPNN.png)

- Click **Install** to confirm TAP driver setup.

![Download](./screenshots/45_openVPNN.png)

- Final confirmation: Installation complete.

![Post Install](./screenshots/46_openVPNN.png)

---

### Step 3: Connect to pfSense VPN

- Locate the **OpenVPN icon** in the system tray (bottom right).
- Right-click → Select **Connect**.
![Post Install](./screenshots/47_openVPNN.png)

- Choose the config: `vpnuser-config (UDP4:1194)`
- When prompted, enter your **Username** and **Password** from pfSense.

![Post Install](./screenshots/48_openVPNN.png)

- After successful login:

![Post_Install](./screenshots/49_openVPNN.png)

---

### Step 4: Test Internal Network Access (Ping Test)

After connecting, open Command Prompt and run:

```bash
ping 192.168.10.101     # Debian Admin Machine (VLAN10) → Success ✅
ipconfig /all   # Check the IP OpenVPN issued (10.8.0.2) → Success ✅
```

![Post_Install](./screenshots/50_openVPNN.png)
![Post_Install](./screenshots/51_openVPNN.png)



## 🔁 Fix: Missing Users in Export List

### Step 1: Create a User with Linked Certificate

1. Go to: `System > User Manager > Users`
![Cert](./screenshots/30_OpenVPN.png)

2. Click **Add**
![Cert](./screenshots/31_OpenVPN.png)

3. Fill in:
   - **Username:** `vpnuser`
   - **Password:** (strong)
   - Under **Certificate**, select `OpenVPN-User1`
4. Click **Save**
![Cert](./screenshots/32_OpenVPN.png)
![Cert](./screenshots/33_OpenVPN.png)
![Cert](./screenshots/34_OpenVPN.png)

### Step 2: Return to Client Export

1. Go to `VPN > OpenVPN > Client Export`
![Cert](./screenshots/35_OpenVPN.png)

2. Scroll down — user `vpnuser` should now appear
3. Export Windows Installer or .ovpn file
![Cert](./screenshots/36_OpenVPN.png)
![Cert](./screenshots/37_OpenVPN.png)

---

## 🧹 Uninstall or Clean Up

### To Remove VPN Setup from Client VM:

1. Uninstall **OpenVPN GUI** via `Apps & Features`
2. Delete config files from:
   - `C:\Program Files\OpenVPN\config\`
   - `C:\Users\<YourUser>\OpenVPN\config\`

### To Delete on pfSense:

1. **VPN > OpenVPN > Servers** — Delete the VPN server
2. **System > Certificates** — Delete server & user certs
3. **System > Certificate Authorities** — Delete CA (if not reused)
4. **System > User Manager > Users** — Delete user

