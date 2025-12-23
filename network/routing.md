# Routing

This file documents where routing occurs in the homelab and what routes are in effect.
Keep this aligned to **live state** (what is actually implemented), not future design.

---

## Current Routing State (Active)

- **Default gateway (home network):** `192.168.68.1` (Deco / upstream router)
- **Default gateway (homelab VLAN 10):** `192.168.10.1` (pfSense `LAB_VLAN10`)

- **Inter-VLAN routing location:** pfSense  
  - Status: **Not in use yet**
  - Notes: Only VLAN 10 is active. No additional VLAN interfaces are routed yet.

- **Outbound routing (homelab → internet):** pfSense → upstream NAT (double-NAT)  
  - pfSense WAN obtains IP via DHCP from upstream `192.168.68.0/24`
  - Upstream router performs NAT to ISP

- **Static routes:** None  
  - Rationale: Current design relies on pfSense as the L3 boundary for VLAN 10 with standard default routing.

---

## Planned (Not Implemented)

- **Inter-VLAN routing:** Will occur on pfSense once VLAN 20 (IOT) and VLAN 30 (MGMT) are created and validated.
- **Static routes:** Not expected unless a separate routed segment is introduced (e.g., dedicated server subnet, VPN subnet routing, or downstream router).

---

## Notes / Guardrails

- Routing and VLAN expansion will be introduced one layer at a time:
  - VLAN interfaces on pfSense → validate DHCP + outbound → then switch tagging/access ports.
- Do not add static routes until a clear requirement exists (avoid complexity early).
