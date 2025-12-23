# IP Addressing Plan

This document defines the current and planned IP addressing strategy for the home network and homelab.
Only **implemented networks** are treated as active. Planned ranges are explicitly labeled.

---

## Home Network (Existing)

**Purpose:** Household connectivity  
**Status:** Live / unmanaged by homelab  

- Gateway: `192.168.68.1`
- Subnet: `192.168.68.0/24`
- DHCP: Provided by Deco
- Notes:
  - Upstream of pfSense (intentional double-NAT)
  - No changes planned
  - Treated as external dependency

---

## Homelab Network (Active)

### VLAN 10 — LAB

**Purpose:** Lab systems and management  
**Status:** Active  

- Gateway: `192.168.10.1`
- Subnet: `192.168.10.0/24`
- DHCP: Provided by pfSense (`LAB_VLAN10`)
- Parent Interface: `LAN_CORE`

#### Static / Reserved Addresses

| Device              | IP Address        | Notes                         |
|---------------------|-------------------|-------------------------------|
| pfSense (VLAN 10)   | 192.168.10.1      | Homelab gateway               |
| switchOTS           | 192.168.10.101    | Switch management (DHCP)      |

> Static reservations for lab hosts will be added after switch-side VLAN enforcement is complete.

---

## Planned Networks (Not Implemented)

These networks are **design intent only** and are not active.

### VLAN 20 — IOT (Planned)
- Subnet: TBD
- Gateway: TBD
- Purpose: Isolated IoT and smart devices

### VLAN 30 — MGMT (Planned)
- Subnet: TBD
- Gateway: TBD
- Purpose: Dedicated infrastructure management

---

## Design Notes

- VLAN 1 is not used for management.
- VLAN 10 serves as the initial control and validation network.
- New VLANs will not be introduced until VLAN 10 is validated end-to-end
  (firewall, switch, client connectivity).
- Addressing favors clarity and debuggability over density.

---

## Change Control

Any modification to this plan requires:
- Validation of current network state
- Documentation update prior to implementation
- Corresponding Build Journal entry after execution
