# Logs Overview

`01-logs/` is the operational record for this lab — not informal notes, but the place that shows why decisions got made, not just what got configured. In a real shop this is what supports change management, incident response, and handing work off to someone else.

Not everything gets logged. Only state changes, architecture decisions, or moments where I actually understood something new get written down — routine commands, exploratory clicking around, and small edits don't make the cut. That keeps the signal-to-noise ratio high enough that these logs are still worth reading a year from now.

## What lives where

**Build Journal** (`build-journal.md`) — the authoritative record of state changes: infrastructure changes, configuration milestones, phase transitions, validated outcomes. It does not include individual commands or minor edits. If you want to know what the lab currently looks like and how it got there, this is the file.

**Change Control** (`change-control.md`) — planned or significant changes before they happen: design intent, risk assessment, rollback plan, and sign-off to proceed. This is the closest thing here to formal MSP/enterprise change management.

**Checklists** (`checklists.md`) — phase-gated execution control. Completion criteria, readiness checks, progress tracking. Its whole job is to stop me from jumping ahead of myself.

**Learning Log** (`learning-log.md`) — what I actually understood, not what I did. Concepts internalized, judgment refined by experience, cause and effect. If the build journal answers "what changed," this answers "what do I understand now that I didn't before."

**Homelab Log** (`homelab-log.md`) — session-level continuity: what got worked on, environment notes, context for picking things back up. This is for continuity, not for auditing.

**Session Notes** (`session-notes.md`) — short-lived working notes: temporary observations, scratch thoughts, things to formalize elsewhere later if they turn out to matter.

## Why bother separating all this

Because a single giant notes file becomes useless fast. Splitting execution, planning, and learning apart is what makes this stuff reviewable months later — by me or by someone else — and it's the same separation of concerns that shows up in any team that actually manages infrastructure change well instead of just remembering it.
