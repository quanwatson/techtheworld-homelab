# Architecture Overview

This document describes how the HomeLab is actually put together — how it's structured, why I split things up the way I did, and what assumptions shaped those decisions. This is design documentation, not a dump of live config output.

## Principles guiding the design

**Separation of concerns.** Each major responsibility is isolated so a failure in one place doesn't take down everything else and so troubleshooting stays simple. The firewall handles routing and security. Switching enforces Layer 2 boundaries. Virtualization hosts services — it doesn't do control logic. Management traffic and production traffic don't mix.

**Layered, one-thing-at-a-time changes.** Layer 3 (pfSense) gets validated before Layer 2 (switching). Core networking has to be stable before I deploy any services on top of it. Platform hardening happens before application workloads land. This is slower, but when something breaks I generally know which layer to start looking in.

**Documentation as the actual control plane.** Decisions get written down before implementation — not after, and not as an afterthought for style points. Runbooks, checklists, and logs are what govern execution and validation here. In a real sense, the repository itself is the control surface for this environment.

**Constraints, on purpose.** I'm working with legacy hardware, an older IOS version with real limitations, finite CPU/memory/storage, and a household connection that has to stay stable no matter what I'm doing in the lab. There's no "assume greenfield" here — every design has to work within what I've actually got, and that's treated as a training input, not a blocker.

## High-level layout

**Edge / firewall layer** — pfSense on dedicated hardware. Handles WAN connectivity, inter-VLAN routing, firewall policy enforcement, and DHCP/gateway services.

**Access / switching layer** — a Cisco Catalyst 3560 running IOS 12.2 IPBASE. Handles VLAN enforcement, trunking to pfSense, port-level security and hardening, and physical access control.

**Compute / virtualization layer** — Proxmox VE on a dedicated host. Hosts infrastructure services, isolates workloads via VMs, handles snapshotting and recovery, and will be the foundation for everything in later phases.

## Network segmentation

| VLAN | Purpose | Notes |
|-----|--------|------|
| 10 | LAB / Management | Primary management and lab traffic |
| 20 | IOT (planned) | Restricted device network |
| 30 | MGMT (future) | Dedicated management plane |
| 999 | Blackhole / Native | Disabled ports and native VLAN |

A few rules I hold to without exception: VLAN 1 never carries management traffic, the native VLAN stays unused and non-routable, trunks only carry the VLANs they actually need, and access ports are hardened and scoped rather than left wide open.

## Trust and identity boundaries

External trust is handled through Cloudflare for public DNS and TLS — nothing internal is exposed directly. Internally, there's a dedicated DNS namespace (`corp.techtheworld.win`), an internal certificate authority (planned), and service-to-service trust that's managed within the lab rather than borrowed from outside it. This mirrors how a lot of real organizations run hybrid trust models, which is intentional.

## How services get placed

Services get deployed based on role, not whatever's convenient at the time: one service per VM where it makes sense, infrastructure services before applications, control-plane services (DNS, CA, identity) kept isolated from everything else, and application services that never take on identity or trust responsibilities of their own. It's more setup work up front, but it keeps troubleshooting sane and leaves room to grow later.

## Assumptions about failure

I assume interfaces will get misconfigured, ports will err-disable, services will fail, and documentation will occasionally lag behind reality for a bit. What makes that survivable is console access paths, known-good baselines, incremental changes, and rollback procedures that are actually written down instead of remembered. Failure here is an expected state, not something that means I did it wrong.

## What this architecture is, and isn't

It's production-inspired, aware of its own constraints, documented well enough to review, and built to grow. It is not a high-availability production system, it's not optimized for peak performance, it's not locked to a particular vendor, and it's not designed to scale past a single operator running it.

## The point of it

This architecture is intentionally simple, explicit, and disciplined — not because simple is impressive, but because it's the version I can actually reason about end to end. If it shows anything, I'd want it to show sound infrastructure thinking, respect for operational risk, clear separation of responsibility, and documentation habits that would hold up on a real team.
