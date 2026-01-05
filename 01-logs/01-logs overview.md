# Logs Overview

## Purpose of This Directory

The `/01-logs` directory contains the **authoritative operational record** of this HomeLab.

Logs are treated as **first-class system artifacts**, not informal notes.  
They provide traceability, accountability, and insight into *why* decisions were made—not just *what* was configured.

This mirrors professional environments where logs support:
- Change management
- Incident response
- Knowledge transfer
- Audit and review

---

## Logging Philosophy

Not all activity deserves to be logged.

Only **state changes, architectural decisions, or meaningful learning moments** are recorded.  
Routine commands, exploratory clicks, and minor edits are intentionally excluded.

This discipline keeps logs:
- High signal
- Reviewable
- Professionally relevant

---

## Log Types & Intent

### Build Journal (`build-journal.md`)
**Purpose:**  
Records **authoritative state changes** to the lab.

**Includes:**
- Infrastructure changes
- Configuration milestones
- Phase transitions
- Validated outcomes

**Does NOT include:**
- Individual commands
- Minor edits
- Reversible experiments that did not alter state

This file answers:  
> *“What is the current state of the lab, and how did it get here?”*

---

### Change Control (`change-control.md`)
**Purpose:**  
Tracks **planned or significant changes** before execution.

**Includes:**
- Design intent
- Risk assessment
- Rollback strategy
- Approval to proceed

This mirrors formal change management used in MSP and enterprise environments.

---

### Checklists (`checklists.md`)
**Purpose:**  
Phase-gated execution control.

**Includes:**
- Phase completion criteria
- Execution readiness checks
- Progress tracking

This file prevents premature execution and scope creep.

---

### Learning Log (`learning-log.md`)
**Purpose:**  
Captures **understanding gained**, not steps performed.

**Includes:**
- Concepts internalized
- Judgment refined through experience
- Cause-and-effect understanding

This file answers:  
> *“What do I now understand that I didn’t before?”*

---

### Homelab Log (`homelab-log.md`)
**Purpose:**  
Session-level continuity and context.

**Includes:**
- What was worked on during a session
- Environmental notes
- Context for resuming work later

This file supports continuity, not auditing.

---

### Session Notes (`session-notes.md`)
**Purpose:**  
Short-lived working notes.

**Includes:**
- Temporary observations
- Scratch notes
- Items to formalize later

Content here is promoted to other logs only if it becomes meaningful.

---

## Professional Relevance

This logging structure demonstrates:
- Change discipline
- Operational maturity
- Audit-ready documentation habits
- Clear separation between execution, planning, and learning

It reflects how infrastructure work is responsibly managed in production environments.

---

## Summary

Logs in this HomeLab are **intentional, scoped, and professional**.

They exist to support:
- Safe iteration
- Clear reasoning
- Knowledge transfer
- Career-ready documentation artifacts
