# Switching Overview

This directory documents switch inventory, management strategy, and VLAN/trunk design for the homelab.

This is **design and intent documentation**, not live configuration output.

## Current State
- One managed switch in use:
  - Cisco Catalyst 3560 (8-port PoE)
  - Hostname: `switchOTS`
- Switch is currently in a baseline state
- Management interface assigned via DHCP on VLAN 10 (LAB)

## Management Strategy
- Switch management is isolated to VLAN 10
- VLAN 1 is not used for management
- Console access retained as out-of-band recovery

## VLAN Strategy (Design)
- VLAN 10 — LAB (management and lab devices)
- VLAN 20 — IOT (planned)
- VLAN 30 — MGMT (planned, future)

No trunking or access port enforcement has been applied yet.
