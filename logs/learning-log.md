# Learning Log

This log documents technical knowledge, workflows, and engineering judgment developed during the design and build of my homelab. Entries focus on understanding, application, and professional relevance rather than raw command history.

---

## 20251220

### 20251220001 — Git-based workflow, documentation discipline, and repo hygiene

**Scope:**  
Local development workflow, Git/GitHub usage, documentation structure, and professional logging practices.

---

### What I learned

- Git tracks files relative to the repository root, not the editor or terminal context.
- VS Code and the terminal must operate on the same physical repository path for Git to detect changes.
- `.gitignore` rules are absolute unless explicitly overridden with exceptions.
- A clean Git workflow requires intentional staging, meaningful commits, and a consistent pull–commit–push cycle.
- Logs serve different purposes and should be separated by intent (build, learning, operational).

---

### Key concepts understood

- **Source of truth:** GitHub functions as the authoritative state across devices, regardless of power state.
- **Repo hygiene:** Clean status (`working tree clean`) is a deliberate goal, not an accident.
- **Change control:** Not all activity warrants a build log entry; only state-changing actions should be recorded.
- **Documentation-first methodology:** Writing design decisions before implementation reduces mistakes and rework.
- **Professional logging:** Logs should explain *why* decisions were made, not just *what* was done.

---

### Applied in the lab

- Established a repeatable Git workflow:
  - `git pull` before work
  - `git status` for awareness
  - Explicit `git add` for intentional staging
  - Clear, descriptive commit messages
  - `git push` to synchronize state
- Resolved repository path conflicts between VS Code and PowerShell.
- Implemented `.gitignore` exceptions to allow a shared homelab log across devices.
- Standardized the Build Journal with deterministic, date-based identifiers.
- Created structured folders for:
  - `/logs` (activity, learning, and build records)
  - `/playbooks` (procedural references and cheat sheets)
  - `/runbooks` (operational and incident response guidance)

---

### Why this matters professionally

- Mirrors real-world engineering practices used in MSP, NOC, and infrastructure roles.
- Demonstrates understanding of version control beyond basic usage.
- Shows ability to document systems, decisions, and learning clearly.
- Establishes habits that scale to teams, production systems, and audits.
- Produces artifacts that can be reviewed by employers to assess growth and technical maturity.

---

### Outcome

- Laptop development environment fully operational and synchronized with GitHub.
- Documentation structure and logging standards established before further infrastructure changes.
- Homelab now functions as both a technical platform and a professional portfolio.

---

### Next focus areas

- Sync and validate repository on the Dell OptiPlex 3080
- Network segmentation and VLAN design
- First operational runbooks and infrastructure playbooks

# Learning Log

This log captures technical understanding, workflow refinement, and professional skill development gained while building and operating my homelab. Entries focus on *why* things work, not just *what* was done.

---

## 20251220

### 20251220002 — Git fundamentals, repo convergence, and multi-device workflow control

**What I learned:**
- Git does not track folders unless they contain tracked files.
- Empty directories will never appear in GitHub unless a placeholder file (e.g., `.gitkeep`) is added.
- `git status` being “clean” does not mean the filesystem matches expectations — it only reflects tracked state.
- Multiple machines can diverge structurally even when pointing to the same repository.
- GitHub only reflects committed state, not local filesystem state.

---

**Key concepts understood:**
- **Source of truth:** GitHub represents the authoritative state; all devices must converge to it.
- **Tracked vs untracked:** Files and directories must be explicitly tracked to exist in version control.
- **Canonical editor:** Choosing a primary authoring device (3080) prevents structural drift.
- **Controlled convergence:** Blending environments requires intentional commits, not copying files manually.
- **Infrastructure hygiene:** Structure decisions should be committed once, then pulled everywhere else.

---

**Applied in the lab:**
- Identified why the 3080 directory structure differed from GitHub.
- Confirmed that missing folders on GitHub were untracked/empty.
- Added `.gitkeep` files to all structural directories to enforce canonical layout.
- Committed and pushed the unified directory structure from the 3080.
- Pulled the canonical structure to all other devices.
- Established the 3080 as the primary editing and execution node.

---

**Why this matters professionally:**
- Prevents configuration drift across environments.
- Mirrors how teams manage multi-node infrastructure repositories.
- Demonstrates understanding of Git beyond basic commands.
- Shows ability to debug tooling issues methodically instead of guessing.
- Establishes habits used in MSP, NOC, and infrastructure engineering roles.

---

**Outcome:**
- All devices now share an identical, intentional repository structure.
- GitHub accurately reflects the full homelab layout.
- Future changes can be made confidently without desynchronization.

---

**Next learning focus:**
- Writing first operational playbooks and runbooks.
- Applying documentation standards to live infrastructure changes.
- Network segmentation and service-level validation.
<<<<<<< HEAD

## 2025-12-21 — Logging Discipline as a Force Multiplier

**Key Insight:**  
The value of a homelab compounds when decisions and state changes are documented, not just actions.

**Rules Locked In:**  
- Do not log individual Git commands  
- Do not log minor edits or file viewing  
- Log only decisions, architecture changes, or learning moments  

**Logging Framework:**  
- Build Journal → state changes & decisions  
- Homelab Log → session timeline  
- Learning Log → understanding gained  

**Why This Matters:**  
- Enables faster troubleshooting  
- Makes rebuilds possible  
- Trains enterprise-grade change management habits  
- Produces interview-ready artifacts

## 2025-12-21 — Layered Network Changes Reduce Cognitive Load

**Insight:**  
Stacking Layer 2 and Layer 3 changes simultaneously increases failure ambiguity.

**Lesson Learned:**  
- Validate routing and DHCP before touching switches  
- Treat pfSense VLAN setup as deterministic  
- Introduce switch configuration only after a known-good firewall state  

**Application Going Forward:**  
- One major network change per session  
- Validate → document → then proceed
=======
>>>>>>> 859a8c1c8a4ec77b44982bcfa30bf217c7da3eed
