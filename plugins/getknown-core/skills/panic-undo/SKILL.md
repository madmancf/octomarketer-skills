---
name: panic-undo
description: Use when the user wants to preview or roll back the last change to their voice file, brand design guide, instruction sheet, or campaign drafts.
argument-hint: "[--client <slug>] [--file <path>] [--dry-run] [--yes]"
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(git *), Read, Edit, Write
---

# Panic Undo & Version Restore (`/panic-undo`)

Give marketers a safe, confirmation-gated undo path whenever a draft, brand token file, `tov/tov.md`, or `CLAUDE.md` change needs to roll back without losing work.

## Step 1: Inspect Available Backups First

Inspect both backup layers in read-only mode before restoring anything:
1. **Automatic `.history/*.bak` Snapshots:**
   ```bash
   ./plugins/getknown-core/bin/gk undo --client <slug> --dry-run
   ```
   *(On a fresh workspace with no `.history/` snapshots yet, `gk undo` safely returns `status: "noop"` and leaves all files untouched.)*
2. **Git Checkpoints (When Inside a Git Repository):**
   - Check `git status --short` and `git log -n 5 --oneline` if `.git/` exists, summarizing recent changes in plain English (1 line per file).

## Step 2: Offer Safe Restore Options (Always Confirm First)

Present the exact target file and timestamp, then run the chosen restore command (`gk undo` and `gk tov restore` automatically create a pre-restore safety backup and prompt for confirmation via `.claude/settings.json` `permissions.ask`):
- **Option A: Restore Latest `.history/*.bak` Snapshot:**
  ```bash
  ./plugins/getknown-core/bin/gk undo --client <slug> [--file <relative-path>]
  ```
- **Option B: Roll Back Protected `tov/tov.md`:**
  Direct `Edit` on `clients/*/tov/tov.md` is blocked by workspace guardrails, so restore `tov.md` safely via:
  ```bash
  ./plugins/getknown-core/bin/gk tov restore --client <slug>
  ```
- **Option C: Restore Client Folder to Last Git Commit (Git Workspaces Only):**
  Copy current modified files into `clients/<slug>/.history/stash-<timestamp>/` first, then restore from git after explicit user confirmation.
