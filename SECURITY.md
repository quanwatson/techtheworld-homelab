# Security

Security isn't a section I bolted onto this lab — it's most of the reason the lab exists. This page covers what's safe about publishing this repo publicly and how I think about security across the environment.

## Scope and repo safety

Everything in here is documentation and sanitized configuration references. No passwords, API keys, private keys, tokens, or credentials live in this repo — anywhere you see something that looks like a credential, it's a placeholder or has been redacted on purpose. This repo is meant to show architecture, process, and reasoning, not to expose anything live.

## How I think about security here

A few principles run through the whole design:

- **Least privilege.** Access is scoped by role, identity, and network zone — not "whoever's on the LAN gets in."
- **Segmentation.** VLANs and trust zones, deny-by-default between them.
- **Boundary enforcement.** Anything crossing a zone, or hitting the internet, goes through the firewall.
- **Controlled admin access.** Management traffic has its own restricted paths.
- **Observability.** Logging and monitoring where it actually matters, not everywhere for its own sake.
- **Resilience.** Backups exist, and I've actually tested that the restore path works.

## Access and exposure

I treat the household network and anything upstream of it as untrusted from the lab's point of view. Admin access happens over local management networks or (eventually) controlled remote-access paths — not by opening ports and hoping. Nothing gets exposed to the public internet without a documented reason and a change-control entry first, and if I ever do expose something publicly, it'll go through a real, auditable entry point rather than ad-hoc port forwarding.

## Guardrails I hold myself to

Security decisions get documented before implementation, not after. Any temporary exception is time-bound and gets reviewed — it doesn't quietly become permanent. When segmentation or identity controls are in tension with convenience, the controls win. And if a change ever weakens the security posture, it has to be justified, logged, and reversible — no silent trade-offs.

## Why this matters to me

This lab is where I practice actual security thinking: how systems should be designed, reviewed, operated, and recovered when it counts. What you're reading here is process and intent — not secrets, and not a target.
