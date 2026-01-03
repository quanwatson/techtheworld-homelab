# Internal CA Architecture — techtheworld Homelab

This document defines the **internal PKI architecture** for the homelab.

---

## Objective

Provide a secure, enterprise-aligned PKI supporting:
- Internal HTTPS
- VPN authentication
- RADIUS / 802.1X
- Future SSO and Zero Trust models
- MSP-grade scalability

---

## Architecture Overview

```
[ Offline Root CA ]
        |
        v
[ Online Issuing CA ]
        |
        +--> HTTPS Certificates
        +--> VPN Certificates
        +--> RADIUS / 802.1X Certificates
        +--> Device / User Certificates
```

---

## Root CA (Offline)

**Purpose**
- Signs the Issuing CA
- Rarely used

**Security Controls**
- No internet access
- Powered off except for signing
- Snapshotted immediately
- Encrypted offline backups

**Identity**
- CN: TTW-ROOT-CA
- O: TechTheWorld
- OU: Certificate Authority

---

## Issuing CA (Online)

**Purpose**
- Issues and renews certificates
- Handles revocation

**Security Controls**
- Internal-only access
- Limited admin accounts
- Encrypted backups
- Logging enabled

**Identity**
- CN: TTW-ISSUING-CA
- O: TechTheWorld
- OU: Certificate Authority

---

## Hosting Model

- Root CA: Linux VM (offline)
- Issuing CA: Linux VM (online)

Planned realism:
- Migrate to Windows AD CS when AD is deployed

---

## Certificate Profiles

### HTTPS Server Certificates
- SAN-based
- No wildcards by default
- 90–365 day validity

### VPN / RADIUS Certificates
- Strong identity binding
- Revocation-capable

---

## Self-Signed Policy

Self-signed certificates allowed **only** during bootstrap.
Never allowed for:
- VPN
- RADIUS / 802.1X
- Identity services
- Long-lived admin portals

---

## Logging Requirements

Log:
- Root CA creation and backup
- Issuing CA creation
- Critical certificate issuance
- Renewals and revocations
