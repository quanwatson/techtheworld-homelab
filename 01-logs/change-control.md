## CC-001 — Phase 4 Control Plane Foundation (Proxmox + Services)

**Date:** 2025-01-XX  
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
☐ Completed  
☑ Paused (Intentional checkpoint for documentation & review)

---

### Notes
This change intentionally pauses execution to ensure documentation quality, audit readiness, and professional presentation before public sharing.
