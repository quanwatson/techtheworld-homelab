# Build Journal

## 12-19-2025

### BJ-001
**Change:** Documentation repository initialized  
**Notes:**  
Initialized homelab repository using a documentation-first approach. Established Git-based version control before making any infrastructure changes to ensure traceability and rollback capability from day one.

**Status:** Baseline documentation environment created

---

### BJ-002
**Change:** Network design documentation completed  
**Notes:**  
Documented initial network architecture, including home vs lab segmentation strategy, IP addressing scheme, and pfSense firewall placement. Design decisions were recorded prior to hardware deployment to reduce configuration drift.

**Status:** Network design approved

---

### BJ-003
**Change:** Packet Tracer validation deferred  
**Notes:**  
Cisco NetAcad service outage prevented Packet Tracer access. Decision made to proceed with documentation-driven design and defer simulation until tooling access is restored.

**Status:** Deferred, no impact to build sequence

---

### BJ-004
**Change:** pfSense deployment planned and documented  
**Notes:**  
Defined pfSense role, interface mapping, installation checklist, and rollback strategy. Planning emphasized minimizing risk to the existing home network during initial firewall insertion.

**Status:** Approved for installation

---

### BJ-005
**Change:** Documentation-first phase completed  
**Notes:**  
- Repository structure finalized  
- Network and firewall plans committed and pushed  
- No hardware or network changes made prior to documentation lock  

**Status:** Cleared to proceed with controlled firewall deployment

---

## 12-20-2025

### BJ-006
**Change:** pfSense installed and staged on bare metal  
**Notes:**  
Installed pfSense CE 2.8.1 on dedicated firewall hardware. Initial setup performed in an isolated state. Temporary WAN connectivity used only for first-run validation, then stabilized.

**Status:** Firewall installed, not yet segmented

---

### BJ-007
**Change:** pfSense baseline configuration validated  
**Notes:**  
- Filesystem: UFS selected due to 2 GB RAM constraint  
- WAN configured as DHCP client and verified operational  
- LAN configured as `192.168.1.1/24` with DHCP enabled  
- Outbound connectivity validated via ICMP and DNS  
- IPv6 services intentionally disabled to maintain IPv4-only lab simplicity  
- Configuration backups captured for rollback  

**Status:** Firewall baseline stable

---

### BJ-008
**Change:** Canonical repository structure published  
**Notes:**  
- Identified folder structure inconsistencies across devices  
- Confirmed Git behavior regarding empty directories  
- Added `.gitkeep` placeholders to enforce directory tracking  
- Published GitHub repository as the authoritative source  
- Designated Dell OptiPlex 3080 as primary authoring system  

**Status:** Repository structure locked

---

### BJ-009
**Change:** pfSense internal architecture documented and locked  
**Notes:**  
- Renamed interfaces to functional identifiers (`WAN_UPSTREAM`, `LAN_CORE`)  
- Verified LAN DHCP and default firewall policy behavior  
- Confirmed intentional double-NAT with upstream gateway `192.168.68.1`  
- Documented current topology as a stable baseline  
- Designed VLAN segmentation plan (LAB, IOT, MGMT) without applying changes  

**Status:** Architecture documented, no segmentation applied yet

---

### BJ-010
**Change:** VLAN 10 (LAB) implemented on pfSense  
**Notes:**  
- Created VLAN 10 on `LAN_CORE`  
- Assigned routed interface `LAB_VLAN10`  
- Configured gateway `192.168.10.1/24`  
- Enabled DHCP for VLAN 10  
- Applied initial outbound allow rule  
- Deferred switch configuration to isolate variables  

**Status:** VLAN 10 operational at Layer 3

---

## 12-21-2025

### BJ-011
**Change:** Network documentation artifacts added  
**Notes:**  
- Updated `network/topology.md` to reflect segmented design  
- Created `network/vlan-plan.md` as VLAN source of truth  
- Established VLAN 10 as the reference implementation pattern  
- Explicitly deferred switch-side changes  

**Status:** Documentation aligned with live firewall state

---

### BJ-012
**Change:** Repository workflow standardized  
**Notes:**  
- Added Git workflow playbook  
- Defined standard session flow (status → stage → commit → push)  
- Established commit message conventions  
- Locked logging discipline rules  

**Status:** Workflow standardized

---

### BJ-013
**Change:** Build roadmap re-anchored  
**Notes:**  
- Confirmed active phase: **Switch Integration**  
- Defined clear Definition of Done for switch phase  
- Locked rule: no additional VLANs until VLAN 10 is validated end-to-end  

**Status:** Roadmap stabilized

---

## 12-22-2025

### BJ-014
**Change:** Git repository recovered after relocation  
**Notes:**  
- Repository directory moved, resulting in loss of `.git` metadata  
- Reinitialized Git and reattached to existing GitHub remote  
- Resolved authentication via fine-grained GitHub PAT  
- Reconciled divergent histories using `--allow-unrelated-histories`  
- Confirmed `main` branch tracking `origin/main`  

**Status:** Repository fully operational

---

### BJ-015
**Change:** Documentation and control-plane baseline locked  
**Notes:**  
- Finalized Network Playbook lifecycle (Design → Implement → Validate → Document → Promote)  
- Standardized role-specific and platform command libraries  
- Confirmed documentation readiness prior to switch-side changes  

**Status:** Cleared for Layer 2 enforcement

---

### BJ-016
**Change:** Switch management interface established  
**Notes:**  
- Cisco Catalyst 3560 (`switchOTS`) reset to baseline  
- Management moved to VLAN 10  
- DHCP-assigned management IP: `192.168.10.101`  
- Console and web GUI access verified  
- VLAN 1 management intentionally disabled  

**Status:** Switch Phase 1 complete  
**Next Step:** Secure management plane (SSH, users) and begin VLAN port enforcement

## 12-23-2025

### BJ-017 
**Change:** Documentation and governance baseline locked  

**Notes:**  
- Finalized repository-wide documentation structure  
- Standardized security, networking, firewall, and validation artifacts  
- Resolved all outstanding merge conflicts in core documentation  
- Established README as authoritative navigation guide for reviewers  
- Confirmed documentation accurately reflects current lab state (home-based, pfSense + VLAN 10 active)  

**Impact:**  
- No infrastructure changes  
- Documentation now serves as the control plane for future lab work  

**Status:** Baseline locked  
**Next Step:** Resume physical switch configuration and VLAN enforcement (Phase 3)

## 12-23-2025

### BJ-018
**Change:** Switch management plane secured under legacy IOS constraints  

**Notes:**  
- Cisco Catalyst 3560-8PC reset and integrated into LAB network  
- Management interface reachable on VLAN 10 (LAB) with DHCP-assigned IP `192.168.10.101`  
- Confirmed IOS 12.2(35)SE IPBASE image lacks crypto support (no SSH / HTTPS / RSA)  
- HTTP management server explicitly disabled  
- VTY access locked down to prevent Telnet exposure  
- Management access limited to physical console only  

**Impact:**  
- No production services affected  
- Switch management hardened within platform limitations  

**Status:** Management plane stabilized and secured  
**Next Step:** Finalize port roles, disable unused interfaces, and prepare MGMT VLAN (VLAN 30)

## 12-23-2025

### BJ-019  
**Change:** Layer 2 VLAN enforcement validated (LAB baseline)

**Notes:**  
- Confirmed **VLAN 10 (LAB)** as active management + lab device network  
- Verified switch management strategy:
  - Management isolated to **VLAN 10**
  - **VLAN 1 not used** for management
  - **VLAN 999 designated as native / disabled-port VLAN**
  - Console retained as out-of-band recovery path  
- Validated trunk and access configuration:
  - `Gi0/1` configured as **802.1Q trunk**
    - Allowed VLANs: **10**
    - Native VLAN: **999**
  - `Fa0/8` configured as **access VLAN 10**
    - Connected device: **OptiPlex 3080 (LAB workstation)**
  - `Fa0/1–7` administratively **shutdown** and assigned to **VLAN 999**  
- Confirmed end-to-end LAB connectivity:
  - OptiPlex received IP `192.168.10.100/24`
  - Default gateway `192.168.10.1` (pfSense LAB interface)
  - Switch management IP reachable at `192.168.10.101`
- Verified no unintended inter-VLAN access
- No additional VLANs activated beyond VLAN 10 (per roadmap lock)

**Validation Evidence:**  
- `show interfaces trunk` confirms:
  - Native VLAN: 999
  - Allowed VLANs: 10  
- `show ip interface brief` confirms:
  - VLAN 1 unassigned
  - Management reachable via VLAN 10  
- Client IP configuration confirms correct LAB addressing and gateway

**Impact:**  
- LAB network now enforced at Layer 2  
- Management plane isolated from default VLANs  
- Reduced attack surface by disabling unused switch ports  

**Status:** LAB VLAN enforcement complete and stable  
**Next Step:**  
- Disable unused trunk VLANs explicitly  
- Prepare **MGMT VLAN (VLAN 30)** design (no deployment yet)  
- Begin Phase 3: switch hardening + port role documentation

## 12-23-2025

### BJ-020
**Change:** Phase 3 switch hardening planned (access-layer protections)

**Notes:**  
- Reviewed current switch state to confirm:
  - VLAN 10 (LAB) is enforced and stable
  - Management plane isolated and secured
  - Trunk configuration locked and validated
- Identified Phase 3 hardening scope limited to **access ports only**
- Selected hardening controls compatible with **IOS 12.2(35)SE IPBASE**:
  - BPDU Guard on endpoint-facing ports
  - Storm Control with conservative thresholds
  - Explicit interface documentation
- Confirmed no overlap with previously completed actions:
  - VLAN enforcement completed under BJ-019
  - Management plane controls completed under BJ-018
- Confirmed no SSH, HTTPS, or crypto-based controls available on platform

**Planned Controls:**  
- Enable `spanning-tree portfast` and `bpduguard` on access ports  
- Apply storm-control limits for broadcast, multicast, and unicast traffic  
- Preserve trunk (`Gi0/1`) and management VLAN configuration unchanged  
- Maintain console-only access as recovery path  

**Risk Assessment:**  
- Low risk (access-port scoped)  
- No expected impact to LAB connectivity or management plane  
- Changes fully reversible via console  

**Status:** Phase 3 hardening approved, execution pending  
**Next Step:** Apply access-layer hardening to LAB access ports and validate behavior
git