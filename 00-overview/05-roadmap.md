# Roadmap Overview

This is the phase-based plan I'm using to build out the HomeLab — sequencing, defined stopping points, and gates between phases so the work stays aligned with what I'm actually trying to learn. It's not a task list so much as an execution framework: nothing here happens just because it's next on a list.

A few rules I try to follow: build foundations before services, validate before expanding, document before implementing, one major change per session, and no phase advances until the current one is actually stable. Each phase is supposed to leave behind something reviewable, not just a config that happens to work.

## Where things stand, phase by phase

**Phase 0 — Foundations & Discipline** ✅ complete
Professional workflow and documentation habits: repo structure, logging taxonomy, git workflow, documentation-first methodology. Outcome: a place where I can make changes safely and actually trust my own review of them.

**Phase 1 — Firewall & Layer 3 Baseline** ✅ complete
pfSense deployment, VLAN routing, DHCP and firewall rules, Layer 3 validation. Outcome: deterministic routing and a real segmentation foundation.

**Phase 2 — Switching & Layer 2 Enforcement** ✅ complete
Managed switch configuration, VLAN trunking, access port control, management isolation. Outcome: Layer 2 boundaries enforced and validated.

**Phase 3 — Switch Hardening** ✅ complete
PortFast, BPDU Guard, storm control, err-disable recovery. Outcome: protection mechanisms I've actually tested against live failure scenarios, not just configured and hoped worked.

**Phase 4 — Service Enablement & Virtualization** 🟡 active

- *4.1 — Domain & Certificate Strategy* ✅ complete: external domain, internal namespace design, certificate trust model, DNS strategy.
- *4.2 — Proxmox Platform* 🟡 planning complete: hardware validated, VM layout designed, network integration planned, execution pending.

Outcome once this phase wraps: a platform ready to actually host infrastructure services.

**Phase 5 — Core Infrastructure Services** 🔜 future
Internal DNS, internal certificate authority, time and trust services.

**Phase 6 — Identity & Directory Services** 🔜 future
Active Directory, GPO baselines, role-based access.

**Phase 7 — Control Plane & Documentation Services** 🔜 future
An Odoo-based IT-Glue-style system, asset inventory, credential management, service mapping.

**Phase 8 — Automation, Monitoring & AI** 🔜 future
Monitoring stack, alerting, automation workflows, private AI services.

**Phase 9 — Client-Ready Reference Architecture** 🔜 future
MSP-ready reference designs, client onboarding playbooks, portfolio artifacts, mapping the homelab patterns onto enterprise scale.

## Where I actually am right now

Foundations are stable, and networking is complete and hardened. Virtualization execution is pending. Services and identity work is planned but not started. This roadmap is meant to keep the lab evolving on purpose instead of reactively chasing whatever seems interesting that week — each phase builds on validated work from the last one, which is really the only way any of this sticks.
