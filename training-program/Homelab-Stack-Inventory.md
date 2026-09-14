# Homelab & Infrastructure Stack Inventory
**Confirmed 2026-09-13 — supersedes earlier hardware references in the Index doc and the training program**

This is the file-of-record for what physically and virtually makes up the homelab/OTS infrastructure. Update it in place whenever hardware or services change — this is where "what do I actually have" gets answered, separate from the training-program calendar in *Master Training Program*.

## One correction worth flagging

Earlier project notes (Index doc, training program v1) referred to an "RTX 3080 desktop" as the daily-driver box. Per this inventory and the existing *Omarchy-Dual-Boot-Runbook* doc, that machine is actually a **Dell OptiPlex 3080** (the model number) running a **GTX 1060 6GB** (not an RTX 3080 GPU) — the two "3080"s were getting conflated. Treat the spec below as authoritative going forward.

## Physical Compute

| Device | Spec | Role |
|---|---|---|
| Dell OptiPlex 3080 | GTX 1060 6GB, 32GB RAM, Omarchy (Arch/Hyprland) | Daily-driver workstation |
| Mac Pro (2013, "trash can") | — | Go-to Mac creative workstation |
| Lenovo box | — | Proxmox virtualization host |
| pfSense box | dedicated appliance | Perimeter firewall/router |
| Cisco switch | 8-port | LAN switching / VLAN trunking |
| Raspberry Pi #1 | — | Remote-lab thin client (dual-purpose candidate for in-office smart assistant) |
| Raspberry Pi #2 | Linux/Android-flavored OS | Dedicated entertainment box — retro gaming, game streaming, media player |

*(HP EliteBook + Dell WD19 dock, referenced in the original Index doc as the remote-access laptop, is assumed still current — not re-confirmed in this pass.)*

## Cloud / Rented Compute

| Service | Purpose |
|---|---|
| RunPod | On-demand GPU rental for large model workflows (the ComfyUI/Muse video-generation pipeline — see *ComfyUI-Muse-Workflow-Notes* — not the homelab's local-first AI Gateway, which stays homelab-hardware-only per the locked architecture) |
| Hostinger KVM 4/8 | VPS for public-facing workflows/hosting |

## Network, Security & Access

| Tool | Role |
|---|---|
| pfSense | Perimeter routing/firewall, VLAN gateway |
| Cisco 8-port switch | LAN switching, VLAN trunking |
| Cloudflare | DNS/CDN/tunnel — likely fronting the Hostinger VPS and any other public-facing service |
| Tailscale | Mesh VPN tying the home network, cloud VPS, and Mac Pro together for private remote access |

## AI / Productivity Tooling

| Tool | Purpose |
|---|---|
| Claude Pro | Planning, coaching, and general AI-assisted work (this program) |

## Notes for the training program

- This stack is genuinely good CCNA/CCST/Security+ practice material once rebuilt: pfSense + VLANs + Cisco switching is core to Phase 2/2b/3, and Tailscale + Cloudflare are a real-world, hands-on introduction to Zero Trust/remote-access concepts ahead of the Security Architecture skill (currently 0/5).
- RunPod and Hostinger don't conflict with the "local-first AI, no Claude API/no per-call billing" architecture already locked in for the AI Gateway VLAN — they're serving the separate creative-AI-video track, not the homelab AI assistant.
- Proxmox now has a confirmed home (the Lenovo box) — Skill 10 (Virtualization, currently 1/5) has a concrete target machine rather than an abstract plan.
