# Learning Log

---

## 12-20-2025

### LL-001
**Topic:** Git-based workflow, documentation discipline, and repository hygiene  

**What I learned:**  
- Git tracks files relative to the repository root, not the editor or terminal context.
- VS Code and the terminal must operate within the same physical repository path for Git to detect changes.
- `.gitignore` rules apply globally unless explicitly overridden.
- A clean Git workflow requires intentional staging, meaningful commits, and a consistent pull–commit–push cycle.
- Logs serve different purposes and must be separated by intent to remain useful.

**Key concepts internalized:**  
- **Source of truth:** GitHub represents the authoritative state across all devices.
- **Repo hygiene:** A clean working tree is a deliberate outcome, not an accident.
- **Change control:** Not all activity warrants documentation—only state changes or decisions do.
- **Documentation-first methodology:** Writing decisions before implementation reduces error rate and rework.
- **Professional logging:** Logs should explain *why* decisions were made, not just *what* was done.

**Applied in the lab:**  
- Established a repeatable Git workflow:
  - `git pull` before work
  - `git status` for awareness
  - Explicit `git add` for intentional staging
  - Descriptive commit messages
  - `git push` to synchronize state
- Resolved repository path mismatches between VS Code and PowerShell.
- Implemented `.gitignore` exceptions to allow shared logs across devices.
- Standardized the Build Journal using deterministic identifiers.
- Created structured directories for:
  - `/logs` (build, activity, learning)
  - `/playbooks` (procedural references)
  - `/runbooks` (operational and incident guidance)

**Why this matters professionally:**  
- Mirrors real-world practices used in MSP, NOC, and infrastructure teams.
- Demonstrates understanding of Git beyond basic command usage.
- Produces reviewable artifacts that show technical growth and maturity.
- Establishes habits that scale to teams, audits, and production systems.

**Outcome:**  
- Laptop environment fully operational and synchronized with GitHub.
- Documentation and logging standards established before further infrastructure changes.
- Homelab now functions as both a technical platform and a professional portfolio.

---

### LL-002
**Topic:** Repository convergence, tracked state, and multi-device workflow control  

**What I learned:**  
- Git does not track directories unless they contain tracked files.
- Empty folders will never appear in GitHub without placeholder files (e.g., `.gitkeep`).
- A “clean” `git status` only reflects tracked content, not filesystem intent.
- Multiple machines can diverge structurally while pointing to the same repository.
- GitHub only reflects committed state—not local filesystem assumptions.

**Key concepts internalized:**  
- **Tracked vs untracked:** Files and directories must be explicitly tracked to exist in version control.
- **Canonical structure:** One device must be designated to author and enforce structure.
- **Controlled convergence:** Repositories should be reconciled via commits, not file copying.
- **Infrastructure hygiene:** Structural decisions should be committed once and pulled everywhere else.

**Applied in the lab:**  
- Diagnosed why the OptiPlex 3080 structure differed from GitHub.
- Identified missing directories as untracked/empty.
- Added `.gitkeep` files to all structural folders.
- Committed and pushed the canonical directory layout.
- Pulled the unified structure to all secondary devices.
- Designated the OptiPlex 3080 as the primary authoring and execution node.

**Why this matters professionally:**  
- Prevents configuration drift across environments.
- Reflects how teams manage shared infrastructure repositories.
- Demonstrates methodical debugging of tooling issues.
- Reinforces disciplined environment control.

**Outcome:**  
- All devices now share an identical, intentional repository structure.
- GitHub accurately reflects the full homelab layout.
- Future changes can be made without desynchronization risk.

---

## 12-21-2025

### LL-003
**Topic:** Logging discipline as a force multiplier  

**Key insight:**  
The value of a homelab compounds when *decisions and state changes* are documented, not just actions.

**Rules locked in:**  
- Do not log individual Git commands  
- Do not log minor edits or file viewing  
- Log only decisions, architecture changes, or learning moments  

**Logging framework reinforced:**  
- **Build Journal:** State changes and architectural decisions  
- **Homelab Log:** Session-level activity and environment continuity  
- **Learning Log:** Understanding gained and judgment refined  

**Why this matters:**  
- Enables faster troubleshooting
- Makes rebuilds and audits possible
- Trains enterprise-grade change management habits
- Produces interview-ready documentation artifacts

---

### LL-004
**Topic:** Layered network changes reduce cognitive load  

**Insight:**  
Stacking Layer 2 and Layer 3 changes simultaneously increases ambiguity when failures occur.

**Lesson learned:**  
- Validate routing and DHCP before touching switches.
- Treat pfSense VLAN configuration as deterministic and isolated.
- Introduce switch configuration only after a known-good firewall state exists.

**Application going forward:**  
- One major network change per session.
- Validate → document → then proceed.

**Professional relevance:**  
This mirrors best practices used in production networks where change isolation is critical for fault attribution and rollback.

## 12-23-2025

### LL-005
**Date:** 12-22-2025  
**Topic:** Documentation as a control plane, not a byproduct  

**What I Learned:**  
Well-structured documentation reduces cognitive load, prevents configuration drift, and acts as a control surface for infrastructure changes. Treating documentation as authoritative enables safer iteration, clearer rollback paths, and easier peer review.

**Professional Relevance:**  
This mirrors enterprise environments where documentation, not memory, governs system evolution. It also enables asynchronous review and handoff without loss of context.

**Applied Going Forward:**  
- No infrastructure change without corresponding documentation updates  
- Documentation reviewed before implementation, not after  
- README and validation checklists treated as gating artifacts

