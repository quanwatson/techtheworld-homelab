# Runbook: Omarchy Install (Dell OptiPlex, GTX 1060 6GB)

**Renamed 2026-09-14** — was framed as a dual-boot runbook. Dropped "dual-boot" from the framing because it no longer reflects the plan: the Windows-side drive has been physically removed and this is now a **single-OS Omarchy build**. History below is kept as-is, including the earlier dual-boot framing, since it's still the accurate record of how this build got here.

## Purpose
Get the Dell OptiPlex (daily-driver / remote-workstation box, GTX 1060 6GB, Pascal architecture) running Omarchy (Arch + Hyprland) as its only OS, with the Nvidia driver and remote-access stack (Sunshine + Moonlight) working on top of it.

## Scope
- In scope: disk/BIOS prep, `archinstall`, the Omarchy post-install layer, Nvidia driver setup for this Pascal-generation GPU, validating the box as a daily driver.
- Out of scope as of Attempt 3: Windows dual-boot (see Section "Attempt 3" below — the Windows-side drive is physically gone).

## Current Status (as of BJ-030, 2026-09-14)
**Attempt 3, in progress — paused, blocked.** All prior drives removed; a single new 512GB M.2 NVMe is the sole drive, used whole-disk. `archinstall` has been completed (redone once to correctly select Limine as the bootloader). The Omarchy installer is mid-package-install, blocked on a `gum-2.0.1-1-x86_64.pkg.tar.zst` 404 from `stable-mirror.omarchy.org`. Posted to the Omarchy Discord for help; unresolved as of session end. GPU driver setup has not started this attempt.

---

## Standing rule (carried forward from the Attempt 1 postmortem)

**Do every post-install step — Omarchy's installer, Nvidia setup, all config edits — logged in as the real desktop user, never as `root`.** Use `sudo` from that user's session instead of switching to a root login shell. Root-only configuration was the confirmed root cause of Attempt 1's graphical-login crash-loop (see below) — fixes landed in `/root` instead of the real user's home, so the greeter kept loading an unconfigured session.

---

## Postmortem: Attempt 1 (abandoned)

Installed onto the original 931.5GB games drive, alongside Windows, via `archinstall` manual partitioning + Omarchy applied as a post-install layer. Reached a fully-rendering desktop but was ultimately abandoned. Two distinct problems, in order:

1. **Root cause of the graphical-login crash-loop:** all post-install configuration (Nvidia driver setup, env vars, Hyprland config edits) had been done while logged in as `root`, not the actual desktop user (`ots1`) the graphical greeter logs in as. `root`'s home (`/root/.config/hypr`, `/root/.local/share/omarchy`, `/root/.config/omarchy`, `/root/.local/state/omarchy`) had all the fixes; `ots1`'s home had none of it. Confirmed by running `Hyprland` raw from a TTY as `ots1` and watching it auto-generate a stub config. Fixed for that attempt by copying all four directory trees from `/root` to `/home/ots1` and `chown -R ots1:ots1`, which got Hyprland to a fully-rendering desktop with one non-fatal error.
   - Also found: `ots1` had no sudo/wheel access at all during Attempt 1 — non-blocking since root was directly reachable, but confirm sudo/wheel is granted during account creation going forward.
2. **Unresolved, install-ending issue:** immediately after the fix above, the next full reboot hit a **LUKS disk-unlock failure** — passphrase entry produced a few seconds of black screen, then looped back to the same unlock prompt. This happens before any userspace/desktop code runs, so it's architecturally independent of the Hyprland/user-config issue above. Suspected passphrase/keyboard-layout mismatch, never confirmed. Rather than keep debugging blind through photographed TTY output, wiped and reinstalled from scratch.

**Carried forward as confirmed-working, not in question:** `nvidia_drm.modeset=1` via `/etc/kernel/cmdline` + `sudo mkinitcpio -P` (capital P) is the correct, persistent way to set that kernel parameter — direct edits to `/boot/limine.conf` get silently overwritten by the `limine-mkinitcpio` hook. `nvidia-dkms` (not `nvidia-open-dkms`) is the correct driver package for this Pascal-generation GTX 1060.

---

## Attempt 2 (historical, superseded by a hardware change before resolution)

Added a dedicated 240GB Kingston SSD (`/dev/sdb`, `KINGSTON SQ500S37240G`) so Omarchy no longer shared the games drive with Windows. The Seagate `ST1000LM035-1RK1` 931.5GB HDD (`/dev/sda`) was left untouched.

`archinstall` on `/dev/sdb`: Btrfs with the standard subvolume split (`@` → `/`, plus `@home`/`@var`/`@snapshots`), zstd compression, **no LUKS** (removed as a variable after Attempt 1's unresolved unlock failure), **Limine** bootloader, user `ots` created with sudo/wheel requested. Completed without errors.

**Password/login saga (resolved):**
- `passwd ots <password> <password>` fails — `passwd` doesn't take the new password as CLI arguments, it prompts interactively (twice, hidden). Run `passwd ots` alone.
- `sudo` then rejected the real password (which contained `!`) inside the Omarchy install script — suspected keyboard-layout mismatch, same family of issue as the Attempt 1 LUKS suspicion. Worked around by resetting to an alphanumeric-only password to confirm sudo/login mechanics worked at all.

**Blocker that ended Attempt 2** — the Omarchy installer halted mid-script:
```
grep: /boot/limine.conf: Permission denied
sudo: limine-update: command not found
Error: failed to add boot entries to /boot/limine.conf
Failed script: /home/ots/.local/share/omarchy/install/login/limine-snapper.sh
```
Not a sudo/password issue (earlier steps in the same run used sudo successfully). The `limine-snapper.sh` step — which wires Btrfs/Snapper snapshots into the Limine boot menu — couldn't read `/boot/limine.conf` and couldn't find `limine-update` even under sudo. Likely a package/version mismatch or a `/boot` mount/permission state the script doesn't expect. **Not resolved** — superseded when the hardware change below happened before diagnostics were run. If a future attempt hits the same failure, the queued diagnostics are:
```bash
pacman -Q | grep limine
which limine-update
ls -la /boot/
mount | grep boot
```

---

## Attempt 3 (current) — hardware change, drive visibility, and the archinstall/Omarchy redo

### Hardware change
Both prior drives (Kingston 240GB SSD, Seagate 931.5GB HDD) were physically removed from the system. A single new **512GB M.2 NVMe drive** was installed as the sole drive, intended for whole-disk use. **This machine is now single-OS Omarchy — Windows dual-boot is retired from scope for this build.**

### Drive-visibility issue — resolved
BIOS correctly detected the new M.2 drive. An Ubuntu live session did not show it at all in `lsblk`/`fdisk -l`.

Diagnosed with:
```bash
lspci | grep -iE "nvme|non-volatile|raid|vmd"
```
which returned:
```
00:17.0 RAID bus controller: Intel Corporation Device a386
```
`a386` is Intel's **VMD (Volume Management Device)** controller — when active, it hides the NVMe drive from a plain Linux kernel unless VMD-aware boot/kernel support is present. Fix: since no Windows/RAID dependency remains to protect (all other drives are gone), disabled VMD outright — reboot into BIOS, switch the SATA/NVMe controller mode from **RAID/VMD to AHCI** (on this Dell OptiPlex, under System Configuration → SATA Operation, or Advanced → Intel VMD Controller depending on BIOS version), save, reboot, re-confirm with `lsblk`/`fdisk -l`.

*(Secondary note: plain `dmesg` failed with "Operation not permitted" in the live session — needed `sudo dmesg | grep -i nvme`. Not chased further once `lspci` gave the answer.)*

- [x] BIOS controller mode switched from RAID/VMD to AHCI
- [x] Drive visible in `lsblk`/`fdisk -l` after the switch

### archinstall — completed (redone once)
Ran `archinstall`: Btrfs with subvolumes, zstd compression, no LUKS, Limine bootloader, sudo-enabled user `ots1` created during setup.

- `ots1`'s sudo/login password was rejected post-install. Fixed by logging in as `root` and running `passwd ots1`, resetting to an **alphanumeric-only password** to rule out a keyboard-layout mismatch on symbol characters (same family of issue as Attempt 1/2).

Started the Omarchy installer (`curl -fsSL https://omarchy.org/install | bash`), logged in as `ots1` per the standing rule, not root:
- Hit a `linux-firmware-other` vs `linux-firmware-ti` package file conflict. Fixed with `sudo pacman -Syu`.
- Installer then warned **"Omarchy install requires: Limine bootloader."** Diagnosed:
  ```bash
  pacman -Q | grep limine      # empty
  cat /boot/limine.conf        # missing
  efibootmgr -v                # showed systemd-bootx64.efi
  ```
  Confirmed `archinstall` had actually installed **systemd-boot**, not Limine, despite Limine being the intended/selected choice on the bootloader screen.
- **Redid `archinstall` from scratch**, this time explicitly confirming Limine on the bootloader screen rather than accepting whatever was pre-highlighted.

### Current blocker — unresolved
On the redo: user creation and the firmware conflict cleared cleanly again, the Omarchy repo cloned, and package installs started — then hit:
```
gum-2.0.1-1-x86_64.pkg.tar.zst — 404 from stable-mirror.omarchy.org
```
Tried `sudo pacman -Syyu` (forced database refresh) — did not resolve it. **Unresolved as of session end.** Posted to the Omarchy Discord: "gum-2.0.1-1 404 error from stable-mirror.omarchy.org during install."

- [x] All prior drives (Kingston SSD, Seagate HDD) physically removed
- [x] New 512GB M.2 drive installed, whole-disk target
- [x] Drive visible in BIOS and in a live session (post-AHCI fix)
- [x] `archinstall` completed with Limine confirmed as bootloader
- [x] `ots1` password reset, sudo confirmed working
- [ ] Omarchy package install completed — **blocked on `gum` 404 mirror error**
- [ ] Omarchy/Hyprland desktop booted
- [ ] Nvidia driver + env vars + kernel param set (not started this attempt)

---

## Pending: Nvidia driver setup (GTX 1060 6GB, Omarchy side)

**Not yet started this attempt — queued for once the `gum` blocker clears.**

**Critical: use the proprietary driver, not the open one.** Nvidia's open kernel modules (`nvidia-open-dkms`) only support Turing and newer. The GTX 1060 is Pascal — it requires the closed/proprietary `nvidia-dkms` package. Do this step logged in as the real desktop user, not root.

```bash
sudo pacman -S nvidia-dkms nvidia-utils lib32-nvidia-utils egl-wayland
```

Add to Hyprland env config (`~/.config/hypr/envs.conf`):
```
env = LIBVA_DRIVER_NAME,nvidia
env = GBM_BACKEND,nvidia-drm
env = __GLX_VENDOR_LIBRARY_NAME,nvidia
env = NVD_BACKEND,direct
```

Add kernel parameter `nvidia_drm.modeset=1` via `/etc/kernel/cmdline` — **never edit `/boot/limine.conf` directly**, it's auto-regenerated from `/etc/kernel/cmdline` by a Limine mkinitcpio hook and gets silently overwritten:
```bash
sudo sed -i 's/$/ nvidia_drm.modeset=1/' /etc/kernel/cmdline
sudo mkinitcpio -P
```
Reboot and confirm with `nvidia-smi`.

---

## Validation checklist (once unblocked)

- [ ] Boot into Omarchy, confirm GPU acceleration works (`glxinfo`/`hyprctl` reports Nvidia)
- [ ] `nvidia-smi` reports the GTX 1060 correctly post-reboot
- [ ] Graphical login succeeds without crash-looping
- [ ] Install and test Sunshine + Moonlight connection
- [ ] Confirm nothing on the separate Windows GPU-workstation node in the AI Gateway VLAN was affected
- [ ] Update `10-hardware/inventory/optiplex-3080.md` with final storage/OS specs once confirmed

---

## Troubleshooting quick reference

| Symptom | Likely cause | Fix |
|---|---|---|
| New M.2/NVMe drive visible in BIOS but missing entirely from `lsblk`/`fdisk -l` in a live session | Intel VMD (Volume Management Device) RAID controller active (`lspci` shows a RAID bus controller, device ID `a386`), hiding the drive from a kernel without VMD support | Switch BIOS SATA/NVMe controller mode from RAID/VMD to AHCI, reboot, re-check |
| `passwd` run as `passwd user newpass newpass` throws a usage error | `passwd` doesn't take the new password as CLI args — it prompts interactively | Run `passwd user` alone, type the new password twice at the hidden prompts |
| `sudo`/login rejects a password containing symbols (e.g. `!`), plain alphanumeric works | Suspected keyboard-layout mismatch at that point in boot/session | Set a temporary alphanumeric-only password to confirm mechanics work, then check `localectl status` / Hyprland's `input.conf` `kb_layout` before reintroducing symbols |
| Omarchy installer stops with a package file conflict (e.g. `linux-firmware-other` vs `linux-firmware-ti`) | Stale/partial package state | `sudo pacman -Syu` |
| Installer warns "Omarchy install requires: Limine bootloader" after `archinstall` claimed Limine was selected | `archinstall`'s bootloader screen defaulted to systemd-boot instead of the intended selection | Confirm with `pacman -Q \| grep limine`, `cat /boot/limine.conf`, `efibootmgr -v`; if it shows `systemd-bootx64.efi`, redo `archinstall` and explicitly select Limine rather than accepting the pre-highlighted option |
| Omarchy installer halts at `.../install/login/limine-snapper.sh` with `grep: /boot/limine.conf: Permission denied` and `sudo: limine-update: command not found` | Not fully diagnosed (Attempt 2) — specific to that script expecting a `limine-update` binary not on PATH, and/or a `/boot` permission state it doesn't handle | Diagnose with `pacman -Q \| grep limine`, `which limine-update`, `ls -la /boot/`, `mount \| grep boot`; installer's own "Retry installation" is worth trying once first |
| Package install 404s from `stable-mirror.omarchy.org` (e.g. `gum-2.0.1-1-x86_64.pkg.tar.zst`) | Unresolved — suspected stale mirror index | `sudo pacman -Syyu` (forced refresh) did not resolve it; posted to the Omarchy Discord — **check for a response before retrying blind** |
| Graphical login accepts password, screen flashes/loops back | Wrong Nvidia driver package (`nvidia-open-dkms` doesn't support Pascal) | Install `nvidia-dkms` instead, set env vars + kernel param, `mkinitcpio -P`, reboot |
| Kernel param added to `/boot/limine.conf` directly vanishes | File is auto-regenerated from `/etc/kernel/cmdline` by a Limine hook | Edit `/etc/kernel/cmdline` instead, then `sudo mkinitcpio -P` |
| Graphical greeter crash-loops even though config looks right | Fixes were applied as `root`, not the real desktop user the greeter logs in as | Always work as the real user with `sudo`; if already broken, copy the four Omarchy/Hypr config trees from `/root` to the real user's home and `chown -R` |
| Desktop user has no sudo access | Not added to `wheel` during `archinstall` | Grant sudo/wheel explicitly during account creation; verify with a harmless `sudo` command right after first login |
| LUKS unlock: passphrase entered, black screen, loops back to prompt | Unresolved (Attempt 1) — suspected passphrase/keyboard-layout mismatch | Attempts 2+ skip LUKS entirely to remove the variable |

---

## References

- [Dual Boot Install — The Omarchy Manual](https://omarchy.org/manual/dual-boot-install/) — kept for reference; not currently applicable, single-OS build
- [Recommended BIOS Settings for your Linux System | Dell US](https://www.dell.com/support/kbdoc/en-us/000123462/recommended-bios-settings-for-your-linux-system)
- [Omarchy Secure Boot + Windows Dual Boot Setup guide · basecamp/omarchy · Discussion #5306](https://github.com/basecamp/omarchy/discussions/5306) — kept for reference; not currently applicable
- [[SOLVED] RST Issue with Dell OptiPlex 3070 - Linux Mint Forums](https://forums.linuxmint.com/viewtopic.php?t=413671)
- [Guide: Dual boot Omarchy Os with Windows 11 · basecamp/omarchy · Discussion #2479](https://github.com/basecamp/omarchy/discussions/2479) — kept for reference; not currently applicable
- [Can't stream a headless monitor created with Hyprland · Issue #2955 · LizardByte/Sunshine](https://github.com/LizardByte/Sunshine/issues/2955)
- [Omarchy Discord](https://discord.gg/tXFUdasqhY) — used to report the `gum-2.0.1-1` mirror 404, current open item
