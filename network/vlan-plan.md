# Planned VLAN Architecture

The VLAN architecture defines logical trust zones within the lab network.  
Each VLAN represents a distinct security boundary with **no implicit trust** between segments.

---

## VLAN 10 — LAB
- **Purpose:** Test systems, Proxmox, experiments
- **Subnet:** 192.168.10.0/24

## VLAN 20 — IOT
- **Purpose:** Smart devices and low-trust equipment
- **Subnet:** 192.168.20.0/24

## VLAN 30 — MGMT
- **Purpose:** Network management interfaces and administrative access
- **Subnet:** 192.168.30.0/24

---

## Design Notes
- All VLANs are routed by pfSense  
- Inter-VLAN traffic is explicitly controlled by firewall rules  
- No VLAN has implicit trust  
- Access between VLANs is granted only where justified and documented  

This model supports enterprise-style segmentation, security testing, and controlled service exposure.
