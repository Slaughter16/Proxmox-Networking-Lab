# 🛠️ Troubleshooting DNS and Pi-hole Issues

## ❌ Problem: Client devices and Pi-hole itself were unable to resolve domain names.

### Symptoms:
- `nslookup` and `dig` commands failed with timeouts
- `curl` returned “Could not resolve host”
- Pi-hole showed upstream DNS and NTP errors
- DHCP was functional, but no name resolution

- Pi-hole dashboard shows errors about NTP and upstream DNS
- Clients appear to get IP via DHCP, but no hostname resolution

## 🧠 Root Cause:

The **pfSense NAT Port Forward rule** redirected all DNS traffic (port 53) to Pi-hole — including traffic **originating from Pi-hole itself**.

Since the rule did **not exclude Pi-hole's own IP (`192.168.20.2`)**, the DNS resolver looped back and failed to reach any upstream servers (e.g., `8.8.8.8`).

Additionally:
- `/etc/resolv.conf` on Pi-hole pointed to `127.0.0.1`
- DNSSEC caused further resolution failures


### ✅ Fix:
1. **Port Forward NAT Rule with Invert Match**
2. Update Pi-hole upstream DNS settings
3. Disable DNSSEC
4. Manually edit `/etc/resolv.conf`

---

# DNS Resolution Test (Before and After NAT Invert Match Fix)

This folder documents how DNS resolution was affected when the NAT redirect rules for DNS traffic were **not** excluding the Pi-hole (`192.168.20.2`) via "Invert Match."

---

## 🔧 Problem Summary

When **"Invert match"** was **unchecked** in the NAT Port Forward rule:

- All DNS traffic, including Pi-hole’s own queries, was redirected back to itself.
- This caused Pi-hole to fail DNS resolution because it could not reach upstream DNS (like 8.8.8.8).
- As a result, **clients in all VLANs could not resolve domain names**.

---

## 🧪 Testing Tools

The following commands were used in each VMs console to confirm DNS status from clients:

```bash
nslookup google.com
dig google.com
curl https://www.google.com
```
Windows 10 Client
![Win10](1_Troubleshoot_Win.png)

Debian Admin Workstation
![Debian](2_Troubleshoot_Debian.png)

Windows Server 2019
![WinServer](3_Troubleshoot_WinServer.png)

Metasploitable 2
![Meta](4_Troubleshoot_Meta.png)

Pihole
![Pihole](5_Troubleshoot_Pihole.png)


Kali Linux
![Kali](6_Troubleshoot_Kali.png)

Security Onion
![SecO](7_Troubleshoot_Seconion.png)
