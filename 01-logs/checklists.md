# Master Homelab Execution Checklist  
_Source of Truth — Phase-Gated from Foundation to Client-Ready Architecture_

This checklist represents the **authoritative execution state** of the homelab.
Items are only checked when **validated, documented, and stable**.

---

## Phase 0 — Foundations & Professional Discipline (COMPLETE)

**Objective:** Establish enterprise-grade habits before touching infrastructure.

- [x] Defined homelab purpose (career path: Network → Systems → Solutions Architect)
- [x] Adopted documentation-first methodology
- [x] Created GitHub repository as source of truth
- [x] Standardized canonical folder structure
- [x] Implemented logging taxonomy:
  - Build Journal (state changes)
  - Learning Log (understanding gained)
  - Session Notes (continuity)
  - Checklists (execution control)
- [x] Locked logging rules (what qualifies for each log)
- [x] Validated multi-device Git workflow
- [x] Resolved repository divergence and structural drift
- [x] Designated a single primary authoring machine

**Gate:** No infrastructure work permitted before this phase  
**Status:** ✅ COMPLETE

---

## Phase 1 — Firewall & Layer 3 Baseline (COMPLETE)

**Objective:** Establish deterministic routing and segmentation at Layer 3.

### Planning
- [x] Documented firewall role and topology
- [x] Defined LAN, WAN, and upstream NAT design
- [x] Designed VLAN segmentation plan prior to implementation

### pfSense Deployment
- [x] Installed pfSense on dedicated hardware
- [x] Configured WAN as DHCP client
- [x] Configured LAN with static gateway
- [x] Validated outbound connectivity (ICMP, DNS)
- [x] Disabled IPv6 intentionally (scope control)
- [x] Captured configuration backups

### VLAN Routing
- [x] Created VLAN 10 (LAB)
- [x] Assigned routed interface on pfSense
- [x] Enabled DHCP on VLAN 10
- [x] Applied baseline firewall rules
- [x] Deferred switch changes to isolate variables

**Gate:** VLAN 10 must route correctly before touching Layer 2  
**Status:** ✅ COMPLETE

---

## Phase 2 — Switching & Layer 2 Enforcement (COMPLETE)

**Objective:** Enforce VLAN segmentation and control broadcast domains.

### Switch Baseline
- [x] Reset Cisco Catalyst 3560 to known-good baseline
- [x] Verified console access
- [x] Identified IOS 12.2(35)SE IPBASE limitations

### Management Plane
- [x] Removed management dependency on VLAN 1
- [x] Placed switch management interface on VLAN 10
- [x] Obtained DHCP management IP (192.168.10.101)
- [x] Verified GUI access
- [x] Preserved console-only recovery path
- [x] Disabled HTTP services where possible
- [x] Prevented remote management exposure

### VLAN Enforcement
- [x] Configured trunk uplink to pfSense (Gi0/1)
  - [x] 802.1Q trunk
  - [x] Allowed VLANs: 10 only
  - [x] Native VLAN: 999
- [x] Configured LAB access port (Fa0/8)
- [x] Administratively disabled unused ports (Fa0/1–7)
- [x] Assigned disabled ports to VLAN 999
- [x] Verified STP forwarding state
- [x] Verified no VLAN leakage

**Gate:** End-to-end LAB connectivity required  
**Status:** ✅ COMPLETE

---

## Phase 3 — Switch Hardening & Failure Learning (COMPLETE)

**Objective:** Protect the access layer and validate failure modes.

### Planning
- [x] Scoped hardening to access ports only
- [x] Verified no trunk or management plane impact
- [x] Selected controls compatible with legacy IOS

### Hardening Controls
- [x] Enabled PortFast on access ports
- [x] Enabled BPDU Guard on access ports
- [x] Applied storm-control thresholds
- [x] Preserved trunk safety (no PortFast / BPDU Guard)
- [x] Preserved VLAN enforcement

### Validation & Learning
- [x] Triggered real-world storm-control err-disable
- [x] Diagnosed err-disabled port via console
- [x] Recovered port intentionally
- [x] Confirmed protections functioned as designed
- [x] Logged operational and learning impact

**Gate:** Hardening must fail safely without cascading outage  
**Status:** ✅ COMPLETE

---

## Phase 4 — Service Enablement & Virtualization

### Phase 4.1 — Domain & Certificate Strategy (COMPLETE)

**Objective:** Establish naming, trust, and certificate authority direction.

- [x] External domain confirmed: **techtheworld.win**
- [x] Internal AD domain defined: **corp.techtheworld.win**
- [x] Designed split-DNS strategy
- [x] Selected certificate model:
  - Internal services → Internal CA
  - External services → Cloudflare TLS
- [x] Created domain documentation structure
- [x] Drafted certificate strategy documentation

**Gate:** Naming and trust must be decided before services  
**Status:** ✅ COMPLETE

---

### Phase 4.2 — Proxmox Virtualization Platform

**Objective:** Prepare a stable service hosting layer.

#### Hardware Baseline
- [x] Identified dedicated Proxmox host
- [x] Validated hardware via UEFI diagnostics
- [x] Locked specifications:
  - Lenovo ThinkCentre M720s
  - Intel i5-9500 (6C / 6T)
  - 48 GB DDR4 RAM
  - NVMe boot disk
  - Dual 1 TB SATA HDDs
- [x] Confirmed virtualization support
- [x] Documented disk inventory

#### Planning
- [x] Defined Proxmox role in architecture
- [x] Designed VM separation of duties
- [x] Defined management VLAN usage (VLAN 10)
- [x] Created installation and recovery runbooks

#### Execution
- [ ] Install Proxmox VE
- [ ] Configure management networking
- [ ] Secure Proxmox UI
- [ ] Capture baseline snapshot

**Gate:** Proxmox must be stable before deploying services  
**Status:** 🟡 PLANNING COMPLETE — EXECUTION PENDING

---

## Phase 5 — Core Infrastructure Services (FUTURE)

- [ ] Deploy Internal Certificate Authority (VM)
- [ ] Deploy Internal DNS service
- [ ] Integrate DNS with AD namespace
- [ ] Implement time synchronization
- [ ] Harden inter-service trust

---

## Phase 6 — Identity & Directory Services (FUTURE)

- [ ] Deploy Active Directory
- [ ] Join internal services to domain
- [ ] Configure baseline GPOs
- [ ] Implement RBAC model

---

## Phase 7 — Control Plane & Documentation Services (FUTURE)

- [ ] Deploy Odoo (IT Glue–style control plane)
- [ ] Implement asset inventory
- [ ] Implement credential vaulting
- [ ] Map service dependencies
- [ ] Document operational workflows

---

## Phase 8 — Automation, Monitoring & AI (FUTURE)

- [ ] Deploy monitoring stack
- [ ] Configure alerting
- [ ] Implement automation workflows
- [ ] Deploy private AI services
- [ ] Document AI governance

---

## Phase 9 — Client-Ready Reference Architecture (FUTURE)

- [ ] Produce MSP-ready diagrams
- [ ] Define client hardware profiles
- [ ] Create onboarding playbooks
- [ ] Prepare portfolio artifacts
- [ ] Map homelab patterns to enterprise use cases

---

## Current Position

✔ Phase 0 — Complete  
✔ Phase 1 — Complete  
✔ Phase 2 — Complete  
✔ Phase 3 — Complete  
✔ Phase 4.1 — Complete  
🟡 Phase 4.2 — Ready for execution  

**Next authorized action:** Install Proxmox VE
