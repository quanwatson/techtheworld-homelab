# Master Homelab Execution Checklist
_Source of Truth — Phase 0 through Future Phases_

---

## Phase 0 — Foundations & Discipline (COMPLETED)

- [x] Defined homelab purpose (training for network / systems / solutions architect path)
- [x] Established documentation-first methodology
- [x] Created GitHub repository as authoritative source of truth
- [x] Standardized folder structure
- [x] Implemented logging taxonomy:
  - Build Journal
  - Learning Log
  - Session Notes
  - Checklists
- [x] Locked logging rules (what to log vs what not to log)
- [x] Verified multi-device Git workflow
- [x] Resolved repo divergence and structural drift
- [x] Designated primary authoring machine

**Phase 0 Status:** ✅ COMPLETE

---

## Phase 1 — Firewall & Layer 3 Baseline (COMPLETED)

### Planning
- [x] Documented firewall role and topology
- [x] Defined LAN, WAN, and upstream NAT design
- [x] Designed VLAN segmentation plan before implementation

### pfSense Deployment
- [x] Installed pfSense on dedicated hardware
- [x] Configured WAN as DHCP client
- [x] Configured LAN with static gateway
- [x] Validated outbound connectivity (DNS, ICMP)
- [x] Disabled IPv6 intentionally
- [x] Captured configuration backups

### VLAN Routing
- [x] Created VLAN 10 (LAB)
- [x] Assigned routed interface on pfSense
- [x] Enabled DHCP on VLAN 10
- [x] Applied baseline firewall rules
- [x] Deferred switch changes to isolate variables

**Phase 1 Status:** ✅ COMPLETE

---

## Phase 2 — Switching & Layer 2 Enforcement (COMPLETED)

### Switch Baseline
- [x] Reset Cisco Catalyst 3560 to baseline
- [x] Verified console access
- [x] Identified IOS 12.2(35)SE IPBASE limitations

### Management Plane
- [x] Moved switch management off VLAN 1
- [x] Placed management interface on VLAN 10
- [x] Obtained DHCP management IP (192.168.10.101)
- [x] Verified web GUI access
- [x] Verified console recovery path
- [x] Disabled HTTP services where possible
- [x] Restricted management to console only

### VLAN Enforcement
- [x] Configured trunk uplink to pfSense (Gi0/1)
  - [x] 802.1Q trunk
  - [x] Allowed VLANs: 10 only
  - [x] Native VLAN: 999
- [x] Configured access port for LAB workstation (Fa0/8)
- [x] Disabled unused access ports (Fa0/1–7)
- [x] Assigned disabled ports to VLAN 999
- [x] Validated STP forwarding state
- [x] Verified no VLAN leakage

**Phase 2 Status:** ✅ COMPLETE

---

## Phase 3 — Switch Hardening (COMPLETED)

### Planning
- [x] Scoped hardening to access ports only
- [x] Verified no impact to trunk or management plane
- [x] Selected controls compatible with IOS 12.2 IPBASE

### Hardening Controls
- [x] Enabled PortFast on access ports
- [x] Enabled BPDU Guard on access ports
- [x] Applied Storm Control thresholds
- [x] Verified err-disable behavior
- [x] Preserved trunk configuration (no PortFast / no BPDU Guard)
- [x] Preserved VLAN enforcement

### Validation
- [x] Observed real-world storm-control err-disable event
- [x] Diagnosed err-disabled interface via console
- [x] Recovered port intentionally
- [x] Confirmed safeguards function as designed
- [x] Documented learning and operational impact

**Phase 3 Status:** ✅ COMPLETE

---

## Phase 4 — Service Enablement & Virtualization (IN PROGRESS)

### Phase 4.1 — Domain & Certificate Strategy (COMPLETED)
- [x] External domain confirmed: **techtheworld.win**
- [x] Internal AD domain defined: **corp.techtheworld.win**
- [x] Designed split-DNS strategy
- [x] Selected certificate model:
  - Internal services → Internal CA
  - External services → Cloudflare TLS
- [x] Created domain documentation structure
- [x] Drafted certificate strategy documentation

**Phase 4.1 Status:** ✅ COMPLETE

---

### Phase 4.2 — Proxmox Platform (ACTIVE — PLANNING COMPLETE)

#### Hardware Baseline
- [x] Identified dedicated Proxmox host
- [x] Validated hardware via UEFI diagnostics
- [x] Locked hardware specs:
  - Lenovo ThinkCentre M720s
  - Intel i5-9500 (6C / 6T)
  - 48 GB DDR4 RAM
  - NVMe boot disk
  - Dual 1 TB SATA HDDs
- [x] Confirmed virtualization support
- [x] Documented disk inventory

#### Planning
- [x] Designed Proxmox role in architecture
- [x] Planned VM separation of duties
- [x] Defined management VLAN usage (VLAN 10)
- [x] Deferred installation pending checklist approval

#### Execution (NOT STARTED)
- [ ] Install Proxmox VE
- [ ] Configure Proxmox management networking
- [ ] Secure Proxmox UI
- [ ] Snapshot baseline state

**Phase 4.2 Status:** 🟡 PLANNING COMPLETE — EXECUTION PENDING

---

## Phase 5 — Core Infrastructure Services (FUTURE)

- [ ] Deploy Internal Certificate Authority (VM)
- [ ] Deploy Internal DNS service
- [ ] Integrate DNS with AD namespace
- [ ] Implement time synchronization strategy
- [ ] Harden service-to-service trust

---

## Phase 6 — Identity & Directory Services (FUTURE)

- [ ] Deploy Windows Server AD
- [ ] Join internal services to domain
- [ ] Configure GPO baseline
- [ ] Implement role-based access model

---

## Phase 7 — Control Plane & Documentation Services (FUTURE)

- [ ] Deploy Odoo (IT Glue–like internal control system)
- [ ] Configure asset inventory
- [ ] Configure credential vaulting
- [ ] Map services, hosts, and dependencies
- [ ] Document operational workflows

---

## Phase 8 — Automation, Monitoring & AI (FUTURE)

- [ ] Deploy monitoring stack
- [ ] Implement alerting
- [ ] Integrate automation workflows
- [ ] Deploy private local AI services
- [ ] Document AI governance model

---

## Phase 9 — Client-Ready Reference Architecture (FUTURE)

- [ ] Produce MSP-ready reference diagrams
- [ ] Define client hardware profiles
- [ ] Document onboarding playbooks
- [ ] Prepare portfolio artifacts
- [ ] Map homelab → enterprise translation

---

### Current Position
**✔ Phase 3 complete**  
**✔ Phase 4.1 complete**  
**🟡 Phase 4.2 planning complete**  
**➡️ Next action: Install Proxmox VE**

