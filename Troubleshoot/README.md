# 🛠️ Troubleshooting DNS and Pi-hole Issues

## ❌ Problem: DNS Resolution Fails on Clients and Pi-hole

### Symptoms:
- `nslookup` fails with timeout
- `dig` to 8.8.8.8 fails
- `curl` returns "Could not resolve host"

- Pi-hole dashboard shows errors about NTP and upstream DNS
- Clients appear to get IP via DHCP, but no hostname resolution

### Root Cause:
- Pi-hole was being redirected by its **own NAT rule** in pfSense
- No valid upstream DNS or DNSSEC issues
- /etc/resolv.conf incorrectly pointed to itself (127.0.0.1)

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

The following commands were used to confirm DNS status from clients:

```bash
nslookup google.com
dig google.com
curl https://www.google.com
```

![Win10](1_Troubleshoot_Win.png)

![Debian](2_Troubleshoot_Debian.png)

![WinServer](3_Troubleshoot_WinServer.png)

![Meta](4_Troubleshoot_Meta.png)

![Pihole](5_Troubleshoot_Pihole.png)

![Kali](6_Troubleshoot_Kali.png)

![SecO](7_Troubleshoot_Seconion.png)
