# Network Topology (Baseline)

This document describes the baseline physical and logical topology of the homelab.  
The design prioritizes isolation, safety, and realism for enterprise-style testing.

---

## Home Network (Upstream)

- **Gateway:** 192.168.68.1
- **Subnet:** 192.168.68.0/24

---

## pfSense Firewall

### WAN_UPSTREAM
- **IP Address:** 192.168.68.57 (DHCP)
- **Gateway:** 192.168.68.1

### LAN_CORE
- **IP Address:** 192.168.1.1/24
- **DHCP Range:** 192.168.1.100 – 192.168.1.199

---

## Network Segmentation Status (Baseline)

### VLANs Implemented
- **VLAN 10 — LAB**
  - Subnet: 192.168.10.0/24
  - Gateway: 192.168.10.1
  - DHCP: Enabled
  - Status: Routed and operational at the firewall layer

### Switch Integration
Switch-side VLAN tagging and port assignment are introduced deliberately and documented as part of controlled expansion.

---

## Logical Flow

## Logical Flow

The logical flow represents how traffic, trust, and services are intended to move through the environment, independent of physical cabling.

### North–South Traffic (External)
- Internet-facing traffic enters through the home router
- Traffic is forwarded to pfSense via the WAN_UPSTREAM interface
- pfSense enforces perimeter security, NAT, and inspection
- Only explicitly allowed services are exposed outward

### East–West Traffic (Internal)
- Internal traffic flows between VLANs are routed by pfSense
- All inter-VLAN communication is **explicitly controlled** by firewall rules
- No VLAN has implicit trust with any other VLAN
- Lateral movement is restricted unless justified and documented

### Service Access Flow
- Infrastructure services (DNS, directory, monitoring) reside in controlled VLANs
- Application and workload access is mediated through firewall policy
- Management access is restricted to management VLANs and approved identities

### Access Model
- Users and devices are placed into VLANs based on trust level and function
- Administrative access follows least-privilege principles
- Remote access is brokered through secure entry points (VPN / bastion / VDI)

This logical flow mirrors enterprise data center design by separating
**traffic direction**, **trust boundaries**, and **service exposure**.



---

## Design Notes
- Double NAT is intentional  
- This configuration provides isolation from the home network  
- Serves as a safe sandbox for segmentation and security testing  

The topology enables realistic enterprise scenarios while protecting the primary home network from experimentation risk.
