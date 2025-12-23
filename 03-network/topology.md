# Network Topology (Baseline)

This document describes the baseline physical and logical topology of the homelab.  
The design prioritizes isolation, safety, and realism for enterprise-style testing while operating inside a home network.

---

## Home Network (Upstream)

**Role:** Household network and upstream internet access (external dependency)  
- **Gateway:** `192.168.68.1` (Deco)
- **Subnet:** `192.168.68.0/24`
- **DHCP:** Provided by Deco
- **Notes:** No changes planned. Treated as “upstream/ISP edge” for the lab.

---

## pfSense Firewall (Edge of Homelab)

**Role:** Homelab perimeter, routing, firewall policy, NAT  

### WAN_UPSTREAM
- **Addressing:** DHCP from upstream home network  
- **Current WAN IP:** `192.168.68.57` (DHCP) *(value may change)*  
- **Gateway:** `192.168.68.1`

### LAN_CORE
- **Role:** Parent interface for VLAN trunk to switch (design intent)  
- **Base addressing:** `192.168.1.1/24`
- **DHCP on LAN_CORE:** `192.168.1.100 – 192.168.1.199`  
- **Notes:** This subnet exists as a default LAN baseline. Lab traffic is intended to live on VLAN interfaces.

---

## Network Segmentation Status (Current)

### VLANs Implemented (Active)

#### VLAN 10 — LAB
- **Subnet:** `192.168.10.0/24`
- **Gateway:** `192.168.10.1` (pfSense `LAB_VLAN10`)
- **DHCP:** Enabled (pfSense)
- **Status:** Routed and operational at the firewall layer

---

## Switching Layer (Current)

### Managed Switch
- **Device:** Cisco Catalyst 3560
- **Hostname:** `switchOTS`
- **Management VLAN:** VLAN 10 (LAB)
- **Management IP:** `192.168.10.101` (DHCP)
- **Access Methods:** Console + Web GUI confirmed

### Switch Integration Status
- Switch is reachable and managed on VLAN 10.
- VLAN tagging / trunk enforcement for client ports is **not yet fully applied**.
- Switch changes will be introduced incrementally to avoid multi-variable failures.

---

## Physical Topology (High-Level)

- **Internet/ISP**
  → **Deco Router (192.168.68.1)**
  → **pfSense WAN_UPSTREAM (DHCP)**
  → **pfSense LAN_CORE (parent)**
  → **Catalyst 3560 `switchOTS`**
  → **LAB clients (VLAN 10) as ports are assigned/validated**

---

## Logical Flow

The logical flow represents how traffic, trust, and services are intended to move through the environment, independent of physical cabling.

### North–South Traffic (External)
- Household internet traffic terminates at the Deco router
- Homelab traffic egresses through pfSense (`WAN_UPSTREAM`)
- pfSense performs NAT and enforces firewall policy at the homelab boundary
- External exposure is denied by default unless explicitly configured

### East–West Traffic (Internal)
- Inter-VLAN routing will occur on pfSense once additional VLANs are implemented
- All inter-VLAN communication is intended to be **explicitly controlled** via firewall rules
- No VLAN is trusted by default; segmentation is policy-driven

### Service Access Flow (Planned)
- Core services (DNS, directory, monitoring) will be placed into controlled segments
- Management access will be restricted to approved sources and identities
- Remote access will be brokered through secure entry points (VPN / bastion)

---

## Design Notes

- **Double NAT is intentional** (home network upstream + pfSense NAT)
- Protects household network from lab experimentation risk
- Provides a safe sandbox for segmentation, firewalling, and enterprise-style testing

This topology enables realistic network scenarios while maintaining home network stability.
