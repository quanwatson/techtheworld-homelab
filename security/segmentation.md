# Trust-Zone Segmentation Model

This document defines trust zones within the homelab and explicitly documents **allowed and denied communication paths**.  
All access is **deny-by-default** unless stated otherwise.

---

## Trust Zones

| Zone | VLAN | Purpose | Trust Level |
|----|----|----|----|
| WAN | N/A | Internet / untrusted networks | Untrusted |
| HOME | 192.168.68.0/24 | Home network (upstream) | Low |
| LAB | VLAN 10 | Test systems, Proxmox, experiments | Medium |
| IOT | VLAN 20 | Smart / low-trust devices | Low |
| MGMT | VLAN 30 | Network & system management | High |
| DMZ | (future) | Externally exposed services | Low–Medium |

---

## Trust-Zone Communication Matrix

Legend:  
- ✅ Allowed (explicitly permitted by firewall rules)  
- ❌ Denied (default)  
- ⚠️ Conditional (restricted ports, identities, or time-based rules)

| Source → Destination | WAN | HOME | LAB | IOT | MGMT | DMZ |
|---------------------|-----|------|-----|-----|------|-----|
| WAN | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ |
| HOME | ⚠️ | ❌ | ❌ | ❌ | ❌ | ❌ |
| LAB | ⚠️ | ❌ | ❌ | ❌ | ⚠️ | ❌ |
| IOT | ⚠️ | ❌ | ❌ | ❌ | ❌ | ❌ |
| MGMT | ⚠️ | ❌ | ⚠️ | ❌ | ❌ | ⚠️ |
| DMZ | ⚠️ | ❌ | ❌ | ❌ | ❌ | ❌ |

---

## Communication Rules (Narrative)

### WAN → Internal
- No inbound access to internal VLANs by default
- Only explicitly exposed services may exist in DMZ
- Port forwarding is tightly controlled and documented

### HOME → LAB / MGMT
- Home network is treated as **untrusted**
- Any access is conditional and temporary
- Used primarily for administration or troubleshooting

### LAB → WAN
- Outbound internet access allowed for updates and testing
- Inbound access denied by default

### LAB → MGMT
- Restricted to administrative protocols
- Limited to approved hosts and identities
- Logged and auditable

### IOT → Any
- IOT devices have **no lateral access**
- Internet access restricted to required destinations only
- No access to MGMT or LAB

### MGMT → Others
- MGMT can initiate connections to administer systems
- Access is identity-aware and logged
- No inbound access into MGMT

---

## Design Principles Reinforced
- No implicit trust between zones
- Lateral movement is intentionally difficult
- Management access is centralized and controlled
- Every allowed flow has a documented justification
