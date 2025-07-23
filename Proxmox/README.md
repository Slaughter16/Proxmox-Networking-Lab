### Step 1: Proxmox – Editing vmbr1 for VLAN Awareness
Navigated to **Datacenter > Node > System > Network**

### Before Editing
In the original configuration, `vmbr1` was not set to support VLANs.

![Before Editing vmbr1](1_before_vmbr1.png)

---

### Enabling VLAN Awareness

Selected **vmbr1**, then enabled the **VLAN Aware** checkbox to allow VLAN-tagged traffic to pass through.

![Config VLAN Aware vmbr1](2_vlan_vmbr1.png)

> 💡 This setting is crucial for allowing Proxmox to bridge VLAN-tagged traffic across virtual machines and physical interfaces.
---
✅ Click **Apply Configuration** after making the change.

---
### Confirming VLAN Awareness is Enabled

Checked that **vmbr1** now shows **VLAN Aware: Yes**.

![VLAN Aware Enabled](3_vlan_aware_enabled_vmbr1.png)

