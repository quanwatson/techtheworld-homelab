# Runbook: Proxmox Network & Storage Baseline

## Purpose
Establish deterministic **networking and storage baselines** on Proxmox **before** deploying any virtual machines or services.

This runbook enforces a clean separation between:
- Hypervisor installation
- Enterprise service deployment

No services are deployed during this runbook.

---

## Scope
- Proxmox VE host networking
- Linux bridge configuration
- VLAN alignment with pfSense + switchOTS
- Storage pool and content-type setup

---

## Preconditions (Do Not Skip)
- Proxmox installed successfully on bare metal
- LAB network (VLAN 10) stable and reachable
- Switch hardening complete (Phase 3)
- Console or direct access to Proxmox host
- No VMs or containers created yet

---

## Step 1 — Document Intended State (Change Control)
Update documentation **before** making changes:
- `network/topology.md`
- `network/vlan-plan.md`
- `compute/hypervisors.md`
- `compute/storage.md`

If intent is not documented, stop.

---

## Step 2 — Network Baseline (Management Plane)

### 2.1 Define Management Network
- VLAN: 10 (LAB)
- Gateway: 192.168.10.1
- DNS: pfSense (temporary)
- Proxmox IP: Static (documented)

### 2.2 Linux Bridge Design
| Bridge | Purpose | VLAN Aware |
|------|--------|------------|
| vmbr0 | Management + default VM traffic | Yes |
| vmbr1 | Future isolated workloads | Yes (future) |

Only `vmbr0` is created in this phase.

---

## Step 3 — Configure vmbr0

1. Proxmox Web UI → **Datacenter > Node > System > Network**
2. Verify physical NIC mapping
3. Configure:
   - Bridge Ports: physical NIC
   - IPv4: Static (LAB subnet)
   - VLAN aware: Enabled
4. Apply configuration

⚠️ Apply changes only when physically connected or with console access.

---

## Step 4 — Validate Network

- Ping default gateway
- Access Proxmox Web UI after reload
- Confirm no household connectivity impact

If validation fails:
- Revert network config immediately
- Use console recovery

---

## Step 5 — Storage Baseline

### 5.1 Local Storage Strategy
Choose **one**:
- ZFS (preferred if RAM allows)
- ext4 (acceptable for constrained systems)

### 5.2 Storage Content Types
Create logical separation:
- ISOs
- VM Disks
- Templates
- Backups

No mixed-purpose storage.

---

## Step 6 — Storage Validation
- Upload ISO
- Confirm storage visibility
- Confirm no VM creation yet

---

## Step 7 — Close Out
- Update Build Journal (Phase 4.3)
- Commit documentation
- Tag checkpoint

---

## Rollback
- Revert network config via console
- Restore previous storage assignment
- Do not proceed with VM deployment

---

## Notes / Guardrails
- One layer per session
- Hypervisor must be boring and predictable
- Services come later

