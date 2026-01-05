# Runbook: Proxmox VM Layout & Naming Standards

## Purpose
Define **standardized VM naming, IP allocation, VLAN placement, and resource sizing** before any VM creation.
This runbook prevents drift, simplifies troubleshooting, and mirrors MSP / enterprise conventions.

## Scope
- Applies to all VMs hosted on Proxmox
- Covers core services first (CA, DNS, Secrets, Odoo)
- Defers Active Directory until later phase by design

## Preconditions
- Phase 4.1 complete (Domain & Certificate strategy approved)
- Proxmox host installed and reachable (Phase 4.2 install runbook)
- VLAN 10 (LAB) stable and enforced
- Documentation is the source of truth

---

## Global Standards

### Naming Convention
```
<role>-<service>-<index>.<zone>
```

**Examples**
- ca-root-01.lab
- dns-int-01.lab
- secrets-vault-01.lab
- odoo-core-01.lab

### Hostname Rules
- Lowercase only
- Hyphen-separated
- No spaces or underscores
- Stable names (never reuse for different roles)

### VM ID Allocation (Proxmox)
| Range | Purpose |
|-----|--------|
| 100–199 | Core infrastructure |
| 200–299 | Control plane / apps |
| 300–399 | Identity (future AD) |
| 900–999 | Temporary / testing |

---

## Network & VLAN Placement

| Service | VLAN | Subnet | Notes |
|------|-----|-------|------|
| CA | VLAN 10 (LAB) | 192.168.10.0/24 | Internal-only |
| DNS | VLAN 10 (LAB) | 192.168.10.0/24 | Internal resolution |
| Secrets | VLAN 10 (LAB) | 192.168.10.0/24 | No external exposure |
| Odoo | VLAN 10 (LAB) | 192.168.10.0/24 | Reverse proxy later |
| AD (future) | VLAN 30 (MGMT) | Planned | Not deployed yet |

> Rule: **Core services do not live in IoT or user VLANs**.

---

## IP Address Allocation (Reserved)

| Service | Hostname | IP |
|------|---------|----|
| CA | ca-root-01.lab | 192.168.10.10 |
| DNS | dns-int-01.lab | 192.168.10.11 |
| Secrets | secrets-vault-01.lab | 192.168.10.12 |
| Odoo | odoo-core-01.lab | 192.168.10.20 |

- Use DHCP reservations or static IPs (document which)
- Never auto-assign for core services

---

## VM Resource Sizing (Initial)

| Service | vCPU | RAM | Disk |
|------|-----|-----|------|
| CA | 1 | 2 GB | 20 GB |
| DNS | 1 | 2 GB | 20 GB |
| Secrets | 2 | 4 GB | 40 GB |
| Odoo | 2 | 6 GB | 80 GB |
| AD (future) | 2 | 4–8 GB | 60 GB |

> Adjust only after monitoring and documentation update.

---

## Storage Placement
- OS disks: Local NVMe (performance)
- Data disks (later): Secondary SATA HDDs
- No shared storage required at this phase

---

## Security Guardrails
- No public exposure of CA, DNS, Secrets
- TLS required for Secrets and Odoo
- Certificates issued by internal CA
- Backups configured before production data

---

## Change Control
Before creating any VM:
- Update this runbook if deviations are needed
- Record intent in Change Control log
- Confirm rollback plan

---

## Rollback
- Power off and delete VM
- Release IP reservation
- Remove DNS entries
- Document rollback

---

## Notes
This runbook must be **reviewed before Phase 4.3 execution**.
