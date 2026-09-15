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

## 12-29-2025

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

**Status:** Phase 3 hardening plan approved (no changes applied)
**Next Step:** Apply access-port hardening controls and capture validation evidence (BJ-021)

## 12-30-2025

### BJ-021
**Change:** Phase 3 switch hardening validated (execution already completed)

**Notes:**  
- Confirmed Phase 3 access-layer hardening had already been executed prior to formal execution entry  
- Validated all controls against Cisco IOS 12.2(35)SE IPBASE constraints  
- No additional configuration changes applied during this session  

**Validated Controls:**  
- Access ports hardened only (no trunk impact)
  - `spanning-tree portfast` enabled on access ports
  - `bpduguard` enabled on access ports
  - Storm control applied with conservative thresholds
  - Err-disable behavior verified as expected on violation  
- Trunk interface (`Gi0/1`) preserved:
  - No PortFast
  - No BPDU Guard
  - VLAN enforcement unchanged (native VLAN 999, allowed VLAN 10 only)
- Management plane unchanged:
  - Console-only recovery access retained
  - VLAN 10 remains management VLAN
  - VLAN 1 remains unused
- No crypto, SSH, or HTTPS features attempted (platform limitation respected)

**Validation Evidence:**  
- `show interfaces trunk` confirms VLAN enforcement unchanged  
- `show spanning-tree summary` confirms PortFast active on edge ports only  
- Storm control verified on access interfaces  
- No err-disabled interfaces observed during normal operation  

**Impact:**  
- No service interruption  
- No topology changes  
- Switch hardening confirmed stable  

**Status:** Phase 3 (Switch Hardening) COMPLETE  
**Next Step:** Advance to Phase 4 — Service Enablement (Proxmox + Core Services)

## 12-30-2025

### BJ-022
**Change:** Storm-control enforcement validated via real traffic event

**Notes:**  
- Access port `Fa0/8` (LAB_ACCESS_OPTIPLEX) entered `err-disabled` state due to **storm-control**  
- Event triggered by sustained high-throughput traffic from a legitimate torrent download  
- Physical link lights disabled as expected upon err-disable condition  
- Confirmed switch behavior aligns with intended Phase 3 hardening design  

**Validation Evidence:**  
- `show interfaces status err-disabled` confirms:
  - Interface: `Fa0/8`
  - Reason: `storm-control`  
- `show errdisable recovery` confirms:
  - Storm-control recovery disabled by default  
  - Manual recovery required (as designed)  

**Response Actions:**  
- Port manually recovered using `shutdown / no shutdown`  
- Storm-control thresholds preserved (no relaxation applied)  
- No impact to trunk (`Gi0/1`), management VLAN, or other access ports  

**Impact:**  
- Single-port containment verified  
- No lateral impact across VLANs or switch fabric  
- Demonstrated effectiveness of access-layer protections under real-world load  

**Status:** Storm-control protection confirmed operational  
**Next Step:**  
- Decide whether to enable timed errdisable auto-recovery  
- Proceed to Phase 4: Proxmox host deployment and service enablement

## 12-30-2025

### BJ-023
**Change:** Phase 4.1 completed — Domain, DNS, and identity control plane locked

**Notes:**  
- Finalized domain architecture:
  - External domain: `techtheworld.win` (Cloudflare-managed)
  - Internal AD domain: `corp.techtheworld.win`
- Confirmed Cloudflare as authoritative external DNS provider
- Defined DNS responsibility boundaries:
  - Cloudflare → public records only
  - Internal DNS → AD-integrated, private resolution
- Established identity and trust design principles:
  - Windows Server to provide Active Directory and core identity services
  - Linux-first approach for internal services and platforms
- Selected certificate strategy:
  - **Internal Certificate Authority** as long-term trust model
  - Temporary self-signed certificates permitted only for early bootstrap
  - Centralized trust distribution planned for Windows and Linux systems
- Confirmed no compute or services deployed during this phase
- All decisions documented prior to Proxmox installation

**Impact:**  
- No infrastructure changes
- Control plane fully designed and documented
- Reduced future rework by locking identity, DNS, and trust strategy early

**Status:** Phase 4.1 COMPLETE  
**Next Step:** Begin Phase 4.2 — Compute substrate deployment (Proxmox installation and host networking)

## 01-06-2026

### BJ-024
**Change:** Re-tuned access port after repeat err-disable event (Fa0/8)

**Notes:**  
- **Fa0/8** entered an **err-disabled** state again during sustained, legitimate high-throughput traffic (legal torrenting + multiplayer gaming).
- This occurred after Phase 3 hardening, confirming that the previous storm-control and BPDU Guard settings were still too aggressive for this specific endpoint’s traffic profile.
- Event validated the effectiveness of hardening controls while also highlighting the need for **port-specific tuning**.

**Actions Taken:**  
- Manually recovered **Fa0/8** from err-disabled state  
- Further relaxed **storm-control thresholds** on Fa0/8 only  
- Disabled **BPDU Guard** on Fa0/8 only (retained on all other access ports)  
- Left PortFast behavior unchanged  
- Verified no changes were made to:
  - Trunk interface (`Gi0/1`)
  - Management plane
  - Other access ports
  - VLAN enforcement  

**Validation:**  
- Sustained torrent traffic verified without err-disable events  
- Concurrent gaming traffic verified stable  
- No broadcast storms or unintended traffic observed  
- Switch stability and management access confirmed  

**Impact:**  
- Endpoint stability restored under real-world load  
- Switch hardening posture preserved globally  
- No impact to LAB VLAN, trunk configuration, or household connectivity  

**Risk Assessment:**  
- Low risk  
- Change scoped to a single, known high-throughput endpoint  
- Fully reversible via console  

**Status:** Port stabilized after repeat event; configuration now aligned with real traffic patterns

### BJ-025
**Change:** Proxmox host introduced to LAB network (initial integration)

**Notes:**  
- Designated **Fa0/7** as the dedicated **hypervisor infrastructure access port** for the Proxmox host  
- Port 7 was previously **administratively disabled** as part of Phase 3 switch hardening  
- Intentionally re-enabled port 7 for controlled infrastructure use  
- Applied a **Hypervisor Port Profile** distinct from:
  - Standard access ports
  - High-throughput endpoint ports  

**Hypervisor Port Profile Applied (Fa0/7):**  
- Access mode, **VLAN 10 (LAB)**  
- `spanning-tree portfast` enabled  
- **BPDU Guard explicitly disabled** (hypervisor bridges generate BPDUs)  
- **Storm control removed** to prevent false-positive port shutdown during:
  - VM bridge initialization
  - Proxmox network configuration
- Port remains non-trunked (no VLAN tagging at switch level)

**Design Intent:**  
- Place Proxmox management and core infrastructure services on **VLAN 10** alongside:
  - Existing management plane
  - Control-plane services (Internal CA, DNS, Odoo, future AD)
- Preserve strict separation between:
  - Infrastructure ports (Fa0/7)
  - High-throughput endpoints (Fa0/8)
  - Disabled / unused ports (VLAN 999)

**Validation Evidence:**  
- Port 7 link restored intentionally after Phase 3 hardening  
- Initial port drops correlated to storm-control and BPDU guard behavior  
- Port stabilized after applying hypervisor-appropriate profile  
- No err-disable events observed after correction  
- No impact to:
  - Existing LAB endpoints
  - Switch management access
  - Firewall or VLAN enforcement  

**Impact:**  
- Introduces first infrastructure server into the LAB network  
- No impact to household network or existing endpoints  

**Status:** Proxmox host physically integrated and port stabilized  
**Next Step:** Install Proxmox VE and validate management access on VLAN 10

## 01-07-2026
### BJ-026
**Change:** Proxmox storage architecture finalized (clean OS vs service separation)

**Notes:**  
- Finalized and executed disk + partition strategy for Proxmox host **before any VM deployment**
- NVMe (238 GB) intentionally segmented:
  - **64 GB** allocated to Proxmox VE OS (hypervisor only)
  - Remaining NVMe capacity reserved exclusively for **core control-plane VMs and containers**
- Confirmed SATA HDD usage model:
  - **HDD 1 (1 TB):** Reserved for NAS VM backing storage (data-first workload)
  - **HDD 2 (1 TB):**
    - ~500 GB for VM OS disks (non-core / rebuildable workloads)
    - ~500 GB for VM data disks (non-core services)
- Storage decisions executed using Parted Magic to ensure:
  - Deterministic layout
  - Clean boundaries between OS, services, and data
- Explicitly avoided:
  - Monolithic root filesystem
  - Mixing hypervisor OS with service disks
  - Early VM creation before storage intent was locked

**Validation Evidence:**  
- Proxmox installed cleanly on 64 GB NVMe partition  
- Web UI stable and accessible on VLAN 10  
- NVMe remaining capacity visible and allocated for core datastore  
- HDD datastores visible and correctly separated by intent  
- No VMs or containers deployed prior to storage lock-in  

**Impact:**  
- No impact to existing LAB network or endpoints  
- Establishes a clean, auditable, enterprise-aligned virtualization foundation  

**Status:** Storage architecture locked and approved  
**Next Step:**  
- Snapshot baseline Proxmox state  
- Create logical network topology checkpoint (Packet Tracer)  
- Deploy first core VM (Internal CA)

## 01-14-2026
### BJ-027
**Change:** Clean Proxmox reinstall performed to enforce finalized storage architecture

**Notes:**  
- Performed intentional Proxmox VE reinstall after NVMe was fully reformatted
- Reinstall was required to:
  - Correct early LVM layout assumptions
  - Enforce clean separation between hypervisor OS and core service storage
  - Avoid retrofitting storage decisions post-deployment
- Reinstall executed *before* any VM or container creation
- Enterprise repository disabled; community repository enabled
- Host returned to a known-good, minimal baseline

**Validation Evidence:**  
- Proxmox boots cleanly with stable management access  
- Storage layout reflects documented intent exactly  
- No residual services, VMs, or legacy artifacts present  
- Host ready for service-layer deployment  

**Impact:**  
- No disruption to LAB network or endpoints  
- One-time corrective action to protect long-term maintainability  

**Status:** Completed  
**Next Step:**  
- Snapshot baseline state  
- Create current-state logical network topology (Packet Tracer)  
- Begin Phase 5 with Internal CA deployment

## BJ-028 (Draft)
Checkpoint reached — network + hypervisor stable.
Paused before service deployment pending topology commit.

## 09-14-2026
### BJ-029
**Change:** Repo integrated with the 36-month Solutions Architect + vCIO certification/training program; build status reconciled after an ~8-month pause

**Notes:**
- Last commit prior to this entry was dated 2026-01-15 (topology checkpoint referenced in BJ-027/BJ-028's Next Step). The build paused at that checkpoint — Phase 5 (Internal CA / service deployment) was not started.
- The certification/training program (tracked separately in `training-program/`) currently frames the homelab work as a fresh build starting September 2026. This entry exists to reconcile the two: the Phase 0–3 work documented above (BJ-001 through BJ-027) is real, completed, and stands as-is — it is not being discarded or redone from scratch. It is being resumed and extended, not restarted.
- Added new top-level folders to bring this repo in line with the training program: `training-program/`, `15-certifications/`, `16-career/`, `17-ots/`, `18-solutions-architecture-adrs/`, and `.vscode/` (editor settings/extensions only, no build changes).
- No changes made to any existing numbered folder's content in this entry — this is a structural/documentation addition only.

**Validation Evidence:**
- `git log` confirms last prior commit 2026-01-15
- No conflicts between historical build-journal entries and current plan; this entry is additive

**Impact:**
- No disruption to LAB network, endpoints, or prior documentation
- Clarifies repo status for anyone (including future employers/reviewers) reading the history in order

**Status:** Completed
**Next Step:**
- Resume from BJ-028's checkpoint: snapshot baseline state, create current-state logical network topology, begin Phase 5 with Internal CA deployment
- Keep `training-program/Training-Time-Log.md` and this journal in sync going forward — journal entries track the build, the time log tracks study/session hours

## 09-14-2026
### BJ-030
**Change:** Daily-driver OS rebuild (Dell OptiPlex, GTX 1060 6GB) — replaced both prior drives with a single 512GB M.2 NVMe, moved to single-OS Omarchy; Omarchy install in progress, currently blocked

**Notes:**
- Hardware change: removed both prior drives from the earlier dual-boot attempt (Kingston 240GB SATA SSD, Seagate `ST1000LM035-1RK1` 931.5GB SATA HDD). Installed one new 512GB M.2 NVMe drive as the sole drive, used whole-disk. This machine is now single-OS Omarchy — Windows dual-boot is retired from scope for this build.
- New M.2 drive was visible in BIOS but invisible to an Ubuntu live session (`lsblk`/`fdisk -l` returned nothing for it). Root cause: Intel VMD/RAID controller (`lspci` showed `00:17.0 RAID bus controller: Intel Corporation Device a386`). Fixed by switching the BIOS SATA/NVMe controller mode from RAID/VMD to AHCI.
- Ran `archinstall`: Btrfs with subvolumes and zstd compression, no LUKS, Limine bootloader, sudo-enabled user `ots1` created during setup.
- `ots1`'s sudo/login password was rejected after install. Fixed by logging in as `root` and running `passwd ots1`, resetting to an alphanumeric-only password to rule out a keyboard-layout mismatch on symbol characters.
- Ran the Omarchy installer (`curl -fsSL https://omarchy.org/install | bash`) logged in as `ots1`, not root, per the standing rule below. Hit a `linux-firmware-other` vs `linux-firmware-ti` package file conflict; fixed with `sudo pacman -Syu`.
- Installer then warned "Omarchy install requires: Limine bootloader." Diagnosed with `pacman -Q | grep limine` (empty), `cat /boot/limine.conf` (missing), and `efibootmgr -v` (showed `systemd-bootx64.efi`) — confirmed `archinstall` had actually installed systemd-boot, not Limine, despite Limine being the intended/selected choice.
- Redid `archinstall` from scratch, this time explicitly confirming Limine on the bootloader screen rather than accepting whatever was pre-highlighted.
- On the redo: user creation and the firmware conflict cleared cleanly again, the Omarchy repo cloned, package installs started — then hit a new blocker: `gum-2.0.1-1-x86_64.pkg.tar.zst` returns a 404 from `stable-mirror.omarchy.org`. Tried `sudo pacman -Syyu` (forced database refresh) — did not resolve it. **Unresolved as of session end.** Posted to the Omarchy Discord for help: "gum-2.0.1-1 404 error from stable-mirror.omarchy.org during install."
- Standing rule carried into this build: all post-install configuration is done logged in as the real user (`ots1`) using `sudo`, never as a root login shell — root-only config was the root cause of a prior attempt's graphical-login crash-loop (config landed in `/root` instead of `/home/ots1`).
- Full attempt-by-attempt history, troubleshooting table, and pending GPU driver/Hyprland steps are now tracked in `14-runbooks/runbook-omarchy-install.md` (added this entry) rather than duplicated here.

**Validation Evidence:**
- `lspci` confirmed the VMD root cause before the AHCI fix
- `pacman -Q | grep limine`, missing `/boot/limine.conf`, and `efibootmgr -v` confirmed the systemd-boot-vs-Limine mismatch before the `archinstall` redo
- Omarchy Discord post filed as the open item for the `gum` mirror 404

**Impact:**
- No impact to the LAB network, pfSense, or the rest of the homelab build — isolated to the standalone daily-driver/remote-workstation box
- Prior dual-boot framing for this machine is retired; treat it as single-OS Omarchy going forward

**Status:** In progress — paused, blocked on the `gum-2.0.1-1` 404 from `stable-mirror.omarchy.org`

**Next Step:**
- Resolve the `gum` mirror 404 (tracked via the Omarchy Discord post) and resume the Omarchy package install
- Once unblocked: GPU driver setup — `nvidia-dkms` (not `nvidia-open-dkms`, this is Pascal architecture), the four Hyprland env vars in `~/.config/hypr/envs.conf`, and the kernel param via `/etc/kernel/cmdline` + `sudo mkinitcpio -P`
- Re-verify and update `10-hardware/inventory/optiplex-3080.md` once the install completes
 