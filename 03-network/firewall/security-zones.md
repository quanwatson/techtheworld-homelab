# Security Zones

This document defines homelab trust boundaries ("zones") and the allowed traffic flows between them.
Zones are documented by **intent** and **risk level**, not by interface syntax.

Only **active zones** are treated as current. Planned zones are explicitly labeled.

---

## Zone Model (Current)

### UPSTREAM_HOME (External Dependency)
**Trust Level:** External / Untrusted (from homelab perspective)  
**Network:** `192.168.68.0/24`  
**Gateway:** `192.168.68.1` (Deco)  
**Notes:**  
This is the household network and upstream internet edge. It is not governed by pfSense policy and is treated as an upstream dependency.

**Allowed Flows (Current):**
- `LAB_VLAN10` → `UPSTREAM_HOME` → Internet (outbound NAT only)

**Denied / Not Allowed (Current):**
- `UPSTREAM_HOME` → `LAB_VLAN10` (implicit deny / no inbound access)

---

### LAB_VLAN10 (Homelab Zone)
**Trust Level:** Controlled / Internal (lowest risk lab zone for now)  
**Network:** `192.168.10.0/24`  
**Gateway:** `192.168.10.1` (pfSense)  
**Notes:**  
This is the initial lab zone used for validation, management, and early systems. It is the only active segmented network.

**Allowed Flows (Current):**
- `LAB_VLAN10` → Internet (general outbound allowed)
- `LAB_VLAN10` → pfSense management (Web UI / diagnostics)

**Denied / Not Allowed (Current):**
- `LAB_VLAN10` → other VLANs (none implemented yet)
- Inbound from upstream/home network

---

## Planned Zones (Not Implemented)

### IOT_VLAN20 (Planned)
**Trust Level:** Low / Untrusted internal  
**Purpose:** IoT devices, smart home devices, anything that should not touch lab/admin assets by default  
**Expected Policy:**  
- Internet access as needed  
- No access to management or lab systems unless explicitly required

---

### MGMT_VLAN30 (Planned)
**Trust Level:** High / Administrative  
**Purpose:** Dedicated management plane for infrastructure (pfSense, switches, hypervisors, monitoring)  
**Expected Policy:**  
- Management zone initiates access to other zones  
- Other zones do not initiate access to management

---

## Policy Guardrails

- Default stance: **deny at zone boundaries**
- Allow rules must be **documented by intent** (source → destination → ports → reason)
- Avoid “temporary allows” without an expiration plan
- Introduce one major boundary change per session (validate → document → proceed)

---

## Flow Summary (Current)

- **Allowed:** `LAB_VLAN10` → Internet (via pfSense NAT)  
- **Allowed:** `LAB_VLAN10` → pfSense management  
- **Not Allowed:** `UPSTREAM_HOME` → any homelab zone (no inbound initiation)
