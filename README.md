# HomeLab — Network, Systems, and Solutions Architecture Lab

## Overview

This repository documents a deliberately designed HomeLab used to develop and validate real-world skills in **networking, systems administration, security, and solution architecture**.

The lab is built and operated using **documentation-first, phase-gated execution**, mirroring how infrastructure is designed, implemented, and maintained in professional IT, MSP, and enterprise environments.


---

## What This Lab Is (and Is Not)

**This lab is:**
- A controlled, production-inspired environment
- Built with change control, validation, and rollback in mind
- Designed to simulate real operational constraints
- Documented as if it were supporting a real organization

**This lab is not:**
- A collection of ad-hoc experiments
- A “click-through” tutorial repo
- A single-tool showcase
- A résumé keyword dump without operational depth

---

## Core Principles

### Documentation-First Engineering
Documentation is treated as part of the system, not a byproduct.

Before changes are made:
- Design intent is written
- Risks and rollback paths are identified
- Execution is gated by checklists and runbooks

### Layered, Phase-Gated Execution
Infrastructure changes are introduced one layer at a time:
- Layer 3 before Layer 2
- Planning before execution
- Validation before expansion

This reduces ambiguity, simplifies troubleshooting, and mirrors production change management.

### Real-World Constraints
The lab intentionally incorporates:
- Legacy hardware and software limitations
- Platform feature constraints
- Failure scenarios and recovery paths
- Security trade-offs and audit considerations

---

## Repository Navigation

### Start Here
- **`00-overview/overview.md`** — How the lab is structured and how to read this repo

### Core Documentation
- **`01-logs/`**
  - Build Journal (state changes)
  - Learning Log (understanding gained)
  - Session Notes (continuity)
- **`03-network/`**
  - Firewall, routing, VLANs, switching
- **`14-runbooks/`**
  - Phase-gated, step-by-step operational procedures

### Platform & Services
- Proxmox virtualization platform
- Internal certificate authority (planned)
- Internal DNS (planned)
- Identity and directory services (future)
- Control-plane documentation services (future)

---

## Tooling & Methodology

Modern tooling—including AI-assisted research and guidance—was used **selectively and intentionally** to accelerate learning and improve clarity.

All of the following were performed by me:
- Architecture decisions
- Configuration and implementation
- Troubleshooting and recovery
- Validation and documentation

AI tools were treated as **reference and acceleration aids**, not replacements for understanding or responsibility.

---

## For Employers and Reviewers

If you are reviewing this repository in a professional context:

- Begin with **`00-overview/overview.md`**
- Review the **Build Journal** to see real state changes
- Review the **Runbooks** to understand execution discipline
- Review the **Learning Log** to see growth and judgment over time

For a deeper explanation of intent, mindset, and professional framing, see:  
➡️ **Professional Context:** *HomeLab Project — Professional Context (For Employers)*

---

## Project Goal

The goal of this HomeLab is not just to demonstrate technical capability, but to show **how I think, plan, execute, and document** systems—skills directly transferable to **enterprise IT, MSP operations, and solutions architecture roles**.
