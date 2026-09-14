# Runbook Format (Template)

Copy this when starting a new runbook. Fill in every section — an empty section means the runbook isn't ready to execute yet, not that the step doesn't apply.

**Platform:**
**Scope:**
**Phase:**
**Change Type:** Planned / Non-disruptive
**Applies To:**

## Purpose
What this runbook accomplishes and why it exists.

## Scope
What's in bounds and what's explicitly out of bounds for this procedure.

## Preconditions
What has to be true before starting — don't skip this and find out mid-change.

## Procedure
The actual steps, in order.

## Validation
How you prove the change worked, not just that it didn't error out.

## Rollback
How to undo this if it goes wrong. If there's no rollback path, don't run the procedure until there is one.

## Notes
Anything that doesn't fit above — gotchas, platform quirks, things that bit me last time.
