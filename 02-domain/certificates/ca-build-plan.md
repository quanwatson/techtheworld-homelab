# CA Build Plan — Phase 4.x

This document defines the **execution plan** for deploying the Internal CA.

---

## Phase Mapping

- Phase 4.1: PKI strategy documented (complete)
- Phase 4.2: Proxmox deployment
- Phase 4.3: Internal DNS + CA deployment
- Phase 4.4: Issue certificates to services
- Phase 4.5: VPN / RADIUS / 802.1X integration

---

## Step 1 — Prepare Infrastructure

- Create Linux VM for Root CA (offline)
- Create Linux VM for Issuing CA (online)
- Assign static IPs
- Document hostnames

---

## Step 2 — Build Offline Root CA

- Install minimal OS
- Generate Root CA private key
- Create Root CA certificate (10+ years)
- Snapshot VM
- Create encrypted offline backup
- Power off Root CA

---

## Step 3 — Build Online Issuing CA

- Install CA tooling
- Generate Issuing CA key + CSR
- Temporarily power on Root CA
- Sign Issuing CA certificate
- Power off Root CA
- Snapshot Issuing CA VM

---

## Step 4 — Trust Distribution

- Export Root CA public cert
- Install Root CA into:
  - Linux hosts
  - Proxmox
  - Admin workstations
- Verify no browser warnings

---

## Step 5 — First Certificate Issuance

- Reverse proxy
- Odoo
- Monitoring stack
- Replace all self-signed certs

---

## Step 6 — Documentation

- Log CA creation in Build Journal
- Update certificate inventory
- Document renewal timelines

---

## Success Criteria

- Trusted HTTPS for all internal services
- No TLS warnings
- CA lifecycle documented
- Ready for VPN and 802.1X
