# Firewall and Routing Design

This document describes the current firewall placement, interface roles, and security posture of the homelab.
Design intent is separated from future enhancements to maintain accuracy.

---

## pfSense Placement

pfSense is deployed **behind** the existing Deco home router and does **not** replace it.

- The Deco router remains responsible for:
  - ISP connectivity
  - Household device access
- pfSense functions as:
  - Homelab perimeter firewall
  - Layer 3 boundary for lab VLANs
  - NAT gateway for homelab traffic

This results in an **intentional double-NAT** topology.

---

## Interface Design

### WAN_UPSTREAM
- **Connection:** Deco LAN
- **Addressing:** DHCP (`192.168.68.x`)
- **Gateway:** `192.168.68.1`
- **Role:** Upstream internet access for homelab

### LAN_CORE
- **Connection:** Homelab switch (trunk/design intent)
- **Base Addressing:** `192.168.1.1/24`
- **Role:** Parent interface for VLANs
- **Notes:** Not intended for end-host usage long-term

### VLAN Interfaces (Active)

#### VLAN 10 — LAB
- **Gateway:** `192.168.10.1`
- **Subnet:** `192.168.10.0/24`
- **DHCP:** Enabled
- **Role:** Initial lab network and management access

---

## Security Principles (Current)

- The home network does **not** initiate access into the homelab.
- Homelab networks initiate outbound access through pfSense via NAT.
- No inbound port forwarding is configured on the Deco router.
- pfSense blocks unsolicited inbound traffic by default.
- Management access is currently:
  - Local (console)
  - Web GUI via LAB network
- Remote administrative access is **not yet exposed**.

---

## Security Principles (Planned)

These controls are **design intent only** and not yet active:

- Remote administrative access via secure overlay or VPN (e.g., Tailscale or pfSense VPN)
- Dedicated management VLAN for infrastructure access
- Explicit inter-VLAN firewall rules enforcing least privilege

---

## Routing Behavior

- pfSense performs:
  - Default routing for VLAN 10
  - NAT for outbound homelab traffic
- Upstream routing to ISP is handled entirely by the Deco router.
- No static routes are configured at this stage.

---

## Rationale

This design:
- Preserves household network stability
- Allows safe experimentation with firewalling and segmentation
- Enables clear fault isolation between home and lab
- Mirrors real-world edge firewall placement used in small enterprise and MSP environments

Changes to firewall rules, interfaces, or routing must be:
- Validated in isolation
- Documented prior to execution
- Recorded in the Build Journal after completion
