# Proxmox Host – Hardware Baseline

## Overview
This document defines the **authoritative hardware baseline** for the primary Proxmox virtualization host used in the TechTheWorld Homelab.

This host serves as the foundation for:
- Core infrastructure services
- Internal PKI (Certificate Authority)
- Internal DNS
- Odoo-based IT control plane
- Future Windows Server AD integration
- Linux-based service workloads

---

## System Identification
- **Manufacturer:** Lenovo  
- **Model:** ThinkCentre M720s  
- **Machine Type (MTM):** 10SUS0AT00  

---

## BIOS / Firmware
- **BIOS Version:** M1UKT77A  
- **BIOS Release Date:** 04/10/2024  
- **BIOS Manufacturer:** Lenovo  

> BIOS verified current prior to Proxmox deployment.

---

## CPU
- **Processor:** Intel® Core™ i5-9500  
- **Base Clock:** 3.00 GHz  
- **Max Turbo:** 4.40 GHz  
- **Cores / Threads:** 6 / 6  

### CPU Capabilities
- VT-x: Supported  
- VT-d (IOMMU): Supported  
- AES-NI: Supported  
- AVX / FMA: Supported  

> CPU fully supports virtualization, encryption, and containerized workloads.

---

## Memory
- **Total Installed:** 48 GB  
- **Type:** DDR4  
- **Channel Mode:** Dual-Channel  
- **Max Rated Speed:** 2667 MT/s  
- **Current Speed:** 2400 MT/s  

> Memory capacity provides significant headroom for concurrent VMs, containers, and future AI workloads.

---

## Storage Layout

### NVMe (Primary)
- **Vendor:** Micron  
- **Model:** 2200S NVMe  
- **Capacity:** 256 GB  
- **Use Case:**  
  - Proxmox VE OS  
  - ISO storage  
  - Lightweight system VMs  

### SATA HDD #1
- **Vendor:** Western Digital  
- **Model:** WD10JPVX  
- **Capacity:** 1 TB  
- **RPM:** 5400  
- **Use Case:**  
  - VM storage  
  - Application data  
  - Internal services  

### SATA HDD #2
- **Vendor:** Seagate  
- **Model:** ST1000LM035  
- **Capacity:** 1 TB  
- **RPM:** 5400  
- **Use Case:**  
  - Backups  
  - Cold storage  
  - Future ZFS mirror consideration  

---

## Networking
- **Primary NIC:** Onboard Ethernet  
- **MAC Address:** 6C-4B-90-E2-D0-AB  
- **Switch:** Cisco Catalyst 3560 (`switchOTS`)  
- **VLAN:** VLAN 10 (LAB)  

---

## Status
- **Hardware Baseline:** LOCKED  
- **Change Control:** Any hardware changes require a new Build Journal entry  
- **Phase Alignment:** Phase 4 – Service Enablement  

