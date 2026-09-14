## CC-001 — Phase 4 Control Plane Foundation (Proxmox + Services)

**Date:** 2025-12-30  
**Change ID:** CC-001  
**Phase:** Phase 4 — Service Control Plane & Virtualization  
**Requested By:** Quan Watson  
**Role:** Homelab Owner / Systems Engineer  

---

### Change Summary
Establish the virtualization and control-plane foundation for the homelab by introducing a dedicated Proxmox host and defining the initial service architecture (CA, DNS, secrets management, and future AD/Odoo services).

This change formalizes the transition from **network-first buildout** to **service deployment readiness**.

---

### Scope
**In Scope:**
- Lock hardware specifications for Proxmox host
- Define Proxmox installation standards
- Establish VM naming conventions and layout
- Create runbooks for:
  - Proxmox install
  - Network & storage baseline
  - Internal CA
  - Internal DNS (hybrid)
  - Secrets / credential management
- Decide certificate strategy (Internal CA vs self-signed)

**Out of Scope (for this change):**
- Active Directory deployment
- Odoo production deployment
- User-facing services
- External exposure of services

---

### Risk Assessment
**Risk Level:** Low  

**Identified Risks:**
- Misconfiguration of Proxmox networking
- Overcommitment of resources without monitoring
- Certificate trust issues if CA design is rushed

**Mitigations:**
- One service per VM
- Documentation-first execution
- No production data hosted
- Console access maintained for recovery

---

### Impact
- **Household Connectivity:** None
- **Existing LAB VLAN (VLAN 10):** No changes
- **Switch / Firewall Config:** No changes during this phase
- **Downtime Expected:** None

---

### Rollback Plan
- Proxmox host can be powered down without affecting network
- No existing services depend on the new host
- Network remains unchanged if virtualization layer is removed

---

### Validation Criteria
- Proxmox installs successfully on designated hardware
- Management access confirmed on LAB VLAN
- No impact to existing lab devices
- Runbooks reviewed and approved before execution

---

### Status
☐ Planned  
☐ Approved  
☐ In Progress  
☑ Completed  
☐ Paused (Intentional checkpoint for documentation & review)

---

### Notes
This change intentionally pauses execution to ensure documentation quality, audit readiness, and professional presentation before public sharing.

## CC-002 — Proxmox Host Introduction (pve01)

**Date:** 2026-01-06  
**Change ID:** CC-002  
**Phase:** Phase 4 — Service Control Plane & Virtualization  
**Requested By:** Quan Watson  
**Role:** Homelab Owner / Systems Engineer  

---

### Change Summary
Introduce the first virtualization host (**Proxmox VE**) into the homelab to enable controlled deployment of core infrastructure services (CA, DNS, secrets management, and future directory services).

This change establishes the **execution layer** for Phase 4 while preserving all existing network and household connectivity.

---

### Installation Inputs (Locked Before Execution)

- **Hostname:** `pve01`  
- **Domain:** `corp.techtheworld.win`  
- **Management VLAN:** VLAN 10 (LAB)  
- **Management IP:** `192.168.10.104/24`  
- **Gateway:** `192.168.10.1`  
- **DNS Server:** `192.168.10.1` (pfSense — temporary)  
- **Time Zone:** CST  
- **Admin Email:** `admin@techtheworld.win`  

These values are treated as **authoritative** for the initial Proxmox deployment.

---

### Scope

**In Scope:**
- Deploy Proxmox VE on dedicated host (`pve01`)
- Bind Proxmox management interface to VLAN 10 (LAB)
- Reserve and document static management IP
- Establish Proxmox as the virtualization control plane
- Create placeholder documentation for:
  - Proxmox host hardware
  - Network addressing
  - Logical topology updates

**Out of Scope (for this change):**
- VM or container deployment
- Active Directory services
- Odoo production services
- Certificate Authority deployment
- External service exposure
- Backup system implementation (PBS)

---

### Documentation Updates Required (Pre-Execution)

- `hardware/proxmox-host.md`  
  - Lock hardware specifications
  - Define host role and intent

- `network/ip-plan.md`  
  - Reserve `192.168.10.104` for `pve01`
  - Annotate as virtualization management endpoint

- `topology.md`  
  - Logical update only (no physical network changes)
  - Add Proxmox host as control-plane node

> Execution must not begin until documentation placeholders exist.

---

### Risk Assessment

**Risk Level:** Low  

**Identified Risks:**
- Incorrect Proxmox network binding
- Accidental impact to LAB VLAN
- Misallocation of storage during install

**Mitigations:**
- VLAN 10 already validated and stable
- Switch port explicitly enabled and documented
- No changes to firewall or switch trunking
- Console access available for recovery
- Storage layout pre-designed and reviewed

---

### Impact

- **Household Connectivity:** None  
- **Existing LAB VLAN (VLAN 10):** No changes  
- **Switch Configuration:** No changes beyond access-port enablement  
- **Firewall Configuration:** No changes  
- **Downtime Expected:** None  

---

### Rollback Plan

- Power off Proxmox host
- Disable switch access port if needed
- No dependency from existing services
- Network remains fully operational without the host

---

### Validation Criteria

- Proxmox installs successfully on NVMe storage
- Management UI reachable at `https://192.168.10.104:8006`
- Host resolves `pve01.corp.techtheworld.win`
- No disruption to existing LAB devices
- Switch port remains stable under load

---

### Status

☐ Planned  
☐ Approved  
☐ In Progress  
☑ Completed  
☐ Paused (Intentional checkpoint before installation)

---

### Notes
This change explicitly separates **host introduction** from **service deployment**.  
VM creation, certificates, DNS, and identity services will be handled under subsequent change controls.
