# Build Journal

## 20251219

### 20251219001
**Change:** Documentation repository initialized  
**Notes:** Began homelab project using a documentation-first methodology. Established Git-based change tracking prior to any infrastructure changes.

---

### 20251219002
**Change:** Network design documentation completed  
**Notes:** Defined home vs homelab segmentation strategy, IP addressing plan, and pfSense firewall placement prior to hardware deployment.

---

### 20251219003
**Change:** Packet Tracer validation deferred  
**Notes:** Cisco NetAcad maintenance prevented Packet Tracer login. Proceeded with documentation-first design. Simulation to be completed once service availability is restored.

---

### 20251219004
**Change:** pfSense deployment planned and documented  
**Notes:** Defined firewall role, interface assignments, installation safety checklist, and rollback strategy prior to installation to prevent home network disruption.

---

### 20251219005
**Change:** Documentation-first phase completed and validated  
**Notes:** 
- Git repository initialized and structured
- Network design and pfSense planning fully documented
- All changes committed and pushed to GitHub
- Environment confirmed clean prior to any hardware or network changes

**Status:** Approved to proceed with controlled pfSense installation (Step 4)

---

## 20251220

### 20251220001
**Change:** pfSense installed and staged on bare metal  
**Notes:** pfSense CE 2.8.1 installed on dedicated firewall appliance. Initial installation performed in isolated state. Temporary WAN connection used only to satisfy first-run connectivity checks, then validated and stabilized.

---

### 20251220002
**Change:** pfSense configuration validated and baseline established  
**Notes:** 
- Filesystem selected: UFS (due to 2 GB RAM constraint)
- WAN configured as DHCP client and verified UP
- LAN configured at 192.168.1.1/24 with DHCP enabled
- Outbound connectivity validated:
  - ICMP to public IP (8.8.8.8): SUCCESS
  - DNS resolution (google.com): SUCCESS
- IPv6 services intentionally disabled:
  - DHCPv6 Server disabled
  - Router Advertisements disabled
- Rationale: IPv4-only lab for stability and foundational learning
- Configuration backups saved for rollback

**Status:** Step 4 complete and stable  
**Next Step:** Network structuring and segmentation (VLANs, topology)

## 20251220008

**Date:** 2025-12-20  
**Change:** Canonical repository structure established and published  
**Notes:**  
- Identified structural divergence between development devices and GitHub  
- Confirmed Git does not track empty directories  
- Added `.gitkeep` placeholders to all structural folders to enforce tracking  
- Published full directory taxonomy to GitHub as the authoritative state  
- Designated Dell OptiPlex 3080 as the primary authoring and execution device  
- Established GitHub as the single source of truth for all environments  

**Status:** Repository structure stabilized  
**Next Step:** Begin content population via playbooks and runbooks

## 20251220009

**Date:** 2025-12-20  
**Change:** pfSense internal network architecture documented and baseline locked  
**Notes:**  
- Renamed pfSense interfaces to reflect functional roles (`WAN_UPSTREAM`, `LAN_CORE`)  
- Verified LAN DHCP configuration and default firewall behavior  
- Confirmed intentional double-NAT topology with upstream gateway `192.168.68.1`  
- Documented current network topology as a stable baseline state  
- Designed initial VLAN segmentation plan (LAB, IOT, MGMT) without applying configuration  
- Preserved system stability by deferring segmentation until planning was complete  

**Status:** Internal architecture stabilized and documented  
**Next Step:** Implement VLAN segmentation starting with VLAN 10 (LAB)

## 20251220010

**Date:** 2025-12-20  
**Change:** Implemented first VLAN (VLAN 10 – LAB) on pfSense  
**Notes:**  
- Created VLAN 10 on `LAN_CORE` as the parent interface  
- Assigned VLAN 10 as a routed interface (`LAB_VLAN10`)  
- Configured static gateway `192.168.10.1/24`  
- Enabled DHCP scope for VLAN 10  
- Applied initial firewall rule allowing outbound traffic  
- Deferred switch-side VLAN configuration pending validation  

**Status:** VLAN 10 routed and operational at the firewall layer  
**Next Step:** Attach VLAN 10 to a switch port and validate client connectivity

<<<<<<< HEAD
## 20251221011

**Date:** 2025-12-21  
**Change:** Added network documentation artifacts (Topology + VLAN Plan)  

**Notes:**  
- Updated `network/topology.md` to reflect segmented design  
- Created `network/vlan-plan.md` as a VLAN source-of-truth  
- Established VLAN 10 as the reference implementation pattern  
- Explicitly deferred switch configuration to avoid multi-variable troubleshooting  

**Status:** Network documentation aligned with live pfSense state  
**Next Step:** Proceed with managed switch integration (STEP 7)

## 20251221012

**Date:** 2025-12-21  
**Change:** Introduced standardized Git / repo workflow playbook  

**Notes:**  
- Added `playbooks/repo-workflow-playbook.md`  
- Standardized session flow (status → stage → commit → push)  
- Defined when to stage everything vs selectively stage  
- Established commit message conventions  
- Locked logging discipline rules  

**Status:** Repo workflow standardized across devices  
**Next Step:** Apply workflow consistently for all future sessions

## 20251221013

**Date:** 2025-12-21  
**Change:** Re-anchored homelab build steps to prevent step drift  

**Notes:**  
- Confirmed current active step: **STEP 7 — Switch Integration**  
- Clarified Definition of Done for STEP 7  
- Locked rule: no new VLANs or switch tagging until VLAN 10 validation completes  

**Status:** Build roadmap stabilized  
**Next Step:** Execute switch VLAN tagging and port assignment

## 20251222001

**Date:** 2025-12-22  
**Change:** Restored Git tracking after repo relocation and reconciled remote history  
**Notes:**  
- Local homelab repository was moved, resulting in loss of `.git` metadata  
- Re-initialized Git repository and reattached to existing GitHub remote  
- Resolved authentication using fine-grained GitHub PAT (org-scoped)  
- Identified non-fast-forward rejection due to divergent histories  
- Successfully reconciled local and remote histories using `--allow-unrelated-histories`  
- Confirmed local `main` branch now tracks `origin/main`  

**Status:** Repository fully synchronized and operational  
**Next Step:** Resume normal documentation and lab progression

## 2025-12-22 — Documentation & Control Plane Baseline Locked

**Change Type:** Architecture / Documentation Baseline  
**Scope:** Repository, Network Playbook, Command Libraries  

**Summary:**  
Finalized and locked the foundational documentation and control structure for the homelab prior to switch integration. Network Playbook, Role-Specific Command Library, and Windows/Linux Command Library were completed and aligned to the existing repo hierarchy.

**Key Outcomes:**
- Network Playbook established as authoritative lifecycle guide (Design → Implement → Validate → Document → Promote)
- Role-specific and platform command libraries standardized for copy/paste operational use
- Git repository re-initialized and successfully reconnected after directory relocation
- Authentication and ownership corrected to personal GitHub account
- Confirmed readiness for switch-side VLAN integration (next phase)

**Risk / Impact:**  
None. No production services impacted.

**Next Phase:**  
Switch integration and VLAN enforcement at Layer 2.



=======
>>>>>>> 859a8c1c8a4ec77b44982bcfa30bf217c7da3eed
