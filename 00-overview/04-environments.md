# Environments Overview

## Purpose of This Document

This document defines the **logical environments** used within the HomeLab and explains how they are separated, governed, and evolved over time.

Environments are not treated as ad-hoc groupings.  
They are intentional boundaries used to manage **risk, stability, and change velocity**—mirroring how environments are handled in professional IT and MSP contexts.

---

## Environment Philosophy

The HomeLab follows a **progressive environment model**, where stability and experimentation are balanced intentionally.

Key principles:
- Household connectivity must remain stable at all times
- Core infrastructure is protected from experimental workloads
- Changes are introduced incrementally and validated
- Environment boundaries are documented, not assumed

---

## Defined Environments

### 1. Home / Household Environment

**Purpose:**  
Maintain uninterrupted, stable internet access for daily household use.

**Characteristics:**
- Not managed as part of the lab
- Minimal changes
- Treated as an external dependency
- Protected from lab experimentation

**Design Rule:**  
No lab activity should disrupt household connectivity.

---

### 2. LAB Environment (Primary Active Environment)

**Purpose:**  
Hands-on learning, validation, and controlled experimentation.

**Scope:**
- Network segmentation (VLAN 10)
- pfSense routing and firewalling
- Switch configuration and hardening
- Proxmox platform and infrastructure services

**Characteristics:**
- Actively changing
- Fully documented
- Change-controlled
- Console-accessible for recovery

This environment represents a **production-inspired but non-production** system.

---

### 3. Management Plane (Planned / Future)

**Purpose:**  
Centralized management and control of infrastructure components.

**Planned Capabilities:**
- Dedicated management VLAN
- Restricted access paths
- Identity-based access control
- Monitoring and logging endpoints

This environment will eventually separate **control traffic** from **workload traffic**, reflecting enterprise best practices.

---

### 4. Services Environment (Planned)

**Purpose:**  
Host internal infrastructure services that support the lab and future client simulations.

**Examples:**
- Internal DNS
- Internal Certificate Authority
- Directory Services (AD)
- Control-plane tooling (Odoo-based)

Services are deployed **after** platform and network stability are proven.

---

## Environment Interaction Rules

- Home → LAB: Allowed only through pfSense
- LAB → Home: Restricted and monitored
- LAB → Management: Controlled, least-privilege
- Services → Management: Trusted, authenticated paths only

No environment bypasses another directly.

---

## Change Discipline by Environment

| Environment | Change Velocity | Risk Tolerance |
|-----------|----------------|---------------|
| Home | None | Zero |
| LAB | Moderate | Controlled |
| Management | Low | Minimal |
| Services | Low–Moderate | Controlled |

Changes in higher-risk environments never propagate downward without validation.

---

## Summary

Environment separation in this HomeLab is intentional and enforced.

It enables:
- Safer experimentation
- Faster recovery
- Clear fault isolation
- Professional change management habits

This structure mirrors how real-world environments are protected, evolved, and governed.
