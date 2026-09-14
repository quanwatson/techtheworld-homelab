# Environments Overview

This document lays out the logical environments in the HomeLab — how they're separated, who governs what, and how they're expected to change over time. These aren't ad-hoc groupings; they're boundaries I use on purpose to manage risk, stability, and how fast things are allowed to change, the same way environments get handled in a real IT or MSP shop.

## The general approach

I follow a progressive environment model, balancing stability against experimentation on purpose rather than by accident. Household connectivity has to stay up no matter what I'm doing. Core infrastructure is protected from anything experimental. Changes go in incrementally and get validated. And environment boundaries are things I've actually written down — not just things I assume everyone (including future me) will remember.

## The environments

### 1. Home / household

Keeping daily internet access stable and uninterrupted for the household. This isn't managed as part of the lab — it gets minimal changes, gets treated as an external dependency, and is protected from anything I'm experimenting with. Design rule, no exceptions: lab activity never disrupts household connectivity.

### 2. LAB environment (the primary active one)

This is where the hands-on learning, validation, and controlled experimentation actually happens. It covers network segmentation on VLAN 10, pfSense routing and firewalling, switch configuration and hardening, and the Proxmox platform along with whatever infrastructure services sit on it.

It's actively changing, fully documented, change-controlled, and recoverable via console access if I lock myself out (which has happened). Think of it as production-inspired but explicitly non-production.

### 3. Management plane (planned)

Eventually this handles centralized management and control of infrastructure components — a dedicated management VLAN, restricted access paths, identity-based access control, and monitoring/logging endpoints. The goal is separating control traffic from workload traffic the way enterprise environments do, once there's enough here to justify it.

### 4. Services environment (planned)

This is where internal infrastructure services will live once the platform and network are actually stable — internal DNS, an internal certificate authority, Active Directory, and control-plane tooling (Odoo-based). Services get deployed after the foundation is proven, not before.

## How environments are allowed to talk to each other

Home to LAB traffic only goes through pfSense. LAB to Home is restricted and monitored. LAB to Management is controlled and least-privilege. Services to Management uses trusted, authenticated paths only. Nothing skips a hop just because it'd be more convenient.

## Change velocity by environment

| Environment | Change Velocity | Risk Tolerance |
|-----------|----------------|---------------|
| Home | None | Zero |
| LAB | Moderate | Controlled |
| Management | Low | Minimal |
| Services | Low–Moderate | Controlled |

Changes in a higher-risk environment don't propagate down into a lower-risk one without being validated first.

## Why bother with all this

Separating environments this explicitly buys safer experimentation, faster recovery when something breaks, cleaner fault isolation, and habits around change management that actually transfer to a real job. It's the same reasoning that keeps a household network stable while I mess with VLANs three feet away.
