# Runbook: Odoo Control Plane (IT-Glue-like Service)

## Purpose
Deploy Odoo Community Edition as an internal **control plane** for documentation, credentials (vaulted references), asset inventory, and service metadata—functionally similar to IT Glue, but self-hosted.

## Scope
- Proxmox VM deployment
- Odoo Community Edition (self-hosted)
- PostgreSQL backend
- Internal TLS via Internal CA
- No public exposure (internal-only)

## Preconditions
- Proxmox installed and reachable
- Internal CA available
- DNS planned for `odoo.corp.techtheworld.win`
- VLAN 10 (LAB) operational

---

## VM Specification
- **VM Name:** odoo-core
- **OS:** Debian 12
- **vCPU:** 2
- **RAM:** 4 GB
- **Disk:** 60 GB
- **Network:** VLAN 10

---

## Step 1 — Create VM
1. Create Debian 12 VM in Proxmox
2. Enable QEMU agent
3. Assign static DHCP reservation (recommended)

---

## Step 2 — Base OS Prep
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git ca-certificates gnupg
```

---

## Step 3 — PostgreSQL Install
```bash
sudo apt install -y postgresql
sudo systemctl enable --now postgresql
```

Create DB user:
```bash
sudo -u postgres createuser -s odoo
```

---

## Step 4 — Odoo Install
```bash
sudo apt install -y odoo
sudo systemctl enable --now odoo
```

---

## Step 5 — TLS (Internal CA)
1. Generate cert request for `odoo.corp.techtheworld.win`
2. Sign with Internal CA
3. Configure reverse proxy (nginx optional)

---

## Step 6 — Initial Configuration
- Create admin account
- Disable public signup
- Set internal-only access

---

## Validation
- HTTPS loads with trusted internal cert
- Login functional
- DB reachable

---

## Rollback
- Stop Odoo service
- Revert VM snapshot

---

## Notes
- Credentials stored as **references**, not secrets
- Secrets live in vault service later

