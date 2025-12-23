<<<<<<< HEAD
# Homelab (Enterprise-Style Validation Lab)

This repository documents a **scalable enterprise-style homelab** designed as a personal **technology integration, solution validation, and skills development environment**.

This lab is intentionally built to operate more like a **professional data center or enterprise lab** than a hobby setup. Every design choice reinforces production habits, security discipline, and architectural thinking.

---

## Purpose & Design Philosophy

The primary purpose of this homelab is to **train production thinking**.

Rather than focusing only on making systems work, the lab emphasizes:
- isolation
- explicit trust
- documentation
- lifecycle management
- operational realism

The environment is designed to safely emulate real-world enterprise scenarios, allowing experimentation, failure, recovery, and refinement without risking the home network.

---

## What this lab is for

- Build **Network Engineering** skills with a **security-first** mindset  
- Practice enterprise-style **segmentation, routing, and access control**  
- Emulate real-world environments in a **safe, isolated sandbox**  
- Run proof-of-concepts through a full lifecycle:
  - **Sandbox → Pre-Production → Production-like**
- Host and operate core infrastructure services:
  - DNS, DHCP, Directory Services
  - Monitoring, logging, and backups
- Provide a **remote workstation / GPU-backed service** for:
  - creator workloads
  - testing performance-sensitive applications
  - gaming via **Sunshine / Moonlight**
- Create durable artifacts (docs, diagrams, logs) that reflect professional standards

---

## What this lab is not

- It is not optimized for convenience over clarity  
- It is not a flat or implicitly trusted network  
- It is not a collection of undocumented experiments  
- It is not treated as disposable infrastructure  

Every meaningful change is expected to be **intentional, reviewable, and documented**.

---

## Primary domain

- External domain: **techtheworld.net**

The domain is used within the lab to emulate real enterprise identity and service patterns, including:
- Windows Server Active Directory (mock enterprise domain)
- Internal and external DNS zones
- Web hosting and service subdomains
- Certificate management and service identity

---

## Repository structure

This repository is organized by **enterprise infrastructure domains**, not by tools or one-off projects:

- `overview/` — vision, architecture, roadmap, environments, inventory  
- `hardware/` — hardware catalog, device records, naming and labeling standards  
- `network/` — topology, VLAN architecture, routing, firewall, switching, diagrams  
- `compute/` — hosts, hypervisors, VMs, containers, GPU workloads  
- `services/` — service catalog (CMDB-lite) and lifecycle documentation  
- `domain/` — directory services, DNS, web hosting, subdomains, certificates  
- `access/` — identity, VPN, RBAC, zero-trust considerations  
- `security/` — threat modeling, segmentation, hardening, detection, response  
- `automation/` — workflows, scripts, pipelines, promotion mechanics  
- `operations/` — monitoring, backups, patching, maintenance, incidents  
- `playbooks/` — repeatable how-to guides and patterns  
- `runbooks/` — step-by-step operational procedures  
- `logs/` — build journal, homelab log, learning log, change control  
- `configs/` — sanitized configuration references (**no secrets**)  
- `diagrams/` — source and exported architecture diagrams  

---

## Operating principles

- **No secrets in this repository**  
- **No implicit trust** between networks, systems, or services  
- **Decisions and state changes are logged**; commands are not  
- **Changes are deliberate**, scoped, and recoverable  
- **Documentation is part of the build**, not an afterthought  

This repository is treated as **production documentation for a living system**, even though the environment itself is a lab.

---

_Last updated: 2025-12-22_
=======
﻿# TechTheWorld Homelab

This repository documents a documentation-first homelab focused on:

- Network engineering
- Virtualization and compute
- Automation and orchestration
- Secure remote access
- AI-assisted operations
- MSP-style documentation and workflows

## Philosophy

No infrastructure is deployed without documentation.
All changes are planned, logged, and reviewed.

## Status

 In active build-out
>>>>>>> 859a8c1c8a4ec77b44982bcfa30bf217c7da3eed
