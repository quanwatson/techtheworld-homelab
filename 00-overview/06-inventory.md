# Inventory Overview

## Purpose of This Document

This document provides a **high-level inventory snapshot** of core HomeLab assets.

It is intentionally concise and human-readable.  
Detailed hardware specifications, serials, and lifecycle data live in dedicated inventory records under:

➡️ `hardware/inventory/`

This mirrors professional practice where:
- Executive views summarize assets
- Detailed inventories are stored separately

---

## Core Infrastructure Assets

### Domains
- **External Domain:** `techtheworld.win`
- **Internal Namespace:** `corp.techtheworld.win`

---

### Compute & Endpoints
- **Primary Authoring / Remote Desktop:** Dell OptiPlex 3080  
- **Virtualization Host:** Lenovo ThinkCentre M720s (Proxmox VE planned)
- **Thin Client / Terminal:** Raspberry Pi (role TBD)

---

### Network Infrastructure
- **Firewall / Router:** Repurposed Untangle hardware (pfSense)
- **Switch:** Cisco Catalyst 3560 (8-port, managed)
- **Wireless Access Point:** TBD (planned phase)

---

## Inventory Governance

- This file is a **summary view only**
- No serial numbers or sensitive details are stored here
- Updates occur only when:
  - A core asset is added, removed, or repurposed
  - Roles change meaningfully

Detailed inventory records are treated as operational artifacts and versioned separately.

---

## Summary

This inventory reflects the **current, intentional scope** of the HomeLab.

It supports:
- Architectural clarity
- Reviewer orientation
- Professional documentation standards

As the lab evolves, this overview will remain concise while detailed records scale independently.
