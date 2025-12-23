# NAT

This document tracks NAT behavior and intent for the homelab firewall.
It covers outbound NAT, inbound exposure (port forwards), and any special NAT cases.
Keep this aligned to **live state** first; planned items must be explicitly labeled.

---

## Current State (Active)

### Topology
- **Double NAT is intentional**
  - Upstream NAT: Deco router (home network → ISP)
  - Homelab NAT: pfSense (lab VLANs → home network)

### Outbound NAT
- **Status:** Enabled (default pfSense behavior)
- **Mode:** Default / automatic behavior (no custom NAT rules documented yet)
- **Effect:** Homelab VLAN traffic (currently VLAN 10) can reach the internet through pfSense and the upstream router.

### Inbound NAT / Port Forwards
- **Status:** None configured
- **Policy:** No inbound services are exposed through the Deco router or pfSense at this stage.

### 1:1 NAT
- **Status:** Not used

---

## Validation Notes

- VLAN 10 clients should have:
  - Default gateway: `192.168.10.1`
  - Working outbound connectivity via pfSense NAT
- Any testing should confirm:
  - DNS resolution works
  - Internet egress works
  - No inbound exposure exists

---

## Planned (Not Implemented)

These items are intentionally deferred until the switch layer is fully validated:

- **Selective outbound NAT rules** (only if needed for multi-WAN, VPN egress, or policy-based routing)
- **Inbound exposure** (only if required for a specific lab service, and only after Change Control approval)
- **Hairpin / NAT reflection** (only if hosting internal services accessed by public DNS)

---

## Guardrails

- Do not add port forwards “just to make it work.”
- If inbound access is required:
  - Prefer VPN / overlay access first
  - Document the service, port, and justification
  - Restrict source IPs where possible
  - Add corresponding firewall rules explicitly
  - Record the change in Change Control and Build Journal
