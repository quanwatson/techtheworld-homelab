# Firewall Rules

This document describes firewall rules by **intent**, not by raw rule syntax.
Rules are documented in terms of **source → destination → ports → reason** to preserve clarity and auditability.

Only **active rules** are listed as current. Planned rules are explicitly labeled.

---

## Default Policy

- **Inbound (WAN):** Deny by default
- **Inter-VLAN:** Deny by default
- **Outbound (LAN/VLAN):** Explicitly allowed as documented

pfSense default deny behavior is relied upon unless overridden.

---

## Active Firewall Rules

### VLAN 10 — LAB → Internet

**Source:** VLAN 10 (`192.168.10.0/24`)  
**Destination:** Any (Internet)  
**Ports:** Any  
**Action:** Allow  
**Reason:**  
Allow lab systems to access the internet for updates, testing, and general usage.

**Notes:**  
- NAT handled automatically by pfSense  
- No inbound return traffic allowed unless stateful  

---

### VLAN 10 — LAB → pfSense (Management)

**Source:** VLAN 10  
**Destination:** pfSense firewall  
**Ports:**  
- HTTPS (Web GUI)  
- ICMP (optional, for diagnostics)

**Action:** Allow  
**Reason:**  
Permit administrative access to pfSense from the lab management network.

---

## Explicitly Denied / Not Implemented

### Home Network → Homelab

**Source:** Home network (`192.168.68.0/24`)  
**Destination:** Homelab VLANs  
**Action:** Deny (implicit)  
**Reason:**  
Prevent household devices from initiating access into the homelab environment.

---

### Inter-VLAN Traffic

**Source:** Any VLAN  
**Destination:** Any other VLAN  
**Action:** Deny (implicit)  
**Reason:**  
No lateral trust between segments unless explicitly justified and documented.

---

## Planned Rules (Not Implemented)

These rules represent **design intent only** and will not be applied until
the switch layer and VLAN enforcement are fully validated.

- VLAN 10 → VLAN 20 (selective service access)
- VLAN 30 → All VLANs (management-only access)
- VPN / overlay network → Management VLAN

---

## Rule Documentation Standard

All future firewall rules must be documented using the following format:

- **Source:**  
- **Destination:**  
- **Ports / Protocols:**  
- **Action:** Allow / Deny  
- **Reason:**  
- **Scope:** Temporary / Permanent  

---

## Guardrails

- Do not add rules “just to make it work.”
- Every allow rule must have a documented reason.
- Deny by default is preserved at all trust boundaries.
- Rule changes must be:
  - Planned
  - Validated
  - Documented
  - Recorded in the Build Journal after implementation
