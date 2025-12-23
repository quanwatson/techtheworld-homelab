# Security Validation Checklist (Per Phase)

This checklist is used to validate security posture as the lab evolves through its lifecycle.
Each phase builds on the previous one. A phase is considered **complete only when all applicable checks pass**.

---

## Phase 1 — Baseline Network & Isolation

**Objective:** Ensure the lab is safely isolated from the home network and internet exposure is controlled.

### Network Isolation
- [ ] Lab traffic is isolated from the home network by a firewall boundary
- [ ] Double NAT is intentional and documented
- [ ] No inbound access from the internet to internal lab networks
- [ ] Default deny rules exist at the perimeter

### Firewall & Routing
- [ ] Outbound internet access is explicitly allowed
- [ ] No implicit inbound rules exist
- [ ] Firewall configuration is backed up or documented

### Validation Evidence
- [ ] Topology documented in `network/topology.md`
- [ ] Build journal entry recorded for baseline isolation

---

## Phase 2 — Network Segmentation & Trust Zones

**Objective:** Establish explicit trust boundaries using VLANs and firewall policy.

### VLAN Architecture
- [ ] VLANs are defined with clear purpose and risk level
- [ ] IP subnets do not overlap
- [ ] Default deny exists between VLANs

### Inter-VLAN Controls
- [ ] All inter-VLAN traffic requires explicit firewall rules
- [ ] No “any-to-any” rules between internal VLANs
- [ ] Justification exists for every allowed flow

### Trust-Zone Validation
- [ ] Trust-zone matrix is defined and reviewed
- [ ] IOT VLAN has no access to MGMT or LAB
- [ ] MGMT VLAN access is tightly restricted

### Validation Evidence
- [ ] VLAN plan updated in `network/vlan-plan.md`
- [ ] Trust-zone matrix updated in `security/segmentation.md`

---

## Phase 3 — Switching & Layer 2 Integration

**Objective:** Ensure segmentation is preserved at the switch level.

### Switch Configuration
- [ ] Trunk ports explicitly defined and documented
- [ ] Access ports assigned to correct VLANs
- [ ] No unused ports left active

### Layer 2 Security
- [ ] No VLAN hopping paths exist
- [ ] Management interfaces are not exposed to user VLANs
- [ ] Switch management access restricted to MGMT VLAN

### Validation Evidence
- [ ] Port maps documented in `network/switching/port-maps.md`
- [ ] Switch overview updated with VLAN strategy

---

## Phase 4 — Compute & Virtualization Platform

**Objective:** Ensure compute resources do not weaken network or access controls.

### Host Security
- [ ] Host OS hardened (baseline settings applied)
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

## Phase 5 — Core Services & Platform Enablement

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
- [ ] Backups are configured for critical services
- [ ] Restore procedure documented (at least conceptually)

### Validation Evidence
- [ ] Service records created in `services/`
- [ ] Backup and monitoring notes documented

---

## Phase 6 — Identity, Security & Access Control

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
- [ ] Authentication events are logged
- [ ] Administrative actions are reviewable

### Validation Evidence
- [ ] Identity model documented in `access/`
- [ ] Security model reviewed in `security/architecture.md`

---

## Phase 7 — Service Lifecycle & Environment Promotion

**Objective:** Ensure services are safe to promote beyond experimentation.

### Promotion Readiness
- [ ] Service purpose clearly defined
- [ ] Security boundaries reviewed
- [ ] Firewall rules documented
- [ ] Monitoring enabled
- [ ] Backup strategy exists

### Change Discipline
- [ ] Rollback plan documented
- [ ] Change recorded in build journal
- [ ] No undocumented configuration changes

### Validation Evidence
- [ ] Service lifecycle documented in `services/`
- [ ] Change logged in `logs/build-journal.md`

---

## Phase 8 — Advanced Workloads & Optimization

**Objective:** Ensure high-performance workloads do not bypass controls.

### GPU & Remote Workstation
- [ ] GPU access restricted to approved users
- [ ] Remote workstation requires secure entry (VPN / identity)
- [ ] No direct exposure of GPU host to untrusted networks

### Performance vs Security Balance
- [ ] Firewall rules reviewed for least privilege
- [ ] Logging remains enabled despite performance tuning

### Validation Evidence
- [ ] GPU workflow documented in `compute/gpu/`
- [ ] Remote access documented in `services/remote-access/`

---

## Phase 9 — Continuous Improvement & Expansion

**Objective:** Maintain security posture as the lab evolves.

### Ongoing Validation
- [ ] New hardware added to inventory
- [ ] New services documented before exposure
- [ ] Trust-zone matrix reviewed after changes

### Security Hygiene
- [ ] Periodic rule review performed
- [ ] Obsolete services removed
- [ ] Documentation kept current

### Validation Evidence
- [ ] Logs reflect evolution of the lab
- [ ] Architecture documents updated as needed
