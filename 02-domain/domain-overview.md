# Domain Overview

This document is the source of truth for domain architecture in the lab: how the external (public) and internal (directory-based) domains are split, and why. It's the same split most MSPs and enterprises run, for the same reason — internal identity infrastructure has no business being reachable from the internet.

This split is what makes secure internal authentication possible, keeps services deployable from Proxmox without exposing anything by accident, and leaves room to grow toward MSP-style client environments and hybrid on-prem/cloud setups later. Nothing gets exposed publicly until it's documented and approved — no exceptions.

## The two domains

**External (public):** `techtheworld.win`, registered and managed through Cloudflare. This is for anything internet-facing — public sites, client portals, remote access endpoints down the line. Treated as zero-trust by default, since it's the internet.

**Internal (directory / identity):** `corp.techtheworld.win`, the Active Directory domain. Internal only, non-routable from the internet, no automatic trust with the external domain. Handles user and service-account authentication, computer/server identity, Group Policy, and internal DNS resolution.

## The rules that keep this clean

| Component | Rule |
|---------|------|
| External DNS | Managed exclusively via Cloudflare |
| Internal DNS | Managed via Active Directory-integrated DNS |
| AD Namespace | Subdomain of the external domain (this is standard practice, not a shortcut) |
| Internal Services | Never directly exposed to public DNS |
| Certificates | Internal CA for AD, public CA for external services |

Keeping it this rigid avoids namespace collisions and means the internal side can keep growing without ever having to think hard about the external side.

## Who owns what DNS-wise

Cloudflare handles `techtheworld.win` — public A/CNAME records, future reverse proxies, external TLS. Windows Server AD DNS handles `corp.techtheworld.win` — domain controllers, internal services, Proxmox-hosted infrastructure, private service discovery. They don't talk to each other; there's no split-brain DNS here.

## What's planned for Phase 4 and beyond

Active Directory Domain Services, AD-integrated internal DNS, an internal certificate authority, and a handful of Proxmox-hosted services — documentation systems, asset management, a password vault (an IT Glue alternative), automation tooling, and eventually some private AI services.

## Security posture, in plain terms

No split-brain DNS, no public exposure of AD services, no wildcard external records. Anything that gets published follows an explicit allow-only model — and needs a firewall rule, a DNS record, a documentation entry, and a build journal entry before it's real. If any one of those is missing, it doesn't happen yet.

## Where this stands against the roadmap

| Phase | Status |
|-----|------|
| Phase 1 – Network Foundation | Complete |
| Phase 2 – VLAN Enforcement | Complete |
| Phase 3 – Switch Hardening | Complete |
| Phase 4 – Service Enablement | In progress |

Next up: finalize the Proxmox deployment, stand up the first Windows Server domain controller, implement the internal DNS zone for `corp.techtheworld.win`, document the Cloudflare side (no records yet), and start planning the actual service catalog.

This file is the one to trust if anything elsewhere in the repo disagrees with it about domain structure.
