# Master Training Program — Solutions Architect + vCIO Track
**36-Month Edition — issued 2026-09-13 · Program kickoff 2026-10-05 · Target close ~2029-11-05**

---

## 1. Executive Overview

This is the control document for a 36-month transformation from L1 Support Engineer (MSP, ~4 years experience) toward Sr. Solutions Architect and/or vCIO, running in parallel with the Ogun Tech Solutions (OTS) business build and a from-scratch homelab rebuild. Year 1 (the original 12-month plan) still stands on its own as an L1→L2/Systems Engineer bridge; Years 2–3 (added 2026-09-13, §3/§9a/§18a) extend it toward the dual Sr. Solutions Architect/vCIO capstone.

**What changed from the original plan (July 4, 2026 version):**

| Item | Original | Re-baselined |
|---|---|---|
| Kickoff | July 4, 2026 | **October 5, 2026** (your instruction) |
| Certifications completed pre-kickoff | assumed 0 | confirmed 0 — clean start |
| Homelab state | Phase 3.7 complete, Phase 8 in progress | **full rebuild from zero** — phase counter resets |
| Study tools on hand | not specified | **CBT Nuggets + Cisco Packet Tracer already available** — no acquisition delay |
| MS-102 | in original 9-cert list | **retiring Oct 2026 — replaced with AB-650** (see §3) |
| CCT Collaboration + CCT Routing | in original 9-cert list | **recommended swap to CCST Networking + CCST Cybersecurity** (see §3) |
| 9 certs in strict 12 months | assumed feasible | **not realistic without cramming — see honest capacity math below** |
| AI-901 (Azure AI Fundamentals) | not in original list | **added as cert #10**, added 2026-09-13 at your request — see §3 |
| CCT Collaboration + CCT Routing & Switching | recommended swap to CCST (above) | **added back, alongside CCST** — you do field network technician work as well as remote MSP support, so both tracks are job-relevant. Now 12 certs total. See §3 addendum. |

**The one hard call this document makes, up front:** the certification list plus a full homelab rebuild plus OTS plus a leadership track, inside 8–14 hours/week, does not fit into 52 weeks without either cramming or quietly dropping quality. Rather than pretend it does, this plan completes **9 of the 12 certifications in Year 1** (AZ-900, MS-900, CCST Networking, CCST Cybersecurity, CCT Collaboration, CCT Routing & Switching, CCNA, AZ-104, MD-102) and carries **AB-650 (MS-102's replacement), AI-901, and Security+ into the first quarter of Year 2**, which is exactly where Part 24's "Year-2 advanced roadmap" already expected the program to extend. This is a re-baseline, not a scope cut — every certification in your original list is still in the plan, plus two additions; Year 1 now runs about 5 weeks longer (closing 2027-11-08 instead of 2027-10-04) to hold the two added CCT exams without compressing anything else. See §26 (Risk Register) for the capacity math.

Governing principle for the whole document, restated from your brief: **CONSISTENCY > INTENSITY.**

---

## 2. Current-State Assessment (as of 2026-09-13)

- **Role:** L1 Support Engineer, MSP, ~4 years experience, 40 hr/week (8am–5pm)
- **Certifications held:** none yet
- **Homelab:** being rebuilt from scratch. Whatever Phase 3.7/Phase 8 state exists in older project notes is **superseded** — treat this program's homelab phase counter as starting fresh at Phase 0. **Full confirmed hardware/service inventory as of 2026-09-13 lives in the companion doc *Homelab & Infrastructure Stack Inventory*** — Dell OptiPlex 3080 (GTX 1060 6GB, 32GB RAM, Omarchy) as daily driver, Mac Pro 2013 as creative workstation, a Lenovo box for Proxmox, a dedicated pfSense box, an 8-port Cisco switch, two Raspberry Pis (one thin client, one dedicated retro/streaming/media box), plus RunPod, Hostinger KVM 4/8, Cloudflare, Tailscale, and Claude Pro in the cloud/service layer. This corrects the earlier "RTX 3080 desktop" reference — see that doc for the full note. The rebuild is a reconfiguration/reinstall effort, not a re-purchase, unless you tell me otherwise.
- **Study resources on hand:** CBT Nuggets (video courses — covers most of this list), Cisco Packet Tracer (CCNA/CCST simulation — removes the "no physical lab yet" blocker for early networking labs)
- **OTS (Ogun Tech Solutions):** side/passive business build, must not interfere with employment
- **Constraints:** one child, work/life balance is a stated priority, normal-week capacity 8–10 hrs, heavy-week 10–14 hrs, occasional 4–6+ hr vacation deep-work days

## 3. Target-State Assessment

### 12 months out (2027-11-08, Year 1 close)

By the end of Year 1 you should hold **AZ-900, MS-900, CCST Networking, CCST Cybersecurity, CCT Collaboration, CCT Routing & Switching, CCNA, AZ-104, and MD-102**, have a rebuilt and *measured* (not guessed-at) homelab running real VLAN/routing/virtualization infrastructure, have at least 3–4 completed OTS Proof-of-Work records, have started the leadership/MSP-operations track in parallel rather than after, and be positioned to interview credibly for L2/Systems Engineer roles — not yet Solutions Architect or vCIO, which need Years 2–3's production hours, security depth, and business-strategy reps to be credible.

### 36 months out (~2029-11-05, program close) — added 2026-09-13

This program now targets a dual capstone: **Sr. Solutions Architect and/or vCIO**, not Solutions Architect alone. Those two roles share a technical foundation but diverge in emphasis — Solutions Architect leans on technical depth and design tradeoffs, vCIO leans on business alignment, budget ownership, vendor management, and translating technical risk into terms leadership acts on (see §18a). Rather than pick one now, this plan builds the shared foundation through Year 2 and lets Year 3 specialize based on which direction is pulling harder by then — a decision for the Year 2 close review (§26), not this document.

By month 36 you should hold everything from Year 1 plus **AB-650, AI-901, Security+, AZ-800/AZ-801, and AZ-305** (§9a), have delivered at least one real multi-year technology roadmap with a budget attached — the vCIO's signature deliverable — to an actual client or stakeholder (OTS or otherwise), have a portfolio of completed ADRs spanning both technical and business tradeoffs, have real vendor-negotiation reps, and be able to independently run a quarterly business review. That combination — not the certifications alone — is what makes you credible for Sr. Solutions Architect and/or vCIO conversations. Certifications get you in the room; the roadmap-delivery and QBR reps are what keep you in it.

**One more layer, added 2026-09-13 (see §29 in full):** the certs and reps above describe *2026's* version of these roles. By program close in late 2029, both roles will plausibly be doing meaningfully different work — industry research (Microsoft's own new Agentic AI Business Solutions Architect track, IDC's FinOps-for-AI forecasting, platform-engineering predictions for agentic infrastructure) points at architects shifting from hands-on design toward AI/agent-system orchestration, governance, and cost accountability, and vCIOs needing real technical-financial fluency specifically for AI workload economics. §29 lays out what that implies for this plan and where it's already been folded into §9a, §18a, and §19 below, rather than treated as a bolt-on.

### Addendum (2026-09-13): AI-901 added as certification #10

You asked whether an AI certification belonged on the list. It does, and it closes a real gap: nothing in the original 9-cert list maps to Skill 13 (Local AI/LLM Infrastructure) or Skill 14 (AI for IT Operations) in your own skill matrix (§4), even though the homelab's AI Gateway VLAN is already locked-in architecture in this project.

**Pick: AI-901 (Azure AI Fundamentals).** Microsoft retired AI-900 on June 30, 2026 — AI-901 isn't a renumbering, it's a substantial redesign: 55–60% hands-on work in Microsoft Foundry (agents, multimodal models, content extraction), some Python expected, vs. AI-900's pure concept-recognition format. Still fundamentals-tier pricing/passing bar ($99, 700/1000). It stays on the Microsoft track alongside AZ-900/MS-900/MD-102/AZ-104/AB-650, which keeps your vendor-ecosystem consistent.

*(CompTIA also offers an "AI Essentials" credential, but as of this research it reads as a skills-badge / Career Builder product rather than a proctored exam with the same weight as the rest of your list — not recommended as a substitute for AI-901.)*

**Placement (your call):** Year 2, Q1 — grouped with AB-650 and Security+ as the "modern/emerging" quarter, so Year 1's calendar and hour budget stay exactly as built. See §9a for the full Year 2 window.

### Addendum (2026-09-13): CCT Collaboration + CCT Routing & Switching added back, plus salary data

You supplied your employer's (or industry) certification pay matrix and asked to add CCT Collaboration and CCT Routing & Switching alongside CCST — you do field network technician work in addition to remote MSP support, so the original "CCT is field-repair-oriented, weaker fit" reasoning doesn't hold for you specifically. Both are back in the plan, run **alongside** CCST rather than instead of it.

**Where they land:** a new short block, **Phase 2b**, runs 2027-01-04 → 2027-02-08 (5 weeks) — right after the holiday buffer and before CCNA. CCT technician exams (100-890 CLTECH, 100-490 RSTECH) are narrower than CCST's, so this doesn't need a full 7-week slot. Consequence: CCNA's start slides from 2027-01-04 to 2027-02-08, and every phase after it slides the same 5 weeks — Year 1 now closes **2027-11-08**, not 2027-10-04. See the updated calendar in §5–9. Nothing else in the plan was compressed to absorb this; the honest move was to extend the timeline, consistent with how this whole document has handled every other addition.

**One asymmetry worth flagging:** on the pay matrix you provided, CCT Collaboration and CCT Routing & Switching each carry a **$1,000/yr** increase — but **CCST doesn't appear on the matrix at all**. If your employer's incentive program only pays for what's on that list, CCST may not carry a direct pay bump the way CCT does, even though it's still the better on-ramp to CCNA and broader competency-builder. Worth a quick confirmation with whoever owns that matrix (HR/your manager) on whether it's exhaustive or just examples — I'm not assuming either way. See §28 for the full salary mapping.

### Certification currency check (verified via web search, September 2026)

| Cert | Status | Action |
|---|---|---|
| AZ-900 (Azure Fundamentals) | Current. Minor refresh expected ~Q3 2026 (more AI/Entra/Well-Architected content, less Service Fabric/SLA-percentage minutiae). | No action — study current objectives when you start. |
| MS-900 (M365 Fundamentals) | Current. Minor refresh expected ~Q4 2026 (Copilot, Viva Suite added; Skype for Business content fully gone). | No action needed for your Phase 1 window. |
| ~~CCT Collaboration~~ / ~~CCT Routing & Switching~~ | Still technically active per Cisco, but CCT is a **field-service repair-technician** credential (diagnose/replace hardware on-site) — a weaker fit for remote MSP L1/L2 work than your original intent suggests. | **Recommended swap: CCST Networking + CCST Cybersecurity.** CCST (Cisco Certified Support Technician) is Cisco's newer (2023+) entry family, explicitly built as the on-ramp to CCNA, and matches help-desk/support work far better. Preserves your original "safe-parallel, low-stakes Cisco pair before CCNA" intent. If you'd rather keep literal CCT, say so and I'll swap it back — the calendar slot is identical either way. |
| MD-102 (Endpoint Administrator) | Current. No retirement flagged. | No action. |
| ~~MS-102~~ (M365 Administrator) | **Retiring October 2026** — right at your kickoff. Replaced by **Exam AB-650 → Microsoft 365 Certified: AI Services Administrator Associate**, reaching general availability October 2026. | **Recommended swap: AB-650.** Note this is a real content shift, not a renumbering — ~35–40% of AB-650 covers material MS-102 never had (Copilot licensing/governance, Microsoft Entra Agent ID, Agent 365 registry, AI cost/compliance). Budget it as a new exam, not a "MS-102 refresh." |
| CCNA (200-301) | Current version active. Blueprint trending toward more automation/Python, cloud/VPC integration, AAA/Zero Trust, Wi-Fi 6/WPA3 — Cisco has historically refreshed the blueprint roughly every 2–3 years (last major refresh Feb 2024), so a new version could land inside your Phase 3 window. | Re-pull the official exam blueprint from Cisco the month before you schedule the exam — don't study 12 months of stale objectives. |
| AZ-104 (Azure Administrator) | Current. Incremental refresh ~Q2 2026 (AI Services management, Container Apps, expanded Monitor/Entra content; Server 2012 migration and classic deployment scenarios removed). | No material action — same guidance as CCNA: re-check objectives near your exam date. |
| Security+ (SY0-701) | Current version, no near-term retirement flagged. | No action. |
| AI-901 (Azure AI Fundamentals) — **added 2026-09-13** | Current — replaced AI-900 (retired June 30, 2026). Real redesign: 55–60% hands-on in Microsoft Foundry (agents, multimodal, content extraction), some Python expected. | New addition, closes the Skill 13/14 gap (§3 addendum). Placed Year 2, Q1 alongside AB-650. |

**Net effect on your original 9-cert list:** 7 unchanged, 1 swapped for content-equivalent reasons (MS-102→AB-650, forced by retirement), 1 recommended swap for job-fit reasons (CCT→CCST, your call to accept or decline), plus 1 addition (AI-901) at your request.

---

## 4. Top 25 (+2 pending) Skill Matrix — Self-Assessed Baseline (2026-09-13)

**Scale changed at your request: 0–5** (0 = no exposure, 1 = aware/read about it, 2 = guided-lab capable, 3 = independent/production-capable, 4 = can teach/mentor others, 5 = expert/could architect it — half-points allowed, you used several). The table below replaces the earlier estimated baseline with your own self-assessment, collected one skill at a time on 2026-09-13. **Average across the original 25: 1.08/5 (27/125 total)** — revisit at every monthly review (§22). Skills 26–27 (added with the §29 future-proofing pass) aren't in that average yet — they're unscored until you give them a real 0–5.

| # | Skill Domain | Self-Assessed (0–5) | Primary Cert/Track Driver |
|---|---|---|---|
| 01 | Network Engineering | **1** | CCST, CCNA |
| 02 | Systems Administration | **2** | MD-102, homelab |
| 03 | Virtualization (Proxmox) | **1** | Homelab |
| 04 | Linux | **1** | Homelab, CCNA labs |
| 05 | Endpoint Management | **1** | MD-102 |
| 06 | Cloud Architecture | **1** | AZ-900, AZ-104 |
| 07 | Azure Administration | **1** | AZ-104 |
| 08 | Microsoft 365 Administration | **2.5** | MS-900, AB-650 |
| 09 | Identity & Access Management | **1.5** | MD-102, AZ-104, AB-650 |
| 10 | Cybersecurity | **0** | Security+, CCST Cybersecurity |
| 11 | Security Architecture | **0** | Security+ → Year 2 |
| 12 | Backup/DR | **0** | Homelab, OTS |
| 13 | Automation (n8n) | **0** | AI/Automation track |
| 14 | Local AI/LLM Infrastructure | **1** | AI Gateway VLAN project |
| 15 | AI for IT Operations | **1** | OTS projects, AI-901 |
| 16 | DevOps/IaC | **0.5** | GitHub habit already established |
| 17 | Observability/Monitoring | **2** | Homelab measurement plan (§13) |
| 18 | Solutions Architecture | **0** | ADR practice, Year 2 focus, AZ-305 (§28) |
| 19 | Technical Documentation | **2.5** | Already a relative strength — keep it |
| 20 | Technical Communication | **2.5** | Existing documentation habit transfers here |
| 21 | MSP Service Delivery | **1.5** | Direct job experience |
| 22 | IT Operations Management | **1.5** | Leadership track |
| 23 | IT Leadership | **1.5** | Leadership track |
| 24 | Project Management | **1** | OTS projects as training ground |
| 25 | IT Business/MSP Economics | **0** | OTS |
| 26 | AI/Agent Architecture &amp; Governance *(added 2026-09-13, see §29)* | **not yet scored** | AZ-305, AI-901, homelab AI Gateway VLAN |
| 27 | FinOps / AI Cost Engineering *(added 2026-09-13, see §29)* | **not yet scored** | §18a vCIO track, homelab metrics (§13) |

Skills 26–27 are new as of the §29 future-proofing pass — deliberately left unscored rather than guessed at; add them to the next skills-matrix update the same way the original 25 were collected (one at a time, your own 0–5).

**Reading this honestly:** six domains sit flat at 0 — Cybersecurity, Security Architecture, Backup/DR, Automation, Solutions Architecture, and IT Business/MSP Economics. That's not alarming this early (Cybersecurity/Security Architecture are explicitly Year 2 by design; Automation is explicitly deferred to homelab Phase 3; Solutions Architecture and MSP Economics are meant to grow out of real OTS reps, which haven't started yet) — but it's the honest starting line, and it's what the Year 1 close review (§26) and each monthly review (§22) will measure progress against. Your three highest scores — Microsoft 365 Administration, Technical Documentation, Technical Communication (2.5 each) — track cleanly with your existing MSP experience and documentation habit.

### 4a. Foundational Skill Priority Stack (added 2026-09-13)

You asked me to use this assessment to actually coach you toward Sr. Solutions Architect, not just schedule exams. The certification calendar (§5–9) is sequenced by exam logistics; this stack is sequenced by what genuinely depends on what — it's the order these skills need to become solid *underneath* the certs, regardless of which exam is "current" that month.

**Tier 0 — bedrock (everything else sits on this):**
- **Linux (1/5)** — CLI, filesystems, permissions, services, SSH, bash. Runs under Proxmox, most of the homelab, and every automation/AI project on the roadmap.
- **Network Engineering (1/5)** — TCP/IP, subnetting, VLANs, routing, NAT, DNS/DHCP. The literal foundation of CCST, CCT, and CCNA — and you cannot architect a network you don't understand at the packet level.
- **Systems Administration (2/5)** — Windows Server, AD, GPO. The parallel bedrock for the Microsoft stack (MD-102, AZ-104, M365).

**Tier 1 — built directly on Tier 0:** Virtualization/Proxmox (1/5, sits on Linux), Cloud Architecture + Azure Administration (1/5 each, sit on networking + systems fundamentals), Identity & Access Management (1.5/5, sits on systems admin).

**Tier 2 — specialty layers that assume Tier 0–1 are solid:** Cybersecurity + Security Architecture (0/5 — you can't reason about defense-in-depth without first understanding what's being defended), Automation/AI (0–1/5 — scripting assumes Linux/networking fluency), Backup/DR (0/5 — assumes systems + virtualization).

**Tier 3 — the Solutions Architect capstone:** Solutions Architecture, IT Business/MSP Economics (0/5 each), and Technical Communication (already your relative strength at 2.5/5). These are synthesis skills — they only become *real* once Tiers 0–2 give you enough raw material to reason about actual tradeoffs. The common failure mode at this level is the architect who knows the vocabulary but can't debug their own design; the antidote is exactly Tiers 0–2 being genuinely solid, not just certified.

**The practical implication:** even though Phase 1 formally starts with AZ-900/MS-900, the deliberate-practice priority underneath the whole calendar is **Linux CLI fluency and core networking** — both sitting at 1/5 and blocking nearly everything above them. The homelab rebuild (Phase 0, happening right now) is the actual vehicle for this — every pfSense/VLAN/Catalyst step is a Tier-0 rep, not just a chore to get through.

### 4b. How I'll coach you from here (added 2026-09-13)

You asked me to help you build skills, not just produce answers for you. Concretely, that means:

- **Attempt before looking.** For hands-on work (CLI commands, configs, subnetting math, troubleshooting), you write your attempt first — I check it and explain what's off, rather than handing you the working version. For concepts, I'll ask a diagnostic question before explaining, so we only spend time on the actual gap.
- **Labs get objectives, not scripts.** When you ask for a lab, you get a scenario and constraints, not a numbered walkthrough — unless you're genuinely stuck after a real attempt, in which case you get a hint sized to close the specific gap, not the full solution.
- **"Test me" means a real test.** Applied troubleshooting scenarios and recall questions, not softball multiple choice.
- **You can always override this.** Say "just give me the answer" or "walk me through it" and I will, immediately, no friction — this is the default mode, not a rule you have to fight.
- **This doesn't apply to program scaffolding.** Building the dashboard, updating the calendar, researching cert changes — that's project infrastructure, not the learning itself, and I'll keep doing that directly.

---

## 5–9. Certification Roadmap, Calendar, Study Hours, Parallel Map, Practice-Exam Strategy

### Sequencing logic

Fundamentals first (build the study habit, low stakes) → CCST pair (still entry-level, but technical — proves you can sustain two-track parallel study) → **CCNA** (the anchor cert of the whole year; everything else is scheduled around protecting this block) → AZ-104 (leverages AZ-900, moderate-high load) → MD-102 (moderate load, closes Year 1). AB-650 and Security+ open Year 2.

### Year 1 Calendar

| Phase | Window | Weeks | Certs | Homelab focus | OTS/Leadership focus |
|---|---|---|---|---|---|
| **Phase 0 — Pre-Kickoff** | 2026-09-13 → 2026-10-05 | 3 | none (setup) | Rebuild plan v1: BOM check, network diagram v1, pfSense/Catalyst reinstall plan | GitHub repo reset, glossary doc restarted, Top-25 self-assessment |
| **Phase 1 — Fundamentals** | 2026-10-05 → 2026-11-02 | 4 | **AZ-900 + MS-900** (parallel) | pfSense reinstalled, VLAN 10 (LAB) recreated | Leadership Module 1: communication basics; OTS docs only |
| **Phase 2 — Entry Cisco pair** | 2026-11-02 → 2026-12-21 | 7 | **CCST Networking + CCST Cybersecurity** (staggered overlap — start Cybersecurity in week 4 of Networking) | Catalyst switching + trunking rebuilt (feeds CCNA labs directly) | Leadership Module 2: delegation/prioritization basics |
| **Holiday/Recovery Buffer** | 2026-12-21 → 2027-01-04 | 2 | none — protected | light review only | protected — family priority |
| **Phase 2b — Field Cisco pair** *(added 2026-09-13)* | 2027-01-04 → 2027-02-08 | 5 | **CCT Collaboration + CCT Routing & Switching** (narrower, technician-level — lighter than CCST) | Field-relevant hardware diagnostics practice on the rebuilt Catalyst gear | OTS/leadership stay light — short block, protect momentum into CCNA |
| **Phase 3 — CCNA (anchor cert)** | 2027-02-08 → 2027-05-31 | 16 | **CCNA 200-301** (solo) | Lab validation gated to CCNA phases D/E (below) — Packet Tracer first, physical hardware once rebuilt | OTS/leadership reduced to maintenance mode during this block |
| **Recovery + Integration** | 2027-05-31 → 2027-06-14 | 2 | none | — | OTS catch-up sprint, Q1 review (see §19) |
| **Phase 4 — AZ-104** | 2027-06-14 → 2027-08-30 | 11 | **AZ-104** (solo) | Proxmox GPU-passthrough planning run as the "applied cloud/virtualization" parallel | Leadership Module 3: feedback & accountability |
| **Recovery** | 2027-08-30 → 2027-09-13 | 2 | none | — | Q2/mid-year review |
| **Phase 5 — Endpoint** | 2027-09-13 → 2027-11-08 | 8 | **MD-102** | Homelab measurement baseline captured (§13 metrics) | OTS: first paying/pilot engagement candidate identified |
| **Year 1 close** | 2027-11-08 | — | 9 certs complete | — | Full competency assessment (§26) |

**Year 2, Q1 (Oct–Dec 2027):** AB-650 + AI-901 (safe-parallel — same low-stakes fundamentals-tier pairing pattern as AZ-900+MS-900 in Phase 1), then Security+ (4–6 week dedicated window as you specified — not compressed). This is the natural bridge into the Year 2–3 extension below.

### §9a. Year 2–3 Calendar (36-Month Extension) — added 2026-09-13

Dates computed from the actual Year 1 close date (2027-11-08), in 13-week quarters. This is the calendar the §3 "36 months out" target and the new §18a vCIO Competency Track run against.

| Quarter | Window | Certs | Homelab / AI focus | vCIO / Architecture focus |
|---|---|---|---|---|
| **Y2 Q1** | 2027-11-08 → 2028-02-07 | **AB-650 + AI-901** (parallel), then **Security+** begins | — | Business/financial literacy reading starts (Skill 24) |
| **Y2 Q2** | 2028-02-07 → 2028-05-08 | **Security+** closes; **AZ-800/AZ-801** (Windows Server Hybrid Administrator Associate) begins | — | First real OTS ADR written under the full 16-element Solutions Architecture Training Framework (§19/§27) |
| **Y2 Q3** | 2028-05-08 → 2028-08-07 | AZ-800/801 continues/closes | AI Gateway VLAN build-out begins (Proxmox stable per §13 Phase 3) — **build basic agent governance/RBAC into it from day one** (§29c), not bolted on later | First "mini-QBR" practice run — informal, internal, low-stakes rep at recognizing/structuring a quarterly business review |
| **Y2 Q4** | 2028-08-07 → 2028-11-06 | none (consolidation) | Homelab metrics pass #2 — **add basic AI/inference cost tracking to the metrics set** (§29b/§13) | First full multi-year technology roadmap + budget document drafted (not yet delivered live) — **draft includes an AI workload cost/ROI section**, not just infra line items (§29b) · **Year 2 close review** (extends §26) |
| **Y3 Q1** | 2028-11-06 → 2029-02-05 | **AZ-305** (Azure Solutions Architect Expert) prep begins — **check the current blueprint for AI/agent workload content before starting** (§29a); it has been expanding on recent refreshes | — | Roadmap document refined against Y2 Q4 feedback |
| **Y3 Q2** | 2029-02-05 → 2029-05-07 | **AZ-305** exam + recovery | — | First real vendor-negotiation reps (via OTS or day-job exposure) |
| **Y3 Q3** | 2029-05-07 → 2029-08-06 | none | — | **vCIO capstone:** the Y2 Q4 roadmap+budget document delivered live to an actual client or stakeholder, QBR-style — **including the AI cost/governance section drafted in Y2 Q4** (§29) |
| **Y3 Q4** | 2029-08-06 → 2029-11-05 | none — optional CCNP/security-associate/vCIO-training-program evaluation only, not committed (§29a flags one more optional candidate: AB-100) | — | Portfolio consolidation (ADRs, proof-of-work, roadmap capstone), job-search readiness · **Program close** |

**Hour-budget sanity check:** Year 2 carries roughly 272 cert-study hours across 52 weeks (~5.2 hrs/week average, front-loaded into Q1–Q3); Year 3 carries roughly 135 cert-study hours (~2.6 hrs/week average, front-loaded into Q1–Q2). Both leave real room in Q3–Q4 of their respective years for the vCIO practice work (roadmap drafting, QBR reps, vendor negotiation) rather than that work getting squeezed out by exam prep — which is also why Year 2 and Year 3 each schedule only **one** new cert beyond what's already listed, despite several "evaluate later" candidates sitting on your matrix (MS-500, SC-200, AZ-500, SC-400, CCNP Enterprise). Adding more would be the cert-stacking your own Part 20 instruction told me to challenge — the business-competency reps are the harder-to-fake differentiator for a vCIO conversation, and they need the hours more than a fifth security cert does.

### Estimated study hours (calibrate against your own pace after Phase 1 — these are planning inputs, not promises)

| Cert | Est. hours | Weeks in plan | Implied hrs/week |
|---|---|---|---|
| AZ-900 | 18–22 | 4 (shared w/ MS-900) | ~5 |
| MS-900 | 14–18 | 4 (shared w/ AZ-900) | ~4 |
| CCST Networking | 45–55 | 7 (shared w/ Cybersecurity) | ~7 |
| CCST Cybersecurity | 45–55 | 7 (shared w/ Networking) | ~6 |
| CCT Collaboration | 25–30 | 5 (shared w/ Routing & Switching) | ~5 |
| CCT Routing & Switching | 25–30 | 5 (shared w/ Collaboration) | ~5 |
| CCNA 200-301 | 160–200 | 16 | ~11 (heavy-week territory — this is why the block is protected) |
| AZ-104 | 80–100 | 11 | ~8 |
| MD-102 | 60–75 | 8 | ~8 |
| *(Year 2)* AB-650 | 60–80 est. (new exam, treat estimate as soft) | — | — |
| *(Year 2)* AI-901 | 20–25 est. (fundamentals-tier, but the Foundry/hands-on portion adds more than AI-900 used to take) | — | — |
| *(Year 2)* Security+ | 80–100 | 4–6 (per your instruction) | ~16–20 — this is intentionally the one cram-adjacent block, and it's short by design, not by accident |
| *(Year 2)* AZ-800/AZ-801 | 80–100 est. (Windows Server Hybrid Administrator Associate — two-exam associate cert, estimate is soft) | ~13 (Y2 Q2–Q3) | ~6–8 |
| *(Year 3)* AZ-305 | 120–150 est. (Expert-level — requires real AZ-104 depth first, this is the heaviest single-cert estimate in the whole 36-month plan outside CCNA) | ~13 (Y3 Q1–Q2) | ~9–11 |

### Practice-exam strategy (applies to every cert, detailed further in §15)

Practice exams are diagnostic, not primary learning. Rule of thumb: don't touch a full practice exam until you've completed guided labs (Phase D) and at least one pass of the official objectives. For fundamentals (AZ-900/MS-900), 1–2 practice exams is enough. For CCST/CCNA/AZ-104/MD-102, run a diagnostic exam at the ~60% material-covered mark, then 2–3 more spaced through weak-area remediation, stopping new-material study 10–14 days before the real exam and switching entirely to review + timed practice.

---

## 10. Weekly Operating System

**Normal week (8–10 hrs):** 3–4 cert-study blocks (60–90 min each) + 1 lab block (90 min) + 1 OTS/documentation block (45–60 min) + 1 short leadership/architecture reading block (30 min).

**Heavy week (10–14 hrs):** add one more cert block and one more lab block. Reserve heavy weeks for the CCNA block (Phase 3) and the pre-exam final-review weeks of any cert — not for routine weeks.

**Vacation deep-work day (4–6+ hrs):** one per identified vacation day, used for whichever is most behind: a full lab session, a practice exam + review, or an OTS proof-of-work sprint. Never used to "catch up" on missed weeks by cramming multiple certs' material at once.

**Daily study template (typical 60–90 min block):** 5 min review of prior session's notes → 35–60 min new material or lab → 10 min notes/glossary update → 5 min log hours + update dashboard weak-areas.

### §10a. Time-Logging Protocol (added 2026-09-14)

You asked for a way to actually log training time — cert study, homelab work, OTS work, anything that counts toward this program — and have it show up as a widget on the dashboard, updated regularly. Here's how it works, given the tools actually available:

**The check-in.** At the start of any session in this project chat, I'll ask: *"Are you in training mode right now?"* — a plain yes/no. This isn't automatic background tracking (I have no way to watch a clock while you're away from the chat, especially for hands-on homelab work happening off-screen) — it's a deliberate check-in, same spirit as the existing daily-template habit of "5 min log hours" you already had in §10.

- **Yes:** I log an entry for that session — date, what you tell me you're working on (or what's obvious from the conversation), and duration. Duration is self-reported by you (either up front — "logging 90 minutes for CCST labs" — or at the end of the session when you tell me how long you were at it). I don't guess at elapsed wall-clock time from message timestamps; that would silently undercount anything you did outside the chat, which is most of the actual homelab/lab work.
- **No:** nothing gets logged. This is the default for sessions that are really about planning, dashboard/doc maintenance, or anything else that isn't training time itself — exactly like this session.

**The log.** Every logged session becomes one row in the companion doc ***Training-Time-Log.md*** — date, category (cert study / homelab / OTS / leadership / other), duration, and a one-line summary of what got done. I write the summary from what actually happened in the session (or what you tell me, for off-screen work); you can always correct it.

**The widget.** The dashboard's Training Time card shows running totals (all-time hours, this week's hours, last logged session) pulled from that log. It updates whenever the log updates and the dashboard gets republished — same manual-republish model as the rest of the dashboard (footer, §Master Dashboard), not a live auto-sync. If you want a truly live, self-serve logging widget (you click a button, it saves instantly, visible to your manager too) that's a different, bigger architecture decision — it would need a shared backend capability that, per the same tradeoff already made for the rest of this dashboard, would restrict viewers to people inside your organization and break the "share the link with my manager" requirement. Flag it if you want to revisit that tradeoff; for now this keeps the dashboard shareable with anyone you send the link to.

## 11. Minimum Viable Week

When work, parenting, illness, or OTS collide: **2 cert-study sessions + 1 lab + 1 short review, nothing else.** No catch-up marathon, ever — the next Monthly Review (§19) re-baselines the calendar instead of trying to recover lost hours by force.

## 12. Burnout Management

Monitor monthly: study hours actually logged vs. planned, exam density (never two exams inside the same 4-week window), OTS workload, homelab workload, family load signals, work intensity. **When two or more of these run hot simultaneously, the response is to cut scope — drop a "nice to have" (an OTS feature, a homelab stretch goal) — never to add hours.** The 2-week recovery buffers in §5–9's calendar are not optional slack; treat them as scheduled the same as an exam date.

---

## 13. Homelab Roadmap (Professional Dojo)

**Ground truth as of this document:** the network lab needs to be rebuilt from scratch. This roadmap treats that as Homelab Phase 0, superseding any earlier phase numbering in prior project notes.

- **Phase 0 (Pre-Kickoff, 3 wks):** hardware/service inventory **confirmed 2026-09-13** (see *Homelab & Infrastructure Stack Inventory*) — produce network diagram v1, reinstall pfSense on the dedicated pfSense box, recreate VLAN 10 (LAB).
- **Phase 1 (during Cert Phase 1–2, ~11 wks):** rebuild Cisco 8-port switching + trunking (this becomes your first CCST/CCNA hands-on validation, not just busywork), re-establish Sunshine/Moonlight remote access, confirm Raspberry Pi #1's thin-client path to the lab VLAN.
- **Phase 2/2b (CCST + CCT blocks, 12 wks):** every networking lab topic gets built twice — once in Packet Tracer (fast iteration), once on physical hardware once it's stable (validation). This is the LAB → STAGING → PRODUCTION discipline from your brief, compressed to LAB(sim) → LAB(physical). CCT's field-technician focus (Phase 2b) is a natural fit for hands-on work on the actual Cisco switch and pfSense box, not just simulation.
- **Phase 3 (during AZ-104 block):** Proxmox stood up on the Lenovo box, GPU-passthrough planning, laying groundwork for the "AI Gateway VLAN" (local-first AI, no Claude API/no per-call billing — this architecture stays locked per your existing project instructions, and stays separate from the RunPod-based creative-AI-video track).
- **Metrics to capture once the lab is stable (don't guess these — measure them):** CPU/RAM/GPU utilization under load, storage IOPS, network throughput/utilization, VM and container density, power draw, temperature, AI inference performance on whatever local model you first deploy, and backup job duration/success rate. First measurement pass targeted for end of Phase 5 (~Oct 2027).

## 14. OTS (Ogun Tech Solutions) Roadmap

OTS stays in documentation-only mode through Phase 2 (protect the CCNA block from business-development distraction), then produces its first Proof-of-Work record (template in §21) once the homelab is stable enough to host a real OTS-facing service. Target: first pilot/paying-candidate engagement identified by end of Phase 5 (Oct 2027) — not necessarily closed, just identified and scoped, so it becomes a Year 2 early win rather than a Year 1 overreach.

## 15. AI / Local LLM Roadmap

Deferred until homelab Phase 3 (Proxmox stable) — building local AI infrastructure before the virtualization layer under it is stable is exactly the kind of premature-technology-before-problem move Skill 18's "what problem are we solving before what technology" principle warns against. When it starts: Ollama (or equivalent) on the rebuilt GPU box, model selection matched to actual VRAM measured in §13 (not assumed), then RAG/embeddings once a concrete use case exists (ticket-summarization or SOP-generation are the two your brief already named as good candidates).

## 16. n8n Automation Roadmap

First real workflow target: **backup verification** (ties directly to §17's Backup/DR skill and gives OTS a genuine proof-of-work artifact) or **infrastructure health reporting** off the homelab metrics in §13 — pick whichever the homelab actually needs first once it's rebuilt, rather than picking in the abstract now.

## 17. MSP Service-Delivery Roadmap

Runs as a reading/reflection track (not a cert) throughout Year 1: SLA/SLO/KPI vocabulary, ticket-lifecycle and escalation practice applied to your actual day job (this is free, real-world reps), backlog and change-management concepts introduced in Phase 2–3, formalized against OTS once OTS has its first real client-shaped workflow in Phase 5.

## 18. IT Management Roadmap

Three leadership modules distributed across Phases 1, 2, and 4 (see calendar in §5–9): communication basics → delegation/prioritization → feedback/accountability. No management certification (e.g., ITIL Foundation) is scheduled anywhere in this 36-month plan — per your own instruction not to over-load management certs, and because it doesn't close a skill gap the technical list plus the vCIO Competency Track (§18a) doesn't already address better. Revisit only if a real gap shows up at the Year 2 close review (§26).

## 18a. vCIO Competency Track (added 2026-09-13)

There's no standardized proctored vCIO certification — unlike AZ-104 or CCNA, this is a role built from business competencies, not an exam. Commercial MSP training programs exist (Kaseya myITprocess, TruMethods, vCIOToolbox RampCamp, vCIO Growth Academy) but they're vendor/cost-variable and not on your pay matrix — optional evaluation, not a scheduled commitment (see Y3 Q4 in §9a). What actually builds vCIO credibility is reps, tracked here against §9a's calendar:

- **Business/financial literacy (Skill 24, currently 0/5):** starts Y2 Q1 as a reading/reflection track — budget structures, TCO/ROI framing, how MSP economics actually work — same low-stakes format as the §18 leadership modules, not a cert.
- **Technology roadmapping:** the vCIO's signature deliverable is a multi-year technology roadmap with a budget attached. First draft in Y2 Q4, refined in Y3 Q1, delivered live in the Y3 Q3 capstone (§9a). This is deliberately sequenced after AZ-800/801 and alongside AZ-305 prep — you need real platform depth before a roadmap you'd stake credibility on.
- **QBR (quarterly business review) practice:** first informal/internal rep in Y2 Q3, building toward the live capstone delivery in Y3 Q3. QBRs are where roadmap content meets executive communication — treat early reps as low-stakes practice, not a performance to get right the first time.
- **Vendor-negotiation reps:** real reps (via OTS or day-job exposure), targeted for Y3 Q2 once the AZ-305 exam is out of the way.
- **Security-posture-assessment practice:** folds into the Solutions Architecture Training Framework's security/tradeoffs elements (§19) rather than running as a separate track — Security+ (Y2 Q1–Q2) is the technical floor this sits on.
- **AI cost/ROI fluency (added 2026-09-13, see §29b):** research on where this role is heading (IDC's FinOps-for-AI forecasting in particular) points at vCIOs increasingly needing real technical-financial fluency specifically for AI workload economics — training costs, inference scaling, token spend — not just traditional infra TCO. The Y2 Q4 roadmap draft and Y3 Q3 capstone (§9a) are where this gets practiced for real, using the homelab AI Gateway's own cost data as the training ground rather than a hypothetical.

**Differentiator worth keeping in view (per research, goleadingit.com):** Solutions Architect leans on technical depth and design tradeoffs; vCIO leans on business alignment, budget ownership, vendor management, and translating technical risk into terms leadership acts on. This program builds the shared technical foundation through Year 2 and lets the Year 2 close review (§26) — not this document today — decide how hard to lean into either specialization for Year 3, since real production reps and homelab/OTS evidence will tell you more about the right fit than a plan written in September 2026 can.

## 19. Solutions Architecture Roadmap

Every OTS project of real size (starting with the Phase 5 pilot candidate) produces a lightweight ADR-style writeup: problem, requirements, constraints, options, tradeoffs, decision. This is deliberately light in Year 1 (you don't have enough production reps yet for heavier architecture work to be honest) and becomes the primary Year 2 focus once AZ-104 and MD-102 give you real platform depth to architect against.

**Added 2026-09-13 (see §29a):** once the homelab AI Gateway VLAN is live (Y2 Q3, §9a/§13), ADRs written from that point forward should start including agent-architecture and AI-governance tradeoffs where relevant — not as a separate track, just as a normal option/tradeoff category alongside the infrastructure ones you're already documenting. The goal is the ADR habit absorbing this as it becomes relevant, not a parallel "AI architecture" curriculum.

## 20. GitHub / Source-of-Truth Architecture

Keep your existing habit (Git/GitHub as file-of-record, safe commit/push sequence already established, laptop+desktop sync via VS Code). Suggested top-level structure, additive to what already exists:

```
homelab/            network diagrams, configs (no secrets), phase logs
certifications/     study notes, glossary additions, practice-exam logs
ots/                proof-of-work records, SOPs, client-facing docs
architecture/       ADRs
automation/         n8n workflow exports (secrets excluded/templated)
career/             skill matrix history, monthly reviews, proof-of-work index
```

## 21. Proof-of-Work System

Use the template your brief already specified for every significant OTS or homelab project:

```
PROJECT / DATE / BUSINESS PROBLEM / TECHNICAL PROBLEM / REQUIREMENTS / CONSTRAINTS /
ARCHITECTURE / TECHNOLOGIES / IMPLEMENTATION / TESTING / SECURITY / AUTOMATION /
MONITORING / RESULT / METRICS / LESSONS LEARNED / WHAT I WOULD CHANGE /
SKILLS DEMONSTRATED / CERTIFICATION CONNECTION / CAREER VALUE
```

Target cadence: not every homelab task warrants one of these — reserve it for things that would actually read well in an interview or a resume line. Realistic Year 1 target: 3–4 completed records, not one per phase.

## 22. Monthly & Quarterly Milestones

**Monthly review** (see §19's original list — certifications hours/progress/practice scores/weak domains, technical skills gained, homelab systems deployed/measured, OTS progress, AI/automation status, leadership skills practiced, architecture designs completed, career evidence created) happens at the end of every calendar month starting November 2026. Ask me for it with "monthly review" and I'll run it against the dashboard state.

**Quarterly milestones** line up with the recovery buffers already in the calendar: end of Phase 2 (Dec 2026), end of Phase 2b/field Cisco pair (Feb 2027), end of Phase 3/CCNA (May 2027), end of Phase 4/AZ-104 (Aug 2027), Year 1 close (Nov 2027).

## 23. Risk Register

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| CCNA block (16 wks, ~11 hrs/wk implied) collides with a genuinely heavy work/family stretch | Medium | High — this is the anchor cert | Phase 3 has zero OTS/leadership load by design; if a heavy stretch hits, drop to Minimum Viable Week (§11) and let the *end date* slip rather than the *content* get rushed |
| Homelab rebuild takes longer than 11 weeks (Phase 1–2 window) | Medium | Medium | CCNA Phase 3 is designed to start on Packet Tracer regardless — physical-hardware validation can trail by a few weeks without blocking study |
| Cisco refreshes the CCNA blueprint mid-Phase-3 | Low–Medium | Medium | Re-pull the objectives the month before scheduling (already built into §5–9) |
| 9-cert-in-12-months expectation causes pressure to cram Security+ or AB-650 into Year 1 | Medium | High (burnout) | This document explicitly does not schedule them in Year 1 — see Executive Overview. Revisit only if Phases 1–5 finish *early*, never by compressing them |
| OTS starts pulling real hours before the CCNA block is done | Medium | Medium | OTS stays documentation-only through Phase 2, explicitly, per §14 |

## 24. Burnout Plan

Covered functionally in §12; the mechanism is: monthly review flags overheating signals → response is scope reduction, not added hours → recovery buffers in the calendar are protected, not optional.

## 25. Career Progression Map

**Primary track:** L1 → L2 (targeted around Phase 3–4 completion, roughly mid-2027, once CCNA + AZ-104 give you real technical range beyond ticket resolution) → Systems/Network/Cloud Engineer (Year 2, once MD-102/AB-650/Security+ round out the platform+security story) → **two possible Year 3 endpoints, not decided until the Year 2 close review (§26):**

- **Sr. Solutions Architect** — gated on real architecture reps from §19, the full 16-element framework applied through Year 2–3, AZ-305 (the matrix's single largest cert value at $5,000/yr — §28), and production platform depth from AZ-104/AZ-800-801.
- **vCIO** — gated on the business-competency reps in §18a: a delivered multi-year roadmap+budget, live QBR capability, real vendor-negotiation reps, and the security-posture-assessment practice folded into §19.

These two share the same Year 1–2 technical foundation and diverge only in Year 3 emphasis (§3's "36 months out" section has the full framing) — this program deliberately keeps both live rather than forcing a choice now, because real production/OTS evidence by the Year 2 close will make the right fit obvious in a way this document can't predict in September 2026.

**Secondary track:** Team Lead readiness builds through the three leadership modules (§18) plus real delegation/feedback practice at your current job — certifications alone don't qualify you for Service Delivery Manager or IT Operations Manager roles; the gap is demonstrated leadership evidence, which is why §18, §18a, and §21 exist.

**Gaps to close before claiming L2 credibly:** production Azure administration hours (AZ-104 gives the cert, not the hours — OTS/homelab has to supply the hours), a documented incident-response rep or two, and at least one completed architecture writeup (§19/§21).

**Gaps to close before claiming Sr. Solutions Architect or vCIO credibly (Year 3):** a full 16-element ADR/roadmap portfolio (not just lightweight Year-1-style writeups), AZ-305 or AZ-800/801 production depth depending on direction, at least one real client/stakeholder-facing roadmap delivery (the Y3 Q3 capstone in §9a), and — for vCIO specifically — actual vendor-negotiation and QBR reps, since those can't be simulated the way a lab can.

## 26. Competency Assessment Checkpoints

**Year 1 close (run Oct/Nov 2027):** Re-score the Top-25 Skill Matrix (§4) against the same 0–5 scale, compare to baseline, and specifically check: can you independently stand up and troubleshoot a VLAN'd multi-switch topology (CCNA proof), administer an Azure subscription end-to-end (AZ-104 proof), manage endpoints via Intune (MD-102 proof), and produce a clean ADR for a real decision (architecture proof)? If any of those four are still "guided-lab" level rather than "independent," that's the honest Year 2 starting point — not a failure of the plan, just where the re-baseline needs to happen next.

**Year 2 close (run ~Oct/Nov 2028):** Re-score again. This is the checkpoint that decides Year 3's specialization lean (Sr. Solutions Architect vs. vCIO vs. genuinely both, per §25) — look specifically at which of §18a's business-competency reps vs. §19's architecture reps are pulling ahead, and which OTS/homelab evidence is accumulating faster. This review also builds the real Year 3 calendar detail that §9a currently only sketches.

**Program close (run ~Oct/Nov 2029):** Final assessment against the full 36-month target state in §3 — certifications held, roadmap capstone delivered, ADR/proof-of-work portfolio, and whether the Sr. Solutions Architect / vCIO positioning is credible enough to act on in the job market.

## 27. Year 2–3 Advanced Roadmap

See **§9a** for the locked quarterly calendar (certs, homelab/AI, and vCIO/architecture focus per quarter) and **§18a** for the vCIO competency track in full. In brief: Year 2 closes out AB-650, AI-901, Security+, and adds AZ-800/801; Year 3 adds AZ-305 (Q1–Q2) and shifts weight onto the business-competency reps — a delivered roadmap+budget capstone and real QBR/vendor-negotiation practice (Y3 Q3). Architecture practice itself shifts across this window from §19's "lightweight ADR" format to the full 16-element Solutions Architecture Training Framework from your original brief (business problem → requirements → constraints → architecture → tradeoffs → cost model → implementation → testing → monitoring → DR → documentation → post-implementation review). §9a's calendar is locked against today's information; the Year 2 close review (§26) is where it gets re-baselined against real progress, same discipline as the Year 1→2 handoff.

## 28. Certification Value — Salary Matrix (added 2026-09-13)

You provided a certification pay-increase matrix (30 entries across Cisco, Microsoft, CompTIA, HPE/Aruba, Fortinet, VMware, Zerto, and (ISC)²). Below is what's directly relevant, mapped onto this program.

### Certs in this plan that appear on your matrix

| Cert | Matrix annual increase | Year |
|---|---|---|
| AZ-900 | $500 | 1 |
| MS-900 | $500 | 1 |
| CCT Collaboration | $1,000 | 1 |
| CCT Routing & Switching | $1,000 | 1 |
| CCNA (200-301) | $2,500 | 1 |
| MD-102 | $2,500 | 1 |
| AZ-104 | $3,500 | 1 |
| Security+ | $1,000 | 2 |

**Year 1 confirmed total (if increases stack): ~$11,500/yr.** **Full-program confirmed total (Years 1–2, matrix items only): ~$12,500/yr.** Treat the stacked total as directional, not contractual — cert pay matrices commonly cap the total, or pay only for the highest cert in a track rather than every rung of it (e.g. CCNA might supersede a lower Cisco cert's bump rather than adding to it). Confirm the stacking rule with whoever owns this matrix before counting on the full number.

**Certs in this plan not on your matrix (no data):** CCST Networking, CCST Cybersecurity (see the asymmetry note in §3), MS-102/AB-650 (MS-102 was on older matrices at $2,000 but AB-650 is a different exam and untested here), AI-901 (too new for this matrix).

### The standout you should know about: AZ-305

**Azure Solutions Architect Expert (AZ-305) carries the single largest increase on your entire matrix — $5,000/yr** — and it is *literally the certification for your named target role*. It requires AZ-104 as a practical prerequisite (not a formal gate, but you need the administrator-level Azure depth AZ-104 gives you to have a realistic shot at it). **Now scheduled: Year 3, Q1–Q2 (§9a)**, after AZ-104 (Year 1) and AZ-800/801 (Year 2) give you real production Azure/hybrid depth to build on.

### AZ-800/AZ-801 (Windows Server Hybrid Administrator Associate) — $2,500

Matches Skill 02 (Systems Administration) and your existing on-prem/hybrid AD work. **Now scheduled: Year 2, Q2–Q3 (§9a)**, as the companion cert to AZ-104 before AZ-305 prep begins.

### vCIO — no matrix entry

Unlike every other cert in this program, vCIO doesn't have a standardized proctored exam or a line on your pay matrix — it's a role built from business competencies (§18a), not a credential. Commercial MSP training programs (Kaseya myITprocess, TruMethods, vCIOToolbox RampCamp, vCIO Growth Academy) exist and are worth evaluating **at the Year 3 Q4 checkpoint (§9a)** if the Year 2 close review (§26) points you toward the vCIO lean — but they're cost-variable and optional, not a scheduled commitment like everything else in this section.

### Other matrix entries worth a second look in Year 3+ (not yet scheduled)

- **MS-500 (Security Administrator Associate) — $2,500**, **SC-200 (Security Operations Analyst Associate) — $1,500**, **AZ-500 (Azure Security Engineer Associate) — $1,500**, **SC-400 — $1,500.** All deepen Skill 09 (Security Architecture) alongside Security+ — evaluate against the "does this close a real gap" test at the Year 2 close review rather than adding all four now. Deliberately left out of Year 2–3's one-new-cert-per-year discipline (§9a) so the business-competency reps get the hours instead.
- **MS-700 (Teams Administrator Associate) — $1,500.** Pairs thematically with CCT Collaboration (voice/collaboration, cloud side vs. field side) — worth a look given you're already doing collaboration field work.
- **CCNP Enterprise** — flagged as an optional Y3 Q4 evaluation only (§9a), not committed; check against the "does this close a real gap" test given you'll already hold CCNA plus two Cisco field certs by then.

### Recommended against adding

- **CompTIA Network+ ($1,000)** — meaningfully overlaps CCNA's own foundational content; CCNA already supersedes it for your purposes. Adding it would be exactly the certification-stacking your own brief told me to challenge (Part 20) without a real skill-gap payoff.
- **Fortinet, Aruba, VMware, Zerto entries** — genuinely can't evaluate these without knowing whether your MSP's client environments actually run this gear. Tell me if they do (which vendor, which product) and I'll assess fit the same way I did for everything else here, rather than adding vendor tracks speculatively.

### AB-100 (Agentic AI Business Solutions Architect) — not on your matrix, flagged for evaluation (added 2026-09-13)

Microsoft's new expert-level credential (AB-100) for exactly this program's target role — see §29a for what it covers. No pay-matrix data exists for it, and it's too new to commit to a calendar slot with confidence. **Flagged as an optional Y3 Q4 evaluation (§9a), alongside the CCNP/vCIO-training-program checks already scheduled there** — not added to the 14-cert count above. Revisit once AZ-305 is done and the Year 3 direction (Sr. Solutions Architect vs. vCIO vs. both) is clearer.

---

## 29. Future-Proofing — The 2029 Skillset (added 2026-09-13)

Everything above this section describes what a Sr. Solutions Architect or vCIO needs *today* (September 2026). You asked me to update the plan with an eye toward what those roles will actually need **36 months from now**, at program close — not just today's job description with a longer runway. This section is that pass: grounded in current industry research (Microsoft's own new credential for this exact target role, IDC's 2026 FutureScape forecasting, and platform-engineering industry predictions — sources below), not speculation. The findings are already woven into §9a (calendar), §18a (vCIO track), §19 (ADR practice), and §4 (two new pending skill domains) above; this section is where the reasoning lives in one place.

**The honest caveat up front:** anything dated 2029 is a forecast, not a fact — three years is a long horizon for a field moving this fast, and this section will need re-checking at the Year 2 close review (§26), the same discipline as everything else in this plan. Treat it as "best current signal," not a locked prediction.

### 29a. Architects are shifting from designers to AI/agent-system orchestrators

Microsoft now offers an expert-level credential — **Agentic AI Business Solutions Architect (AB-100)** — built specifically around this shift: architecting with generative AI and Foundry Tools, designing "agentic-first" solutions and multi-agent orchestrated systems, working with emerging open standards (Agent2Agent/A2A, Model Context Protocol/MCP), and implementing responsible-AI practices, access controls, and audit trails around agent systems. Independent industry commentary points the same direction — architects are expected to spend less time on routine technical design work (which AI increasingly assists with directly) and more time on strategic orchestration, AI governance/ethics, change management, and translating AI-system risk to stakeholders. Practically, for this program: AZ-305's blueprint has been expanding to include AI-workload content on recent refreshes (check it fresh at Y3 Q1, §9a), homelab ADRs should start absorbing agent-architecture tradeoffs once the AI Gateway is live (§19), and AB-100 itself is flagged as an optional Y3 Q4 evaluation (§28) rather than committed now — it's new enough that a 2028/2029 version of it is the more realistic target than today's.

### 29b. FinOps is expanding to cover AI-specific cost dynamics — and vCIOs need dual technical-financial fluency for it

IDC's research (2026 FutureScape) forecasts organizations underestimating AI infrastructure costs by up to 30% through 2027, driven by AI workloads' unpredictable, exponential-scaling cost profile (training runs, data-pipeline overhead, inference-at-scale, token spend) versus traditional flat cloud billing. The skill implication is specific: real-time cost observability across the AI lifecycle (not periodic reviews), adaptive/predictive forecasting instead of static budgets, and — the part that lands squarely on the vCIO side of this program — the ability to translate that technical cost complexity into financial insight leadership can act on. This is exactly the vCIO's signature "translate technical risk into business terms" duty (§18a), just applied to AI economics specifically rather than generic IT spend. Practically: the homelab AI Gateway VLAN (Y2 Q3, §9a) is where you get real cost data to practice this on rather than a hypothetical, the Y2 Q4 roadmap draft should include an actual AI cost/ROI section, and new Skill 27 (FinOps/AI Cost Engineering, §4) tracks this going forward.

### 29c. Platform engineering is treating AI agents as first-class infrastructure citizens

Platform-engineering industry predictions for 2026 describe agents getting the same governance treatment developers already get — RBAC permissions, defined "golden paths," policy-as-code, and pre-deployment cost gates specifically for AI/token spend — plus platforms increasingly serving as the safety net that reviews AI-generated infrastructure code before it ships. The practical implication for this program is narrow and concrete: when the homelab AI Gateway VLAN gets built in Y2 Q3 (§9a, §13, §15), build basic agent governance and access control into it from the start rather than retrofitting it later — even a homelab-scale version of "which agent/automation can touch what" is a real rep at a skill that's becoming a stated expectation for both target roles, and it costs little extra to do it at build time versus after the fact.

### 29d. What stays durable regardless of how fast the tooling moves

Every source above agrees on one thing: the human-centered, synthesis-level skills this program already treats as the Tier-3/capstone layer (§4a) — complex reasoning about unstated requirements, stakeholder trust-building, strategic translation of technical complexity into business terms, change management — become *more* valuable as AI absorbs more routine technical-design and documentation work, not less. That's not a reason to under-invest in the technical certs (§9a); it's a reason not to let §18a's business-competency reps and §19's ADR practice get treated as optional "soft skill" add-ons squeezed in around the real work. By this program's own design (§9a's hour-budget math deliberately protects Y2–Y3 Q3–Q4 for exactly this kind of practice) that's already the plan — this research is confirmation the emphasis is pointed the right way, not a reason to change the calendar.

### Sources consulted (2026-09-13)

- [Microsoft Certified: Agentic AI Business Solutions Architect](https://learn.microsoft.com/en-us/credentials/certifications/agentic-ai-business-solutions-architect/) — AB-100 credential overview and skills coverage
- [The Future of Solutions Architect Role with Agentic AI](https://newsletter.bigtechcareers.com/p/the-future-of-solutions-architect) — shift from technical design to strategic orchestration
- [IDC: Balancing AI innovation and cost — the new FinOps mandate](https://www.idc.com/resource-center/blog/balancing-ai-innovation-and-cost-the-new-finops-mandate/) — AI-specific cost forecasting and required CIO/vCIO fluency
- [10 Platform Engineering Predictions for 2026](https://platformengineering.org/blog/10-platform-engineering-predictions-for-2026) — agent governance, RBAC, and FinOps-as-infrastructure-requirement predictions

---

## Master Dashboard

A live, reopenable control-center version of the fields below has been published separately as an HTML page — use it as the day-to-day "what's next" surface; use this document as the full reference when you need the reasoning behind a decision.
