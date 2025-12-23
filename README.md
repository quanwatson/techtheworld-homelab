# TechTheWorld Homelab  
## Enterprise-Style Validation & Learning Environment

This repository documents a **home-based, enterprise-style homelab** designed as a
**technology integration, solution validation, and professional skills development environment**.

Although physically located at home, this lab is intentionally designed and operated
to mirror **real enterprise and MSP environments**, with an emphasis on
documentation, security boundaries, change control, and lifecycle thinking.

---

## Purpose & Design Philosophy

The primary purpose of this homelab is to **train production-grade thinking**.

Rather than focusing only on “making things work,” the lab emphasizes:

- isolation before optimization  
- explicit trust boundaries  
- documentation-first workflows  
- controlled change and rollback  
- operational realism over convenience  

The environment is built to safely emulate real-world scenarios—including failure and recovery—
without risking household connectivity.

---

## What This Lab Is For

- Building **Network Engineering** skills with a **security-first mindset**
- Practicing enterprise-style:
  - segmentation
  - routing
  - firewall policy
  - access control
- Validating infrastructure designs end-to-end in a **safe sandbox**
- Running proof-of-concepts through a full lifecycle:
  - **Sandbox → Hardened → Production-like**
- Hosting and operating core platform services:
  - DNS, DHCP, directory services
  - monitoring, logging, backups
- Supporting **remote workstation and GPU-backed workloads**
- Producing durable artifacts (docs, diagrams, logs) suitable for:
  - interviews
  - design reviews
  - portfolio demonstration

---

## What This Lab Is Not

- It is not optimized for convenience over clarity  
- It is not a flat or implicitly trusted network  
- It is not a collection of undocumented experiments  
- It is not disposable infrastructure  

Every meaningful change is expected to be **intentional, reviewable, and documented**.

---

## Primary Domain

- **External domain:** `techtheworld.net`

The domain is used to emulate enterprise identity and service patterns, including:
- directory services (mock enterprise domain)
- internal and external DNS zones
- service naming and certificates
- web and application hosting patterns

---

## Repository Structure

This repository is organized by **infrastructure domains**, not by tools or one-off projects:

- `overview/` — vision, architecture, roadmap, environment descriptions  
- `hardware/` — device inventory, roles, naming and labeling standards  
- `network/` — topology, IP plans, routing, firewall, switching, diagrams  
- `compute/` — hosts, hypervisors, VMs, containers, GPU workloads  
- `services/` — service catalog and lifecycle documentation  
- `domain/` — directory services, DNS, certificates, domain integration  
- `access/` — identity, authentication, remote access models  
- `security/` — segmentation, trust zones, firewall design, validation checklists  
- `automation/` — scripts, workflows, orchestration, promotion mechanics  
- `operations/` — monitoring, backups, patching, maintenance, incidents  
- `playbooks/` — repeatable how-to guides and design patterns  
- `runbooks/` — step-by-step operational procedures  
- `logs/` — build journal, homelab log, learning log, change control, session notes  
- `configs/` — sanitized configuration references (**no secrets**)  
- `diagrams/` — source files and rendered architecture diagrams  

---

## How to Navigate This Repository

This repository is organized to reflect **enterprise infrastructure domains** and
**professional engineering workflows**, not ad-hoc experimentation.

If you are reviewing this repository for technical depth, decision-making, or operational maturity,
use the guidance below.

### 1. Start with Intent and Architecture
- `overview/` — vision and architectural direction  
- `network/topology.md` — baseline physical and logical network design  
- `security/` — trust zones, firewall design, and validation framework  

These establish **design intent and boundaries** before implementation details.

---

### 2. Review System Evolution and Decisions
- `logs/build-journal.md` — authoritative system state changes  
- `logs/change-control.md` — planned and executed changes  
- `logs/learning-log.md` — engineering judgment and understanding gained  

This shows **deliberate evolution**, not trial-and-error.

---

### 3. Examine Operational Reality
- `logs/homelab-log.md` — session-level activity  
- `logs/session-notes.md` — in-progress context and assumptions  
- `operations/` — monitoring, backups, and maintenance practices  

This reflects how the lab operates as a **living system**.

---

### 4. Dive into Infrastructure Domains
Each domain stands on its own, mirroring enterprise ownership boundaries:

- `hardware/` — physical systems  
- `network/` — VLANs, routing, switching  
- `compute/` — virtualization and workloads  
- `services/` — service lifecycle documentation  
- `domain/` — identity and DNS  
- `access/` — authentication and remote access  
- `security/` — controls, segmentation, validation  
- `automation/` — workflows and orchestration  

---

### 5. Look at Execution Patterns
- `playbooks/` — reusable implementation patterns  
- `runbooks/` — step-by-step operational procedures  

These demonstrate **repeatability and operational readiness**.

---

### 6. Reference Supporting Artifacts
- `configs/` — sanitized configuration references  
- `diagrams/` — visual architecture representations  

These support the written documentation rather than replace it.

---

### Reviewer Note

This repository is designed to be read **non-linearly**.
Each section stands alone while reinforcing a shared model of:

- isolation  
- security  
- change control  
- documentation discipline  

The goal is not just to show *what* was built, but *how an engineer thinks while building it*.

---

## Operating Principles

- **No secrets** are stored in this repository  
- **No implicit trust** between networks, systems, or services  
- **Decisions and state changes are logged**; commands are not  
- **Changes are deliberate**, scoped, and recoverable  
- **Documentation is part of the build**, not an afterthought  

This repository is treated as **production-quality documentation for a living system**,
even though the environment itself is a lab.

---

_Last updated: 12-22-2025_
