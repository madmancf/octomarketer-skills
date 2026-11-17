---
name: parallel-sprint
description: Use when running multi-channel campaign launches, multi-prospect agency teardowns, or batch asset production across isolated parallel subagents.
argument-hint: "<sprint-goal> [--client <slug>] [--lanes <count>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Glob, Edit, Write, Agent
---

# Parallel Subagent Sprint Orchestrator (`/parallel-sprint`)

Delegate multi-page competitor research and multi-format visual rendering to isolated `Agent` subagents (`gk:gk-researcher` and `gk:gk-renderer`, running on **Claude Sonnet**) inside a single `Claude.app` `</> Code` session so raw HTML and asset builds stay out of the main writing context. *(Note: subagents via `Agent` work natively in both `Claude.app` Desktop and CLI.)*

## Step-by-Step Orchestration

### Step 1: Write the Sprint Plan
Inspect `./plugins/` first so every lane uses only plugins installed in this pack, then write a concise checklist in `clients/<slug>/campaigns/<id>/sprint-plan.md`:
- **Shared Context Inputs:** `clients/<slug>/CLAUDE.md`, `brand/tokens.json`, `tov/tov.md`, and `campaign-brief.json`.
- **Independent Lanes (max 5 parallel lanes per batch):**
  - *Agency Pitch Batch:* Lane 1 (`prospect-a` audit), Lane 2 (`prospect-b` audit), Lane 3 (`prospect-c` audit), initializing each folder via `gk client init <prospect-slug>` first.
  - *Campaign Launch Batch:* Lane 1 (channel post drafts), Lane 2 (`16:9` HTML/PPTX/PDF slide deck), plus animated infographic (`03-animated-infographics`) and `9:16` reel (`04-shortform-video-engine`) lanes when those plugins are installed.

### Step 2: Check Spend Caps First
Run `./plugins/getknown-core/bin/gk cost-check --client <slug> --estimated-usd 0.00 --dry-run` (and `--reserve` if confirmed paid BYOK add-ons are used) across the combined batch so parallel lanes stay inside `GETKNOWN_PER_RUN_CAP_USD` (`$2.50`) and `GETKNOWN_DAILY_CAP_USD` (`$15.00`).

### Step 3: Dispatch Isolated Subagents
- **Research & Site Audits -> `gk:gk-researcher` (`sonnet`):** Runs `gk brand-extract`, `gk teardown --crawl-depth 2`, and `gk harvest-proof`, writes structured outputs into `campaigns/<id>/sources/` and `assets/proof/`, and returns a `<= 1 KB` JSON envelope.
- **Visual, Deck & Video Rendering -> `gk:gk-renderer` (`sonnet`):** Renders HTML compositions plus `gk export-pptx`, `gk export-pdf`, `gk export-png`, and `gk render-video` assets into `campaigns/<id>/assets/` and `exports/`, returning output paths and file sizes.
- **Copy Finalization -> Main Thread (`Claude Opus`):** Keep final copy edits and `gk lint --file <draft> --platform linkedin` checks in the main thread so voice stays consistent across every asset.

### Step 4: Unified Approval Board
Merge lane outputs into `clients/<slug>/campaigns/<id>/drafts/draft-pack.json`, launch `./plugins/getknown-core/bin/gk serve --daemon`, and share the `/board?client=<slug>` URL for batch sign-off.
