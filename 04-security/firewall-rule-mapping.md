# Firewall Rule Categories & Validation Mapping

This document maps **firewall rule intent** to **security validation phases**.
Every firewall rule in the homelab must belong to one of these categories and
support a specific phase objective.

This prevents ad-hoc rule creation and ensures security posture evolves
intentionally as the lab grows.

---

## Rule Category 1 — Perimeter Control (North–South)

**Purpose:**  
Control traffic entering and leaving the homelab environment.

### Typical Rule Patterns
- WAN → Internal: ❌ (default deny)
- Internal → WAN: ✅ (explicit outbound allow)
- WAN → DMZ: ⚠️ (explicit, minimal, service-specific)

### Phase Alignment
- **Phase 1: Baseline Network & Isolation**

### Validation Questions
- Is inbound traffic blocked by default at the perimeter?
- Is outbound access intentional rather than assumed?
- Are any inbound rules documented and justified?

---

## Rule Category 2 — Inter-VLAN Segmentation (East–West)

**Purpose:**  
Prevent lateral movement between internal trust zones.

### Typical Rule Patterns
- LAB → IOT: ❌
- IOT → LAB: ❌
- LAB → MGMT: ⚠️ (restricted ports / hosts)

### Phase Alignment
- **Phase 2: Network Segmentation & Trust Zones**

### Validation Questions
- Does every inter-VLAN allow rule have a documented reason?
- Are there any broad “any-to-any” rules?
- Is default deny preserved between VLANs?

---

## Rule Category 3 — Management Plane Protection

**Purpose:**  
Protect administrative interfaces and infrastructure control paths.

### Typical Rule Patterns
- MGMT → Infrastructure: ✅
- LAB → MGMT: ⚠️ (admin-only, tightly scoped)
- IOT → MGMT: ❌

### Phase Alignment
- **Phase 3: Switching & Layer 2 Integration**
- **Phase 6: Identity, Security & Access Control**

### Validation Questions
- Can non-admin networks reach management interfaces?
- Is management access restricted to known sources?
- Are management ports unnecessarily exposed?

---

## Rule Category 4 — Service Access Control

**Purpose:**  
Control access to specific services regardless of network location.

### Typical Rule Patterns
- LAB → Service (specific ports): ✅
- HOME → Service: ⚠️ (temporary or conditional)
- WAN → Service: ❌ (unless explicitly DMZ-hosted)

### Phase Alignment
- **Phase 5: Core Services & Platform Enablement**
- **Phase 7: Service Lifecycle & Promotion**

### Validation Questions
- Are services reachable only from intended networks?
- Is service exposure broader than required?
- Are temporary access paths tracked and removed?

---

## Rule Category 5 — Identity-Dependent Access (Policy + Network)

**Purpose:**  
Ensure network reachability does not imply authorization.

### Typical Rule Patterns
- Network access allowed, service enforces authentication
- Admin ports restricted to identity-aware endpoints

### Phase Alignment
- **Phase 6: Identity, Security & Access Control**

### Validation Questions
- Does permitted network access still require authentication?
- Are privileged services reachable anonymously?
- Is identity enforcement layered above network access?

---

## Rule Category 6 — Remote Access & Bastion Control

**Purpose:**  
Broker all remote and administrative access through controlled entry points.

### Typical Rule Patterns
- VPN / Overlay → MGMT: ✅
- VPN / Overlay → LAB: ⚠️
- Direct WAN → Internal: ❌

### Phase Alignment
- **Phase 6: Identity, Security & Access Control**
- **Phase 8: Advanced Workloads & Optimization**

### Validation Questions
- Is all remote administrative access brokered?
- Are any internal services directly exposed to WAN?
- Is remote access logged and auditable?

---

## Rule Category 7 — High-Risk / Low-Trust Containment

**Purpose:**  
Isolate inherently risky devices, services, or test workloads.

### Typical Rule Patterns
- IOT → WAN: ⚠️ (restricted destinations)
- IOT → Internal: ❌
- LAB (malware / exploit testing) → MGMT: ❌

### Phase Alignment
- **Phase 2: Network Segmentation & Trust Zones**
- **Phase 8: Advanced Workloads & Optimization**

### Validation Questions
- Can compromised low-trust devices pivot internally?
- Are risky workloads properly constrained?
- Is containment enforced at multiple layers?

---

## Rule Category 8 — Observability & Control Plane Access

**Purpose:**  
Enable monitoring and logging without overexposing the network.

### Typical Rule Patterns
- Monitoring → VLANs: ⚠️ (read-only ports)
- Devices → Central logging: ✅

### Phase Alignment
- **Phase 5: Core Services & Platform Enablement**
- **Phase 9: Continuous Improvement**

### Validation Questions
- Are observability paths minimal and documented?
- Do monitoring tools have unnecessary write access?
- Is telemetry flow one-directional where possible?

---

## Rule Category 9 — Temporary / Exception Rules

**Purpose:**  
Support troubleshooting or transitions without permanent posture erosion.

### Typical Rule Patterns
- Time-bound allow rules
- Source-limited exception rules

### Phase Alignment
- **Phase 7: Service Lifecycle & Promotion**
- **Phase 9: Continuous Improvement**

### Validation Questions
- Are exception rules time-limited?
- Are expired exceptions removed?
- Is temporary access clearly labeled?

---

## Rule Hygiene Standards (Applies to All Categories)

Every firewall rule must have:

- A documented **rule category**
- A **phase justification**
- A clear **source → destination → ports**
- A defined **scope** (permanent or temporary)
- A review or expiration point (where applicable)

Rules without justification are **technical debt** and must be removed or corrected.
