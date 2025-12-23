# Firewall Rule Categories & Validation Mapping

This document maps **security validation checklist items** directly to **firewall rule categories**.
Every firewall rule in the lab should belong to one of these categories and map back to a phase objective.

---

## Rule Category 1 — Perimeter Control (North–South)

**Purpose:**  
Control traffic entering and leaving the lab environment.

### Typical Rules
- WAN → Internal: ❌ (default deny)
- Internal → WAN: ✅ (restricted outbound)
- WAN → DMZ: ⚠️ (explicit, minimal exposure)

### Checklist Mapping
- Phase 1: Baseline Network & Isolation  
  - Default deny at perimeter  
  - No inbound access to internal VLANs  
  - Outbound access explicitly allowed  

### Validation Questions
- Can anything reach internal VLANs from WAN without an explicit rule?
- Are outbound rules overly permissive?

---

## Rule Category 2 — Inter-VLAN Segmentation (East–West)

**Purpose:**  
Prevent lateral movement between internal trust zones.

### Typical Rules
- LAB → IOT: ❌  
- IOT → LAB: ❌  
- LAB → MGMT: ⚠️ (restricted ports/hosts)  

### Checklist Mapping
- Phase 2: Network Segmentation & Trust Zones  
  - Default deny between VLANs  
  - Explicit justification for allowed flows  
  - Trust-zone matrix enforcement  

### Validation Questions
- Does every inter-VLAN rule have a documented purpose?
- Are any “any-to-any” rules present?

---

## Rule Category 3 — Management Plane Protection

**Purpose:**  
Protect administrative interfaces and control paths.

### Typical Rules
- MGMT → Infrastructure services: ✅  
- LAB → MGMT: ⚠️ (admin-only, restricted)  
- IOT → MGMT: ❌  

### Checklist Mapping
- Phase 3: Switching & Layer 2 Integration  
- Phase 6: Identity, Security & Access Control  

### Validation Questions
- Can non-admin VLANs reach management interfaces?
- Is management access limited to known hosts and users?

---

## Rule Category 4 — Service Access Control

**Purpose:**  
Control access to specific services regardless of network location.

### Typical Rules
- LAB → Service (specific ports): ✅  
- HOME → Service: ⚠️ (temporary, conditional)  
- WAN → Service: ❌ (unless DMZ-hosted)

### Checklist Mapping
- Phase 5: Core Services & Platform Enablement  
- Phase 7: Service Lifecycle & Promotion  

### Validation Questions
- Are services reachable only from intended VLANs?
- Is service exposure broader than necessary?

---

## Rule Category 5 — Identity-Dependent Access (Policy + Network)

**Purpose:**  
Ensure network access does not equal authorization.

### Typical Rules
- Allow network path but enforce auth at service layer
- Restrict admin ports to identity-aware endpoints

### Checklist Mapping
- Phase 6: Identity, Security & Access Control  

### Validation Questions
- Does a permitted network path still require authentication?
- Are privileged services reachable anonymously?

---

## Rule Category 6 — Remote Access & Bastion Control

**Purpose:**  
Broker all remote and administrative access through controlled entry points.

### Typical Rules
- VPN → MGMT: ✅  
- VPN → LAB: ⚠️  
- Direct WAN → Internal: ❌  

### Checklist Mapping
- Phase 6: Identity, Security & Access Control  
- Phase 8: Advanced Workloads & Optimization  

### Validation Questions
- Is all remote admin traffic brokered?
- Are any internal services directly exposed?

---

## Rule Category 7 — High-Risk / Low-Trust Containment

**Purpose:**  
Isolate inherently risky devices and workloads.

### Typical Rules
- IOT → WAN: ⚠️ (restricted destinations)  
- IOT → Internal: ❌  
- LAB (test malware, exploits) → MGMT: ❌  

### Checklist Mapping
- Phase 2: Network Segmentation & Trust Zones  
- Phase 8: Advanced Workloads & Optimization  

### Validation Questions
- Can compromised low-trust devices pivot internally?
- Are risky test systems properly constrained?

---

## Rule Category 8 — Observability & Control Plane Access

**Purpose:**  
Ensure security tools can see what they need without overexposure.

### Typical Rules
- Monitoring → All VLANs: ⚠️ (read-only ports)  
- Logging → Central services: ✅  

### Checklist Mapping
- Phase 5: Core Services & Platform Enablement  
- Phase 9: Continuous Improvement  

### Validation Questions
- Are monitoring/logging paths minimal and documented?
- Do observability tools have write access unnecessarily?

---

## Rule Category 9 — Temporary / Exception Rules

**Purpose:**  
Support troubleshooting without permanently weakening posture.

### Typical Rules
- Time-bound access rules
- Source-limited exception rules

### Checklist Mapping
- Phase 7: Service Lifecycle & Promotion  
- Phase 9: Continuous Improvement  

### Validation Questions
- Are exception rules time-limited?
- Are expired exceptions removed?

---

## Rule Hygiene Standards (Applies to All Categories)

Every firewall rule must have:
- A documented **category**
- A **phase justification**
- A clear **source → destination → port**
- A review point or expiration (where applicable)

Rules without justification are technical debt.
