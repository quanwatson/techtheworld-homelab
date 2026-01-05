# Architecture Overview

## Purpose of This Document

This document describes the **intentional architecture** of the HomeLab environment.

It explains:
- How the system is structured
- Why components are separated the way they are
- What assumptions and constraints guided design decisions
- How the architecture supports both learning and professional relevance

This is **design documentation**, not live configuration output.

---

## Architectural Principles

The HomeLab architecture is guided by the following principles:

### 1. Separation of Concerns
Each major responsibility is isolated to reduce blast radius and improve clarity:
- Network security and routing are handled by a dedicated firewall
- Switching enforces Layer 2 boundaries
- Virtualization hosts services, not control logic
- Management and production traffic are separated

### 2. Layered Design
Changes are introduced one layer at a time:
- Layer 3 (pfSense) is validated before Layer 2 (switching)
- Core networking is stabilized before services are deployed
- Platform hardening precedes application workloads

This minimizes ambiguity during failures and simplifies rollback.

### 3. Documentation as Control Plane
Architecture decisions are documented **before** implementation.
Runbooks, checklists, and logs govern execution and validation.

The repository itself acts as a **control surface** for the environment.

### 4. Constraint-Aware Engineering
The architecture intentionally reflects real-world constraints:
- Legacy hardware and older IOS limitations
- Finite CPU, memory, and storage resources
- Household connectivity must remain stable
- No assumptions of “greenfield” perfection

Constraints are treated as training inputs, not blockers.

---

## High-Level Architecture

At a high level, the HomeLab consists of:

- **Edge / Firewall Layer**
  - pfSense running on dedicated hardware
  - Responsible for:
    - WAN connectivity
    - Inter-VLAN routing
    - Firewall policy enforcement
    - DHCP and gateway services

- **Access / Switching Layer**
  - Cisco Catalyst 3560 (IOS 12.2 IPBASE)
  - Responsible for:
    - VLAN enforcement
    - Trunking to pfSense
    - Port-level security and hardening
    - Physical access control

- **Compute / Virtualization Layer**
  - Proxmox VE on dedicated host
  - Responsible for:
    - Hosting infrastructure services
    - Isolating workloads via VMs
    - Snapshotting and recovery
    - Acting as the service foundation for future phases

---

## Network Segmentation Model

The architecture uses explicit VLAN-based segmentation:

| VLAN | Purpose | Notes |
|-----|--------|------|
| 10 | LAB / Management | Primary management and lab traffic |
| 20 | IOT (planned) | Restricted device network |
| 30 | MGMT (future) | Dedicated management plane |
| 999 | Blackhole / Native | Disabled ports and native VLAN |

Key rules:
- VLAN 1 is never used for management
- Native VLAN is unused and non-routable
- Trunks explicitly allow only required VLANs
- Access ports are hardened and scoped

---

## Trust & Identity Boundaries

The architecture separates **trust domains** explicitly:

- External trust:
  - Public DNS and TLS handled via Cloudflare
  - No direct exposure of internal services

- Internal trust:
  - Internal DNS namespace (`corp.techtheworld.win`)
  - Internal Certificate Authority (planned)
  - Service-to-service trust managed internally

This separation mirrors enterprise hybrid models.

---

## Service Placement Philosophy

Services are deployed based on **role**, not convenience:

- One service per VM where possible
- Infrastructure services precede applications
- Control-plane services (DNS, CA, identity) are isolated
- Application services never share identity or trust responsibilities

This improves security, troubleshooting, and future scalability.

---

## Failure & Recovery Assumptions

The architecture assumes:
- Interfaces will be misconfigured
- Ports will err-disable
- Services will fail
- Documentation may lag reality temporarily

Recovery is enabled through:
- Console access paths
- Known-good baselines
- Incremental changes
- Clear rollback procedures

Failure is treated as an expected state, not an exception.

---

## Architectural Scope (What This Is and Is Not)

### This architecture **is**:
- Production-inspired
- Constraint-aware
- Documented and reviewable
- Designed for growth

### This architecture **is not**:
- A high-availability production system
- Optimized for maximum performance
- Vendor-locked or tool-centric
- Built for scale beyond a single operator

---

## Summary

This HomeLab architecture is intentionally simple, explicit, and disciplined.

It is designed to demonstrate:
- Sound infrastructure design thinking
- Respect for operational risk
- Clear separation of responsibility
- Professional documentation practices

Most importantly, it reflects **how I approach engineering problems** — with structure, caution, and intent.
