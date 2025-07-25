# 🛠️ Troubleshooting DNS and Pi-hole Issues

## ❌ Problem: DNS Resolution Fails on Clients and Pi-hole

### Symptoms:
- `nslookup` fails with timeout
- `dig` to 8.8.8.8 fails
- `curl` returns "Could not resolve host"
- Pi-hole dashboard shows errors about NTP and upstream DNS
- Clients appear to get IP via DHCP, but no hostname resolution
