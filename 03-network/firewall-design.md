# Firewall and Routing Design

Current firewall placement, interface roles, and security posture. I keep "what's actually live" and "what's planned" clearly separated here — it's too easy to write down the intended design and forget it isn't real yet.

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

## Why it's set up this way

Household stability comes first, full stop. Beyond that, this gets me a place to actually experiment with firewalling and segmentation, clean fault isolation between home and lab, and an edge-firewall placement that isn't far off from what a small business or MSP client site would run.

Any change to firewall rules, interfaces, or routing gets validated in isolation, documented before it happens, and logged in the Build Journal once it's done.
