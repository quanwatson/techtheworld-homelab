# Security Validation Checklist (Per Phase)

This checklist is used to validate security posture as the homelab evolves through
its lifecycle. Each phase builds on the previous one.

A phase is considered **complete only when all applicable checks pass**.
Items that are not yet applicable should remain unchecked until implemented.

---

## Phase 1 — Baseline Network & Isolation (Active)

**Objective:** Ensure the lab is safely isolated from the home network and
internet exposure is controlled.

### Network Isolation
- [x] Lab traffic is isolated from the home network by a firewall boundary
- [x] Double NAT is intentional and documented
- [x] No inbound access from the internet to internal lab networks
- [x] Default deny behavior exists at the perimeter

### Firewall & Routing
- [x] Outbound internet access is explicitly allowed
- [x] No implicit inbound rules exist
- [x] Firewall configuration is backed up or documented

### Validation Evidence
- [x] Topology documented in `network/topology.md`
- [x] Build Journal entry recorded for baseline isolation

---

## Phase 2 — Network Segmentation & Trust Zones (Partially Active)

**Objective:** Establish explicit trust boundaries using VLANs and firewall policy.

### VLAN Architecture
- [x] VLANs are defined with clear purpose and risk level
- [x] IP subnets do not overlap
- [x] Default deny exists between VLANs
- [ ] Multiple internal VLANs implemented (beyond LAB)

### Inter-VLAN Controls
- [x] Inter-VLAN traffic requires explicit firewall rules
- [x] No “any-to-any” rules between internal VLANs
- [ ] Justification exists for every allowed inter-VLAN flow

### Trust-Zone Validation
- [x] Trust-zone matrix is defined and reviewed
- [ ] IOT VLAN has no access to MGMT or LAB (not yet implemented)
- [ ] MGMT VLAN access is tightly restricted (not yet implemented)

### Validation Evidence
- [x] VLAN plan updated in `network/vlan-plan.md`
- [x] Trust-zone model documented in `security/segmentation.md`

---

## Phase 3 — Switching & Layer 2 Integration (In Progress)

**Objective:** Ensure segmentation is preserved at the switch level.

### Switch Configuration
- [x] Managed switch identified and documented
- [ ] Trunk ports explicitly defined and documented
- [ ] Access ports assigned to correct VLANs
- [ ] No unused ports left active

### Layer 2 Security
- [ ] No VLAN hopping paths exist
- [ ] Management interfaces are not exposed to user VLANs
- [ ] Switch management access restricted to MGMT VLAN (planned)

### Validation Evidence
- [ ] Port maps documented in `network/switching/port-maps.md`
- [x] Switch overview documented with VLAN strategy

---

## Phase 4 — Compute & Virtualization Platform (Not Yet Active)

**Objective:** Ensure compute resources do not weaken network or access controls.

### Host Security
- [ ] Host OS hardened with baseline settings
- [ ] Management interfaces restricted to MGMT VLAN
- [ ] Unused services disabled

### VM & Container Isolation
- [ ] Workloads placed in appropriate VLANs
- [ ] No VM has unnecessary access to MGMT
- [ ] Resource limits defined to prevent abuse

### Validation Evidence
- [ ] Host records updated in `hardware/inventory/`
- [ ] VM inventory updated in `compute/vms/vm-inventory.md`

---

## Phase 5 — Core Services & Platform Enablement (Planned)

**Objective:** Ensure foundational services are secure, observable, and recoverable.

### Identity & Infrastructure
- [ ] DNS is authoritative and consistent
- [ ] DHCP scopes align with VLAN design
- [ ] Directory services are isolated and protected

### Observability
- [ ] Monitoring enabled for critical services
- [ ] Logs are centralized or reviewable
- [ ] Alerting exists for failures or anomalies

### Resilience
- [ ] Backups configured for critical services
- [ ] Restore procedures documented (minimum viable)

### Validation Evidence
- [ ] Service records created in `services/`
- [ ] Backup and monitoring notes documented

---

## Phase 6 — Identity, Security & Access Control (Planned)

**Objective:** Enforce identity-aware access and reduce implicit privilege.

### Identity Controls
- [ ] Administrative access requires authenticated identity
- [ ] Privileged accounts are limited and documented
- [ ] Service accounts follow least privilege

### Access Enforcement
- [ ] MGMT access restricted to approved identities
- [ ] No shared admin credentials
- [ ] Remote access requires authentication and encryption

### Logging & Audit
- [ ] Authentication events logged
- [ ] Administrative actions reviewable

### Validation Evidence
- [ ] Identity model documented in `access/`
- [ ] Security model reviewed in `security/architecture.md`

---

## Phase 7 — Service Lifecycle & Environment Promotion (Planned)

**Objective:** Ensure services are safe to promote beyond experimentation.

### Promotion Readiness
- [ ] Service purpose clearly defined
- [ ] Security boundaries reviewed
- [ ] Firewall rules documented
- [ ] Monitoring enabled
- [ ] Backup strategy exists

### Change Discipline
- [ ] Rollback plan documented
- [ ] Change recorded in Build Journal
- [ ] No undocumented configuration changes

### Validation Evidence
- [ ] Service lifecycle documented in `services/`
- [ ] Change logged in `logs/build-journal.md`

---

## Phase 8 — Advanced Workloads & Optimization (Planned)

**Objective:** Ensure high-performance workloads do not bypass controls.

### GPU & Remote Workstation
- [ ] GPU access restricted to approved users
- [ ] Remote workstation requires secure entry
- [ ] No direct exposure of GPU hosts to untrusted networks

### Performance vs Security
- [ ] Firewall rules reviewed for least privilege
- [ ] Logging preserved despite performance tuning

### Validation Evidence
- [ ] GPU workflow documented in `compute/gpu/`
- [ ] Remote access documented in `services/remote-access/`

---

## Phase 9 — Continuous Improvement & Expansion (Ongoing)

**Objective:** Maintain security posture as the lab evolves.

### Ongoing Validation
- [ ] New hardware added to inventory
- [ ] New services documented before exposure
- [ ] Trust-zone model reviewed after changes

### Security Hygiene
- [ ] Periodic firewall rule review performed
- [ ] Obsolete services removed
- [ ] Documentation kept current

### Validation Evidence
- [ ] Logs reflect lab evolution
- [ ] Architecture documents updated as needed
