# Phase 4 Logical Network Topology (Checkpoint)

## Purpose
This topology captures the current, validated network state prior to deploying the first core services on Proxmox.

It serves as:
- A documentation checkpoint
- A validation reference
- A baseline for future service-layer changes

## Scope (Current State Only)
- Internet / ISP (Cloud)
- pfSense firewall (WAN + LAN)
- Managed switch
- VLAN 10 (LAB)
- Proxmox host (pve01)
- Admin workstation

## Exclusions
- No future VLANs
- No service VMs
- No containers
- No external exposure

## Notes
- pfSense is represented by a router device for logical accuracy
- Cloud device simulates ISP Ethernet handoff
- Diagram reflects validated behavior, not planned architecture
