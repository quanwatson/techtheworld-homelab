## Logs Overview

This repository uses purpose-specific logs to document **system evolution**, **operational continuity**, **engineering judgment**, and **change governance**.  
Each log has a defined **prefix**, **intent**, and **scope** to prevent overlap and logging noise.

| Log                     | Prefix | Purpose                              | Question it answers                                      |
| ----------------------- | ------ | ------------------------------------ | -------------------------------------------------------- |
| **Build Journal**       | `BJ-`  | System state & architecture changes  | “What changed in the lab, and why?”                      |
| **Change Control**      | `CC-`  | Controlled change tracking            | “What change was proposed, approved, and executed?”     |
| **Homelab Log**         | `HL-`  | Operational activity & continuity    | “What work was performed and on which system?”           |
| **Learning Log**        | `LL-`  | Understanding & engineering judgment | “What did I understand better after this?”               |
| **Logs Overview**       | `LO-`  | Logging governance & intent           | “Which log should be used, and when?”                    |
| **Session Notes**       | `SN-`  | Ephemeral working context             | “What was I thinking or testing during this session?”   |

Each entry uses its prefix followed by a sequential identifier (e.g., `BJ-016`, `HL-005`) and a date stamp inside the entry body.

---

## 🚫 What You Should NOT Log

Do **not** create entries for:

- Individual Git commands  
- Minor typo or formatting fixes  
- Viewing or browsing files  
- Routine pulls with no resulting changes  
- Passive reading of documentation  

If nothing changed **structurally, operationally, or conceptually**, no log entry is warranted.

> **Restraint is a skill. Noise is technical debt.**

---

## 🧠 Logging Rule of Thumb (Lock This In)

Before creating an entry, ask:

> *“If I read this six months from now, will it explain a decision, state change, or understanding?”*

Use the answer to select the correct log:

- **Decision, architecture, or system state change → Build Journal (`BJ-`)**  
- **Proposed, approved, or executed change → Change Control (`CC-`)**  
- **Session-level activity or environment continuity → Homelab Log (`HL-`)**  
- **Understanding, insight, or judgment gained → Learning Log (`LL-`)**  
- **Working thoughts, experiments, or scratch context → Session Notes (`SN-`)**

Logging with intent ensures the homelab functions not only as infrastructure, but as a **professional engineering system of record**.
