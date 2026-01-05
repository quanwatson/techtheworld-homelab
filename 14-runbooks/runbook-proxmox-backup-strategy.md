# Runbook: Proxmox Backup Strategy (Local + PBS-Ready)

## Purpose
Define a **reliable, repeatable backup strategy** for Proxmox that:
- Protects critical VMs and configuration
- Works **before** PBS is deployed
- Scales cleanly **into PBS** later without redesign
- Mirrors real MSP / enterprise practices

This runbook establishes **backup intent and execution rules**, not just tooling.

---

## Scope
- Proxmox VE host backups
- VM and container backups
- Configuration backups
- Local backup storage (Phase 4.2)
- PBS integration readiness (Phase 4.3+)

---

## Backup Philosophy (Locked)

1. **Backups are useless unless tested**
2. **Config backups matter as much as VM disks**
3. **One local copy minimum**
4. **Off-host storage preferred**
5. **Immutable backups when possible**
6. **No backups without documentation**

---

## Backup Targets (What Gets Backed Up)

### Tier 0 — Platform (Highest Priority)
- Proxmox host configuration:
  - `/etc/pve`
  - Network config
  - Storage config
- Backup before:
  - Proxmox upgrades
  - Network changes
  - Storage changes

### Tier 1 — Core Services
- Internal CA
- DNS
- Odoo control plane
- Future AD / Identity services

### Tier 2 — Supporting Services
- Monitoring
- Automation
- Internal tools

### Tier 3 — Lab / Experimental
- Disposable VMs
- Test workloads
- Training sandboxes

> Tier 3 may have reduced retention.

---

## Phase 4.2 — Local Backup Strategy (Now)

### Storage Design

**Primary backup target:**
- Dedicated backup disk on Proxmox host
- Mounted as:
  - `local-backup`
- Filesystem:
  - ext4 or xfs (simple, stable)
- Mounted outside VM storage pools

> Backups must NOT share the same disk as VM storage.

---

## Proxmox Backup Configuration (Local)

### Backup Schedule
- **Daily**: Core services (Tier 0–1)
- **Weekly**: Tier 2 services
- **Optional**: Tier 3 on demand

### Backup Mode
- `snapshot` for VMs with QEMU agent
- `stop` only if snapshot fails

### Compression
- `zstd` (balanced speed + compression)

### Notification
- Email alerts (when mail relay exists)
- Manual log review until then

---

## Retention Policy (Local)

| Tier | Daily | Weekly | Monthly |
|----|------|--------|---------|
| Tier 0 | 7 | 4 | 3 |
| Tier 1 | 7 | 4 | 2 |
| Tier 2 | 5 | 2 | 0 |
| Tier 3 | 2 | 0 | 0 |

---

## Validation Procedure (Required)

After first backup run:

1. Confirm backups exist:
   - Proxmox UI → Datacenter → Backups
2. Verify size and timestamp
3. Perform **test restore**:
   - Restore VM to new VM ID
   - Boot and verify service
4. Document validation in:
   - Session Notes
   - Build Journal (only once per tier)

> A backup is not “working” until restored.

---

## Phase 4.3 — PBS Readiness (Future)

This design intentionally mirrors PBS behavior.

### PBS Benefits (When Deployed)
- Deduplication
- Encryption at rest
- Immutable backups
- Faster restores
- Multi-node scaling

### Migration Path
1. Deploy PBS VM
2. Add PBS datastore
3. Disable local jobs gradually
4. Retain one local copy as fast-restore tier

No VM changes required.

---

## Security Considerations
- Backup storage treated as **sensitive**
- No direct user access
- No SMB/NFS exposure to desktops
- Future: encryption keys stored in secrets manager

---

## Change Control
Any of the following requires documentation:
- Backup target change
- Retention change
- Schedule change
- Restore failure

---

## Rollback
- If backups fail:
  - Disable job
  - Preserve last known-good backup
  - Investigate logs before retry

---

## Status
**Phase 4.2 Backup Strategy: DEFINED**  
**Execution:** Pending storage confirmation  
**Next Runbook:** Proxmox Backup Server Deployment
