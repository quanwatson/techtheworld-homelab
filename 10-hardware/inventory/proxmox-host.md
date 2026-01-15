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

# Proxmox Storage Naming Conventions

## Purpose
Establish clear, consistent, and audit-friendly naming conventions for all Proxmox storage objects.

These conventions:
- Prevent ambiguity as the environment scales
- Align with MSP / enterprise audit expectations
- Make it immediately obvious what lives where and why
- Support clean rebuilds, migrations, and documentation review

Once locked, storage names are never repurposed for different roles.

---

## Storage Tiers Overview

Tier 0 (NVMe)
- Purpose: Hypervisor OS + core control-plane services
- Characteristics: Fast, reliable, low latency

Tier 1 (SATA HDD)
- Purpose: VM operating system disks (non-core workloads)
- Characteristics: Rebuildable, snapshot-friendly

Tier 2 (SATA HDD)
- Purpose: VM data disks and bulk storage
- Characteristics: Persistent data, lifecycle independent of OS

---

## Storage Object Naming Standard

Format:
<medium>-<role>-<scope>

Where:
- medium = nvme, hdd
- role = functional intent
- scope = logical usage boundary

---

## Defined Storage Objects

### Proxmox OS (implicit)
- Installed on NVMe
- 50 GB partition
- Not exposed as a general datastore

The Proxmox OS partition is intentionally excluded from VM storage pools.

---

### NVMe Core Services Datastore

Name:
nvme-core-services

Medium: NVMe  
Scope: Control-plane services only  

Allowed workloads:
- Internal Certificate Authority (CA)
- Internal DNS
- Secrets / credential management
- Odoo (IT Glue–like control service)
- Monitoring and automation control nodes

Disallowed workloads:
- Experimental VMs
- Bulk storage
- Media or backups
- NAS data

Rationale:
Fast storage reserved exclusively for services that define trust, identity, and control.

---

### HDD VM OS Datastore

Name:
hdd-vm-os

Medium: SATA HDD  
Scope: VM operating system disks  

Allowed workloads:
- Test VMs
- Lab servers
- Non-core infrastructure
- Disposable and experimental workloads

Rationale:
Separates OS lifecycle from data lifecycle and enables clean rebuilds.

---

### HDD VM Data Datastore

Name:
hdd-vm-data

Medium: SATA HDD  
Scope: VM-attached data disks  

Allowed workloads:
- Application data
- Service state
- Lab datasets

Rationale:
Allows OS rebuilds without data loss.

---

### NAS VM Backend Storage

Name:
hdd-nas-backend

Medium: SATA HDD  
Scope: Raw disk backing for NAS VM  

Usage model:
- Passed through or directly attached to NAS VM
- Not used for standard Proxmox VM disks

Rationale:
Preserves NAS semantics and avoids mixing hypervisor-managed and filesystem-managed storage.

---

## Naming Guardrails (Hard Rules)

- Storage names describe intent, not size
- Storage roles are never repurposed
- Core services never live on experimental storage
- Experimental workloads never live on nvme-core-services
- NAS storage remains isolated from hypervisor-managed VM disks

---

## Audit & Review Benefits

This model allows reviewers to:
- Identify service criticality at a glance
- Understand rebuild and recovery strategy immediately
- Trace data residency without tribal knowledge
- Scale the environment without renaming or cleanup debt

---

## Status
Storage naming conventions locked.  
Changes require a Change Control entry.
