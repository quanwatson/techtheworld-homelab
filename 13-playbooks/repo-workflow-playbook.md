# Repo Workflow Playbook

How I actually work in this repo, session to session. Nothing exotic — the point is doing the same handful of steps every time so nothing gets lost between devices.

## Standard session flow

1. `git pull` — always start here, especially since this repo gets touched from more than one machine.
2. `git status` — know what's actually changed before doing anything else.
3. Make the change (docs, config reference, whatever).
4. `git add` — stage deliberately. Not `git add -A` out of habit; look at what's being staged.
5. Commit with a message that says what changed and, where it matters, why.
6. `git push` — don't let a session end with uncommitted work sitting on one machine.

## Commit message conventions

Short summary line, present tense, specific enough that `git log --oneline` is actually useful six months from now. "Fix stuff" doesn't tell future-me anything; "Fix duplicate date header in build journal" does.

## What gets logged where

This repo separates execution, planning, and learning on purpose (see `01-logs/`). Before committing, ask: is this a state change (Build Journal), a planned change with risk to weigh (Change Control), understanding gained (Learning Log), or just in-progress context (Session Notes)? Not every commit needs a log entry — plenty of doc tweaks don't — but anything that changes the lab's actual state does.

## Multi-device notes

GitHub is the source of truth, not whatever's sitting on any one machine's disk. If a device's local structure ever drifts from what's in GitHub, GitHub wins — pull and reconcile, don't push a local guess over it. Empty directories don't survive in Git without a placeholder file, so structural folders get a `.gitkeep` until they have real content.
