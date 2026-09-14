# Planned VLAN Architecture

This defines the logical trust zones in the lab network. Each VLAN is its own security boundary — nothing gets implicit trust just for being on the same switch.

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

Nothing fancy here — it's just deny-by-default segmentation, done properly, so anything I add later has to earn its way through a rule instead of getting a free pass.
