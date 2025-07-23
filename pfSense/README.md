# pfSense VLAN Configuration

This folder documents the configuration of VLANs within pfSense as part of the lab network.

## Step 1: Log into pfSense Web GUI from Debian Admin Machine

- URL: https://[pfSense LAN IP]
- Default login (if not changed):
  - user:admin
  - pass:pfsense
  
![Login to pfSense](1_login_pfsense.png)

## Step 2: pfSense Dashboard
![pfSense Dashboard](2_dashboard.png)

## Step 3: Create VLAN Interfaces
Go to `Interfaces > Assignments > VLANs`  
Click `+ Add`

- **Parent Interface**: vmbr1 NIC (e.g., vtnet1)
- **VLAN Tag**: 10
- **Description**: VLAN10_Client

Repeat for:

- VLAN Tag: 20, Description: VLAN20_Server
- VLAN Tag: 30, Description: VLAN30_Security

![VLAN10 Created](3_vlan10.png)
![VLAN20 Created](4_vlan20.png)
![VLAN30 Created](5_vlan30.png)
![All VLANs View](6_all_vlans.png)

## Step 4: Assign VLAN Interfaces
...

