# Phase 4.2 — Proxmox Execution Plan (Compute Substrate)

**Objective:** Stand up the hypervisor layer (Proxmox) cleanly so Phase 4.3 can deploy identity + core services.

## Definition of Done (Phase 4.2)

- Proxmox installed and reachable on **VLAN 10 (LAB)**
- Hostname standard set (example: `pve01`)
- Management access documented
- Storage layout documented
- Baseline security set (no exposed services to WAN)
- First VM template workflow decided (Linux + Windows)

---

## 4.2.1 Pre-Install Checklist

- [ ] Confirm pfSense VLAN 10 stable (gateway `192.168.10.1`)
- [ ] Switch access port for Proxmox host set to VLAN 10
- [ ] Confirm DHCP scope available OR choose static IP
- [ ] Decide Proxmox mgmt IP:
  - Option A: DHCP reservation in pfSense
  - Option B: static IP on Proxmox

Recommended: **DHCP reservation** (simpler early, still controlled)

---

## 4.2.2 Install Proxmox (Bare Metal)

- [ ] Download Proxmox ISO
- [ ] Install to target disk
- [ ] Set:
  - Hostname: `pve01.corp.techtheworld.win` (FQDN even before AD exists)
  - Admin email: use a non-private email (avoid GitHub private email issues)
  - IP: DHCP or static on VLAN 10

**Note:** Internal DNS isn’t live yet. Using the FQDN now is still fine—document it.

---

## 4.2.3 Post-Install Baseline

- [ ] Log in to Proxmox GUI
- [ ] Apply updates
- [ ] Confirm time/NTP
- [ ] Confirm networking:
  - Proxmox mgmt IP reachable from LAB workstation
  - Default route points to `192.168.10.1` (pfSense)

---

## 4.2.4 Storage Plan (Documented)

Decide and document:
- [ ] OS disk
- [ ] VM storage (ZFS / LVM-thin / ext4)
- [ ] ISO storage location
- [ ] Backup target plan (even if not deployed yet)

Recommended baseline:
- VM storage: **LVM-thin** (simple) OR **ZFS** (if you want snapshots + learning depth)

---

## 4.2.5 Network Plan (Phase 4.2 scope)

For now (simple):
- [ ] `vmbr0` on VLAN 10 only
- [ ] No additional VLAN trunks until later phases

Later (Phase 4.4+):
- Add VLAN-aware bridge and trunk to support VLAN 20/30/etc.

---

## 4.2.6 Baseline VM Templates (Decide)

- [ ] Linux template: Debian 12 or Ubuntu LTS (stable + common)
- [ ] Windows template: Windows Server (for AD later)
- [ ] Cloud-init approach decided for Linux automation

---

## 4.2.7 Documentation Outputs Required

Update these files:
- `compute/hypervisors.md` (Proxmox host details)
- `compute/hosts/<host>.md` (pve01 inventory)
- `compute/vms/vm-inventory.md` (initial empty inventory with format)
- `operations/backups.md` (backup intent and target placeholders)
- Build Journal: BJ entry for Phase 4.2 execution

---

## Phase 4.3 Preview (Next)

- Deploy Windows Server DC (`dc01`) for:
  - AD DS
  - DNS (internal)
  - (Optional) AD CS later for Internal CA
- Deploy secrets service (`vault01`)
- Deploy Odoo (`odoo01`)
- Deploy monitoring (`mon01`)
