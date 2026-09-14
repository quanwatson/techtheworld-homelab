# Security Model Overview

The short version: segmentation alone doesn't establish trust, and neither does authentication alone. This lab's security model leans on both together — where you are on the network and who you've proven you are.

---

## The three things doing the work

**Where you are — network segmentation.** VLANs set the initial trust boundary. Devices get grouped by function and risk, routing between VLANs is always explicit, and no VLAN gets trusted just because it exists. This is what limits blast radius if something gets compromised.

**Who you are — identity and authentication.** Identity decides who's actually allowed in. Directory accounts and service accounts provide accountability, privileged access is restricted to known identities, and authentication events get logged. This is what stops anonymous or uncontrolled access, which segmentation alone can't do.

**What you can do — authorization and policy.** Firewall rules handle network-level authorization; role-based access control handles it at the service level. Management access is locked to the MGMT VLAN plus approved identities. The goal is access that's purposeful and minimal, not access that's merely possible.

---

## How VLANs and Identity Work Together

### Initial Access Control
- Devices are placed into VLANs based on trust and role
- VLAN placement limits *where* a device can reach

### Secondary Access Control
- Identity determines *what* the device or user can access
- Even within a permitted VLAN path, services may still require authentication

### Example Flow
1. A system resides in the LAB VLAN  
2. Firewall rules allow LAB → MGMT on limited ports  
3. Access to management services still requires authenticated credentials  
4. All activity is logged  

Network access does **not** equal permission.

---

## Zero-Trust Alignment

This model aligns with zero-trust principles:
- Never trust the network alone
- Always verify identity
- Assume breach and limit lateral movement
- Log and observe continuously

---

## What this buys me in practice

Compromising one VLAN doesn't compromise the whole environment. Stolen credentials without network access get you nowhere, and network access without identity gets you nowhere either — you need both. Which also means I can actually run security testing here without it turning into a real incident.
