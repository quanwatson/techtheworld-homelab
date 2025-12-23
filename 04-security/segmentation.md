# Trust-Zone Segmentation Model

This document defines trust zones within the homelab and explicitly documents
**allowed and denied communication paths** between them.

All access is **deny-by-default** unless explicitly stated.

Zones marked *Planned* are design intent only and are not yet enforced.

---

## Trust Zones

| Zone  | VLAN / Network        | Purpose                                   | Trust Level | Status   |
|------|------------------------|--------------------------------------------|-------------|----------|
| WAN  | N/A                    | Internet / untrusted networks              | Untrusted   | Active   |
| HOME | 192.168.68.0/24        | Home network (upstream dependency)          | Low         | Active   |
| LAB  | VLAN 10 (192.168.10.0) | Lab systems, validation, early workloads   | Medium      | Active   |
| IOT  | VLAN 20                | Smart / low-trust devices                  | Low         | Planned  |
| MGMT | VLAN 30                | Network & system management                | High        | Planned  |
| DMZ  | TBD                    | Externally exposed services                | Low–Medium  | Planned  |

---

## Trust-Zone Communication Matrix

Legend:  
- ✅ Allowed (explicitly permitted)  
- ❌ Denied (default)  
- ⚠️ Conditional (restricted ports, identities, or time-based rules)  

> Matrix reflects **intended steady state**.  
> Only LAB ↔ WAN flows are currently active.

| Source → Destination | WAN | HOME | LAB | IOT | MGMT | DMZ |
|---------------------|-----|------|-----|-----|------|-----|
| WAN  | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ |
| HOME | ⚠️ | ❌ | ❌ | ❌ | ❌ | ❌ |
| LAB  | ⚠️ | ❌ | ❌ | ❌ | ⚠️ | ❌ |
| IOT  | ⚠️ | ❌ | ❌ | ❌ | ❌ | ❌ |
| MGMT | ⚠️ | ❌ | ⚠️ | ❌ | ❌ | ⚠️ |
| DMZ  | ⚠️ | ❌ | ❌ | ❌ | ❌ | ❌ |

---

## Communication Rules (Current State)

### WAN → Internal
- No inbound access to internal zones by default
- No port forwards configured
- pfSense blocks unsolicited inbound traffic

### HOME → LAB
- Home network is treated as **untrusted**
- No active access paths into LAB
- Any future access must be temporary and documented

### LAB → WAN
- Outbound internet access allowed for updates and testing
- NAT handled by pfSense
- Inbound access denied by default

---

## Communication Rules (Planned / Design Intent)

### LAB → MGMT
- Restricted to administrative protocols only
- Limited to approved hosts and identities
- Logged and auditable

### IOT → Any
- No lateral access to internal zones
- Internet access restricted to required destinations only
- No access to LAB or MGMT

### MGMT → Others
- MGMT initiates access for administration
- Identity-aware and logged
- No inbound access into MGMT

### WAN → DMZ
- Only explicitly exposed services
- Minimal ports, minimal surface area
- Strict change control required

---

## Design Principles Reinforced

- No implicit trust between zones
- Lateral movement is intentionally difficult
- Management access is centralized and controlled
- Trust is based on **zone + identity**, not network location alone
- Every allowed flow must have a documented justification
