# Runbook: Proxmox VE Initial Installation (Bare Metal)

## Purpose
Install **Proxmox VE** on dedicated bare-metal hardware in a controlled, repeatable way.  
This runbook establishes a **stable virtualization foundation** without impacting household connectivity or upstream infrastructure.

This runbook **does not deploy any services** — it only prepares the host.

---

## Scope
- Bare-metal installation of Proxmox VE
- Initial host configuration (network, storage, access)
- No VMs, containers, or services deployed
- No integration with Active Directory or internal CA yet

---

## Preconditions (Do Not Skip)
- Phase 3 (Switch Hardening) is **complete and stable**
- VLAN 10 (LAB) is fully functional end-to-end
- Management access to:
  - pfSense (existing LAB access)
  - switchOTS (console access available)
- Proxmox host hardware is finalized and dedicated
- You have:
  - Keyboard + monitor access to the host
  - Proxmox VE ISO (verified checksum)
  - Bootable USB created
- Rollback path exists:
  - Host can be powered off without impacting household network
  - No production services depend on this host

---

## Inputs (Fill This In Before Installation)

- **Hostname:** `pve01`
- **Domain:** `corp.techtheworld.win`
- **Management VLAN:** VLAN 10 (LAB)
- **Management IP:** `192.168.10.___`
- **Gateway:** `192.168.10.1`
- **DNS Server:** `192.168.10.1` (pfSense for now)
- **Time Zone:** __________
- **Admin Email:** __________

---

## Step 1 — Document the Change (Change Control)
Before touching hardware:

1. Create a Change Control entry:
   - Purpose: Introduce virtualization host
   - Expected impact: None
   - Rollback: Power off host
2. Update documentation:
   - `hardware/proxmox-host.md` (placeholder allowed)
   - `network/ip-plan.md` (reserve management IP)
   - `topology.md` (logical update only)

> If documentation is not updated, stop here.

---

## Step 2 — Boot and Install Proxmox VE

1. Insert Proxmox VE USB
2. Boot host and select:
   - **Install Proxmox VE**
3. Accept license agreement
4. Select target disk:
   - Choose primary system disk only
   - Do **not** use external or secondary disks
5. Filesystem:
   - Use **default (ext4)** unless ZFS is explicitly planned later
6. Set:
   - Country
   - Time zone
   - Keyboard layout

---

## Step 3 — Initial System Identity

1. Set root password (strong, documented later in secure vault)
2. Enter admin email
3. Configure management network:
   - Interface: primary NIC
   - IP Address: `192.168.10.___`
   - Netmask: `/24`
   - Gateway: `192.168.10.1`
   - DNS: `192.168.10.1`
   - Hostname: `pve01.corp.techtheworld.win`

Confirm and proceed.

---

## Step 4 — Complete Installation and Reboot

1. Allow installer to finish
2. Remove installation media
3. Reboot system

---

## Step 5 — Initial Access Validation

From a LAB client:

1. Open browser:
   ```
   https://192.168.10.___:8006
   ```
2. Accept self-signed certificate warning
3. Login:
   - User: `root`
   - Realm: `pam`
4. Confirm:
   - Web UI loads correctly
   - Node shows **online**
   - No storage or network errors visible

> If UI is not reachable, stop and troubleshoot network before continuing.

---

## Step 6 — Baseline Hardening (Minimal, Safe)

> Do **not** add users, clusters, or VMs yet.

1. Disable subscription nag (non-invasive)
2. Verify:
   - Time is correct
   - DNS resolves external hosts
   - No unexpected services running
3. Confirm management interface is on VLAN 10 only

---

## Step 7 — Validation Checklist

- [ ] Proxmox boots cleanly
- [ ] Web UI reachable from LAB
- [ ] Correct hostname and domain set
- [ ] Correct static IP assigned
- [ ] No impact to household network
- [ ] No services deployed yet

---

## Step 8 — Document and Close Out

1. Update:
   - `hardware/proxmox-host.md` with final specs
   - `logs/build-journal.md` (next BJ entry)
2. Commit and push documentation updates
3. Do **not** proceed to VM deployment in the same session

---

## Rollback (If Needed)

- Power off host
- Disconnect from switch
- Reclaim reserved IP if installation is abandoned
- No other systems affected

---

## Notes / Guardrails
- One infrastructure change per session
- No services until Phase 4.2 approval
- Treat Proxmox host as **infrastructure**, not a playground
- All credentials stored only after secure vault is live

---

## Next Runbook
**Runbook: Proxmox Network & Storage Baseline (Phase 4.2)**
