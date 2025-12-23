# pfSense Interfaces and Cabling Plan

This document defines the physical cabling and logical interface roles for the pfSense firewall.
Only **implemented behavior** is treated as active. Design intent is clearly labeled.

---

## Hardware

- **Device:** Repurposed Untangle appliance
- **Storage:** 32 GB internal drive
- **Network Interfaces:** 2 × NICs
- **Role:** Dedicated homelab firewall and routing boundary

---

## Physical Cabling

| Interface        | Connected To            | Purpose                         |
|------------------|-------------------------|---------------------------------|
| WAN_UPSTREAM     | Deco LAN port           | Internet / upstream access      |
| LAN_CORE         | Homelab switch          | Internal homelab connectivity   |

Console access is retained for out-of-band recovery and initial configuration.

---

## Interface Assignment (Logical)

### WAN_UPSTREAM
- **Type:** Physical interface
- **Addressing:** DHCP
- **Subnet:** `192.168.68.0/24`
- **Gateway:** `192.168.68.1`
- **Role:** Upstream connectivity to the home network and ISP

### LAN_CORE
- **Type:** Physical interface (VLAN parent)
- **Base Address:** `192.168.1.1/24`
- **DHCP Range:** `192.168.1.100 – 192.168.1.199`
- **Role:** Parent interface for VLANs
- **Notes:** Not intended for long-term end-host usage

---

## VLAN Interfaces (Active)

### VLAN 10 — LAB
- **Parent Interface:** `LAN_CORE`
- **Gateway:** `192.168.10.1`
- **Subnet:** `192.168.10.0/24`
- **DHCP:** Enabled
- **Role:** Initial lab network and management access

---

## VLAN Interfaces (Planned)

These VLANs are **design intent only** and not yet implemented.

- **VLAN 20 — IOT**
  - Purpose: Isolated IoT and smart devices
- **VLAN 30 — MGMT**
  - Purpose: Dedicated infrastructure management

Addressing for planned VLANs will be defined only after VLAN 10 is validated end-to-end.

---

## Design Notes

- VLANs are terminated and routed on pfSense.
- Inter-VLAN routing is not active beyond VLAN 10.
- Switch-side trunking and access port enforcement are introduced incrementally.
- One layer (L3 or L2) is changed per session to reduce failure ambiguity.

---

## Change Control

Any changes to interface assignments, addressing, or cabling require:
- Validation of current state
- Documentation update prior to execution
- Corresponding Build Journal entry after completion
