# Device Record — OptiPlex 3080

## Role(s)
- Primary lab host (VMs/services)
- Remote workstation service (Sunshine/Moonlight)
- Daily-driver desktop

## Verified specs (from current context)
- CPU: 6-core 8th-gen Intel i7 (exact model: TBD)
- RAM: 32 GB
- GPU: GTX 1060 6GB (Pascal) — see note below on the earlier GTX 1050 Ti / RTX 3080 confusion
- Storage: single 512GB M.2 NVMe (whole-disk) — as of 2026-09-14, both prior drives (Kingston 240GB SATA SSD, Seagate 931.5GB SATA HDD) were physically removed
- OS/Hypervisor: Omarchy (Arch + Hyprland), single-OS — **install in progress, currently blocked; not yet booted to a working desktop.** See `14-runbooks/runbook-omarchy-install.md` and `01-logs/build-journal.md` BJ-030 for full status/history.

> **Note:** `training-program/Homelab-Stack-Inventory.md` (confirmed 2026-09-13) lists this same machine's GPU as a GTX 1060 6GB running Omarchy (Arch/Hyprland), and calls itself authoritative over earlier hardware references (this record previously showed a GTX 1050 Ti). This record has been updated to match that spec. Windows dual-boot is retired from scope as of the 2026-09-14 hardware change (see BJ-030) — this is now a single-OS Omarchy build.
