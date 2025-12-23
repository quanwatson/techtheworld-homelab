# Security Model Overview

The homelab security model is built on the principle that **network segmentation and identity must work together**.  
Neither VLANs nor authentication alone are sufficient to establish trust.

---

## Core Security Pillars

### 1. Network Segmentation (Where You Are)
- VLANs define **initial trust boundaries**
- Devices are grouped by function and risk
- Routing between VLANs is always explicit
- No VLAN is trusted by default

Segmentation limits blast radius and reduces the impact of compromise.

---

### 2. Identity & Authentication (Who You Are)
- Identity determines **who is allowed access**
- Directory services (domain accounts, service accounts) provide accountability
- Privileged access is restricted to known identities
- Authentication events are logged

Identity prevents anonymous or uncontrolled access.

---

### 3. Authorization & Policy (What You Can Do)
- Firewall rules enforce **network-level authorization**
- Role-based access control enforces **service-level authorization**
- Management access is restricted to MGMT VLAN and approved identities

Authorization ensures access is purposeful and minimal.

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

## Practical Outcomes
- Compromise of one VLAN does not compromise the environment
- Credentials alone are insufficient without network access
- Network access alone is insufficient without identity
- Security testing can be performed safely and realistically

This layered model enables enterprise-grade security experimentation while maintaining a controlled lab environment.
