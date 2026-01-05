# Runbook: Internal DNS (Hybrid Windows + Linux)

## Purpose
Establish a reliable internal DNS architecture for the homelab that supports:
- Active Directory requirements
- Linux-based services (Proxmox, Odoo, Internal CA)
- Cloudflare-managed external DNS
- Proper certificate validation

Internal domain:
- corp.techtheworld.win

External domain:
- techtheworld.win

---

## Scope
- Internal-only DNS resolution
- Forward and reverse lookup zones
- Service discovery
- Certificate trust validation
- No public exposure of internal zones

---

## Design Principles
- Windows AD DNS is authoritative for corp.techtheworld.win
- Linux services use explicit DNS records
- pfSense operates as a DNS forwarder, not authority
- Cloudflare hosts public DNS only

---

## DNS Architecture

### Authoritative Zones
corp.techtheworld.win  -> Windows AD DNS  
_msdcs.corp.techtheworld.win -> Windows AD DNS  
techtheworld.win -> Cloudflare  

### Forwarding Flow
Clients -> pfSense -> AD DNS -> Internet Forwarders

---

## Phase Order
1. Deploy Windows AD DNS
2. Validate AD SRV records
3. Configure pfSense forwarding
4. Register Linux services
5. Validate internal certificates
6. Lock down external DNS exposure

---

## Step 1 — Windows AD DNS

Create AD-integrated zone:
```powershell
Add-DnsServerPrimaryZone -Name "corp.techtheworld.win" -ReplicationScope "Domain"
```

Verify SRV records:
```powershell
nslookup
set type=SRV
_ldap._tcp.dc._msdcs.corp.techtheworld.win
```

---

## Step 2 — pfSense DNS Resolver

Configuration:
- Enable DNS Resolver
- Enable DHCP lease registration
- Forward queries to AD DNS servers

Validation:
```bash
nslookup dc01.corp.techtheworld.win 192.168.10.1
```

---

## Step 3 — Linux Service Registration

Add static A records in AD DNS:
- proxmox01.corp.techtheworld.win
- odoo01.corp.techtheworld.win
- ca01.corp.techtheworld.win

Validate from Linux:
```bash
dig odoo01.corp.techtheworld.win
```

---

## Step 4 — Reverse Lookup Zones

Create reverse zones for internal subnets:
- 192.168.10.0/24
- 192.168.30.0/24

Validation:
```bash
dig -x 192.168.10.20
```

---

## Step 5 — Certificate Validation

Verify internal TLS:
```bash
openssl s_client -connect odoo01.corp.techtheworld.win:443
```

---

## Step 6 — Lockdown

- Block WAN recursion
- Prevent corp domain resolution externally
- Log DNS queries on pfSense

---

## Rollback
- Disable pfSense DNS forwarding
- Restore previous DHCP DNS settings
- Remove static service records

---

## Completion Criteria
- Internal DNS resolves consistently
- AD services fully functional
- Linux services discoverable
- Certificates validate without warnings
