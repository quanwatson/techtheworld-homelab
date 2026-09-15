# Training Time Log
**File-of-record for logged training time — created 2026-09-14**

This is the companion log to *Master Training Program* §10a (Time-Logging Protocol) and the Training Time widget on the dashboard. Every row here is a session you confirmed was "training mode" — cert study, homelab work, OTS work, or leadership/architecture practice that counts toward this program. Sessions logged as "not training mode" (planning, dashboard maintenance, admin) aren't tracked here by design.

**How entries get added:** at the start of a session in the Homelab project, Claude asks whether you're in training mode. If yes, the session (or the off-screen work you describe) gets a row below, with duration as you report it. See §10a for the full protocol and why duration is self-reported rather than auto-tracked.

---

## Running Totals

| Metric | Value |
|---|---|
| **All-time hours logged** | 1 |
| **This week's hours** (week of 2026-09-14) | 1 |
| **Last logged session** | 2026-09-14 · Homelab · 1 hr |
| **Sessions logged** | 1 |

*(Totals update whenever a new row is added below — recompute by hand or ask Claude to "update the training log" and it will refresh both this table and the dashboard widget together.)*

---

## Log

| Date | Category | Duration | Summary |
|---|---|---|---|
| 2026-09-14 | Homelab | 1 hr | Omarchy install session on the OptiPlex daily driver (BJ-030): diagnosed Intel VMD hiding the new NVMe drive and fixed via AHCI, reset the `ots1` sudo password, redid `archinstall` after it silently picked systemd-boot instead of Limine, then hit an unresolved `gum-2.0.1-1` 404 from the Omarchy stable mirror. See `14-runbooks/runbook-omarchy-install.md`. |

---

## Category key

- **Cert study** — dedicated study/lab time toward AZ-900, MS-900, CCST, CCT, CCNA, AZ-104, MD-102, AB-650, AI-901, Security+, AZ-800/801, AZ-305 (§5–9, §9a)
- **Homelab** — hands-on rebuild/build-out work: pfSense, VLANs, Cisco switching, Proxmox, AI Gateway VLAN, etc. (§13)
- **OTS** — Ogun Tech Solutions business build, proof-of-work records, ADRs (§14, §19, §21)
- **Leadership / vCIO** — leadership modules (§18), vCIO Competency Track reps: roadmap drafting, QBR practice, vendor-negotiation reps (§18a)
- **Other** — anything training-relevant that doesn't cleanly fit the above; note what it was in the summary

## Weekly rollups

*(Populated at each monthly/quarterly review, §22 — a compact week-by-week total rather than re-deriving it from the full log every time.)*

| Week of | Total hours | Notes |
|---|---|---|
| 2026-09-14 | 1 | Program setup week — pre-kickoff (§5–9 Phase 0). First logged session: Omarchy install troubleshooting (BJ-030). |
