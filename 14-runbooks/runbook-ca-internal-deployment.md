# Runbook: Internal Certificate Authority (Linux VM)

## Purpose
Establish an internal Certificate Authority (CA) to issue trusted certificates for internal services (Proxmox, Odoo, internal web apps, future AD integration).

## Scope
- Linux-based CA VM
- Internal-only trust
- No public certificate issuance
- Supports TLS, mTLS, and future Windows integration

## Preconditions
- Proxmox installed and reachable
- VLAN 10 operational
- DNS plan defined
- Snapshot capability available

## Step 1 — Provision CA VM
- OS: Debian 12 (minimal)
- vCPU: 1
- RAM: 2 GB
- Disk: 20 GB
- Network: VLAN 10
- Hostname: ca01.corp.techtheworld.win

## Step 2 — Base OS Hardening
- Disable root SSH login
- Enable automatic security updates
- Set timezone and NTP
- Create non-root admin user

## Step 3 — Install CA Tools
```bash
sudo apt update
sudo apt install -y openssl ca-certificates
```

## Step 4 — Initialize CA
- Create directory structure under /root/ca
- Generate root key (4096-bit RSA)
- Generate self-signed root certificate (10-year validity)

## Step 5 — Issue First Cert
- Create CSR for internal service
- Sign with root CA
- Export cert + key securely

## Validation
- Verify certificate chain
- Test TLS on internal service

## Rollback
- Revert VM snapshot
- Destroy CA VM if compromised

## Notes
- Root key never leaves CA
- Future: intermediate CA
