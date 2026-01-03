# Certificates Strategy (PKI) — techtheworld Homelab

This document defines the **certificate (PKI) strategy** for the techtheworld homelab and mock enterprise environment.
The design intentionally mirrors real enterprise and MSP-grade certificate practices.

---

## Domains

- **External domain (public DNS):** `techtheworld.win`
  - Managed by Cloudflare (authoritative)
- **Internal domain (private DNS / AD):** `corp.techtheworld.win`

---

## Goals

- Eliminate browser and client TLS warnings for internal services
- Enable HTTPS for all internal dashboards, APIs, and admin portals
- Support enterprise identity patterns (Active Directory, SSO readiness)
- Enable future VPN, RADIUS, and 802.1X certificate authentication
- Make the lab portable into MSP offerings
- Maintain auditable and repeatable security practices

---

## Trust Model

### Authoritative Strategy (Long-term)
An **Internal Certificate Authority (Internal CA)** is the authoritative trust anchor.

### Bootstrap Allowance (Temporary)
Self-signed certificates are permitted **only** when:
- A service must be deployed before the CA exists
- The certificate will later be replaced by a CA-issued certificate

**Rule:** All self-signed certificates must be replaced once the Internal CA is live.

---

## DNS Responsibility Boundaries

### Public DNS (Cloudflare)
- Manages only `techtheworld.win`
- No private IP records
- No internal hostnames

### Internal DNS (Private)
- Manages `corp.techtheworld.win`
- Example hostnames:
  - `pve01.corp.techtheworld.win`
  - `fw01.corp.techtheworld.win`
  - `odoo01.corp.techtheworld.win`
  - `vault01.corp.techtheworld.win`
  - `mon01.corp.techtheworld.win`

---

## PKI Architecture Summary

This lab uses a **two-tier PKI model**:

```
Offline Root CA
    ↓
Online Issuing CA
    ↓
Internal Services / Devices / Users
```

See: `internal-ca-architecture.md`

---

## Certificate Types

### Internal Service Certificates
Used for HTTPS on:
- Odoo (IT Glue–like control plane)
- Vaultwarden / secrets manager
- Monitoring (Grafana / Prometheus)
- Reverse proxy (Caddy / Nginx / Traefik)
- Proxmox UI (optional replacement later)

### Client / Device Certificates (Future)
Used for:
- VPN authentication
- RADIUS / 802.1X (EAP-TLS)
- Admin workstation identity
- Mutual TLS between services

### Automation / Code Signing (Future)
Used for:
- Script signing
- Secure automation workflows
- Agent trust models

---

## Naming Conventions

### Hostnames
Format:
- `<role><##>.corp.techtheworld.win`

### Certificate CN / SAN Rules
- SAN must include:
  - FQDN (`service01.corp.techtheworld.win`)
  - Short name (`service01`) if used
- Prefer DNS SANs over IP SANs

---

## Certificate Lifetimes

| Certificate Type | Validity |
|-----------------|----------|
| Root CA         | 10+ years |
| Issuing CA     | 5 years |
| Leaf certs     | 90–365 days |

---

## Trust Distribution

### Windows
- Root CA distributed via Group Policy (future)

### Linux
- Install Root CA into system trust store

---

## Validation Checklist

- [ ] Internal DNS resolves `*.corp.techtheworld.win`
- [ ] Root CA trusted by Linux hosts
- [ ] Root CA trusted by Windows hosts
- [ ] No browser TLS warnings
- [ ] Renewal process documented
