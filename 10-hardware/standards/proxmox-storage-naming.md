# Proxmox Storage Naming Conventions

Naming rules for storage objects on the Proxmox host — so six months from now I can look at a datastore name and know exactly what's allowed to live on it, without having to remember or guess. Once a name is locked, it doesn't get repurposed for something else later.

## Storage tiers

**Tier 0 (NVMe)** — hypervisor OS plus core control-plane services. Fast, reliable, low latency.

**Tier 1 (SATA HDD)** — VM operating system disks for non-core workloads. Rebuildable, snapshot-friendly.

**Tier 2 (SATA HDD)** — VM data disks and bulk storage. Persistent, and its lifecycle is independent of whatever OS disk it's attached to.

## Naming format

`<medium>-<role>-<scope>` — where medium is `nvme` or `hdd`, role is the functional intent, and scope is the logical usage boundary.

## The actual storage objects

**Proxmox OS (implicit).** Installed on NVMe, 50 GB partition, not exposed as a general datastore — this space isn't part of any VM storage pool.

**`nvme-core-services`** — NVMe, control-plane services only. Allowed: the internal CA, internal DNS, secrets/credential management, Odoo, monitoring and automation control nodes. Not allowed: experimental VMs, bulk storage, media, backups, NAS data. This is fast storage reserved for the services that define trust and identity — nothing else touches it.

**`hdd-vm-os`** — SATA HDD, VM operating system disks. For test VMs, lab servers, non-core infrastructure, anything disposable. Keeping OS lifecycle separate from data lifecycle is what makes rebuilds clean.

**`hdd-vm-data`** — SATA HDD, VM-attached data disks. Application data, service state, lab datasets. This is what lets an OS get rebuilt without losing the data that mattered.

**`hdd-nas-backend`** — SATA HDD, raw disk backing for the NAS VM specifically. Passed through or directly attached — never used for a standard Proxmox VM disk, since mixing hypervisor-managed and filesystem-managed storage defeats the point of a NAS.

## Rules that don't bend

Storage names describe intent, not size. Roles never get repurposed. Core services never land on experimental storage, and experimental workloads never land on `nvme-core-services`. NAS storage stays isolated from hypervisor-managed VM disks.

Done right, this means anyone reviewing the lab can tell what's critical at a glance, understand the rebuild/recovery story immediately, and trace where data actually lives without needing me to explain it.

**Status:** Locked. Changes go through Change Control.
