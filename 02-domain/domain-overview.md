# Domain Overview

## Purpose

This document defines the authoritative domain architecture for the TechTheWorld Homelab.
It establishes clear separation between **external (public)** and **internal (directory-based)** domains,
mirroring real-world enterprise and MSP best practices.

This domain model supports:
- Secure internal authentication and identity management
- Scalable service deployment from Proxmox
- Future MSP-style client environments
- Hybrid on-prem + cloud integration

No production services are exposed until explicitly documented and approved.

---

## Domain Structure

### External (Public) Domain
- **Domain:** `techtheworld.win`
- **Registrar / DNS Provider:** Cloudflare
- **Purpose:**
  - Public-facing services
  - Marketing sites
  - Client portals
  - Remote access endpoints (future)
- **Security Boundary:** Internet-facing (zero trust posture)

---

### Internal (Directory / Identity) Domain
- **Active Directory Domain:** `corp.techtheworld.win`
- **Scope:** Internal only (non-routable from internet)
- **Purpose:**
  - User authentication (human + service accounts)
  - Computer and server identity
  - Group Policy enforcement
  - Internal DNS resolution
- **Trust Model:** No automatic trust with external domain

---

## Naming & Separation Principles

| Component | Rule |
|---------|------|
| External DNS | Managed exclusively via Cloudflare |
| Internal DNS | Managed via Active Directory-integrated DNS |
| AD Namespace | Subdomain of external domain (industry best practice) |
| Internal Services | Never directly exposed to public DNS |
| Certificates | Internal CA for AD, public CA for external services |

This prevents namespace collision and enables clean hybrid growth.

---

## DNS Responsibility Split

### External DNS (`techtheworld.win`)
Handled by:
- Cloudflare DNS
- Used for:
  - Public A / CNAME records
  - Future reverse proxies
  - External TLS certificates

### Internal DNS (`corp.techtheworld.win`)
Handled by:
- Windows Server AD DNS
- Used for:
  - Domain controllers
  - Internal services
  - Proxmox-hosted infrastructure
  - Private service discovery

---

## Planned Internal Services (Phase 4+)

- Active Directory Domain Services (Windows Server)
- Internal DNS (AD-integrated)
- Certificate Authority (internal PKI)
- Proxmox-hosted services:
  - Documentation systems
  - Asset management
  - Password vault / IT Glue alternative
  - Automation platforms
  - Private AI services

---

## Security Posture

- No split-brain DNS
- No public exposure of AD services
- No wildcard external records
- Explicit allow-only publication model
- All exposure requires:
  - Firewall rule
  - DNS record
  - Documentation entry
  - Build Journal entry

---

## Phase Alignment

| Phase | Status |
|-----|------|
| Phase 1 – Network Foundation | Complete |
| Phase 2 – VLAN Enforcement | Complete |
| Phase 3 – Switch Hardening | Complete |
| **Phase 4 – Service Enablement** | **In Progress** |

---

## Next Steps

- Finalize Proxmox deployment
- Stand up first Windows Server DC
- Implement internal DNS zone for `corp.techtheworld.win`
- Integrate Cloudflare DNS documentation (no records yet)
- Begin service catalog planning

> This document is **authoritative** for all domain-related decisions.
