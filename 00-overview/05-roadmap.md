# Roadmap Overview

## Purpose of This Document

This document outlines the **phase-based roadmap** used to build and evolve the HomeLab.

The roadmap provides:
- Clear sequencing of work
- Defined stopping points
- Gated progression between phases
- Alignment between learning objectives and technical outcomes

This is not a task list — it is an **execution framework**.

---

## Roadmap Philosophy

The roadmap follows these guiding principles:

- Build foundations before services
- Validate before expanding
- Document before implementing
- One major change per session
- No phase advances without stability

Each phase produces **reviewable artifacts**, not just configurations.

---

## Phase Overview

### Phase 0 — Foundations & Discipline ✅ COMPLETE
**Focus:** Professional workflow and documentation discipline

- Repository structure
- Logging taxonomy
- Git workflow
- Documentation-first methodology

**Outcome:**  
A controlled environment where changes can be made safely and reviewed confidently.

---

### Phase 1 — Firewall & Layer 3 Baseline ✅ COMPLETE
**Focus:** Network routing and security foundation

- pfSense deployment
- VLAN routing
- DHCP and firewall rules
- Layer 3 validation

**Outcome:**  
Deterministic routing and segmentation foundation.

---

### Phase 2 — Switching & Layer 2 Enforcement ✅ COMPLETE
**Focus:** Physical and logical network enforcement

- Managed switch configuration
- VLAN trunking
- Access port control
- Management isolation

**Outcome:**  
Layer 2 boundaries enforced and validated.

---

### Phase 3 — Switch Hardening ✅ COMPLETE
**Focus:** Access-layer protection and failure handling

- PortFast
- BPDU Guard
- Storm control
- Err-disable recovery

**Outcome:**  
Real-world protection mechanisms validated through live failure scenarios.

---

### Phase 4 — Service Enablement & Virtualization 🟡 ACTIVE

#### Phase 4.1 — Domain & Certificate Strategy ✅ COMPLETE
- External domain definition
- Internal namespace design
- Certificate trust model
- DNS strategy

#### Phase 4.2 — Proxmox Platform 🟡 PLANNING COMPLETE
- Hardware validated
- VM layout designed
- Network integration planned
- Execution pending approval

**Outcome:**  
Platform ready to host infrastructure services.

---

### Phase 5 — Core Infrastructure Services 🔜 FUTURE
**Focus:** Internal service foundations

- Internal DNS
- Internal Certificate Authority
- Time and trust services

---

### Phase 6 — Identity & Directory Services 🔜 FUTURE
**Focus:** Centralized identity and policy

- Active Directory
- GPO baselines
- Role-based access

---

### Phase 7 — Control Plane & Documentation Services 🔜 FUTURE
**Focus:** Operational visibility and governance

- Odoo-based IT Glue–like system
- Asset inventory
- Credential management
- Service mapping

---

### Phase 8 — Automation, Monitoring & AI 🔜 FUTURE
**Focus:** Operational maturity and efficiency

- Monitoring stack
- Alerting
- Automation workflows
- Private AI services

---

### Phase 9 — Client-Ready Reference Architecture 🔜 FUTURE
**Focus:** Professional translation

- MSP-ready reference designs
- Client onboarding playbooks
- Portfolio artifacts
- Homelab → enterprise mapping

---

## Roadmap Status Summary

- ✔ Foundations stable
- ✔ Networking complete and hardened
- 🟡 Virtualization execution pending
- 🔜 Services and identity planned

---

## Summary

This roadmap ensures the HomeLab evolves **intentionally**, not reactively.

Each phase builds upon validated work, producing:
- Clear learning outcomes
- Professional documentation
- Transferable real-world skills

The roadmap reflects how infrastructure is responsibly grown in professional environments.
