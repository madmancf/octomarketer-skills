---
description: Use when running the daily social and channel copy workflow: topic radar scan, human-voice post drafting for LinkedIn, Instagram, X, or Telegram, Approval Board sign-off, and voice learning.
argument-hint: "[<topic-or-angle>] [--client <slug>] [--platform linkedin|x|instagram|telegram] [--resume <runId>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp *), Read, Grep, Glob, Edit, Write, Agent
---

# `/run-daily-social` (`/gk-social:run-daily-social`) · Outcome Workflow (`01-social-tov`)

## Flow Contract & Checkpoint Recovery
- **Owning Plugin:** `gk-social` (`01-social-tov`), available directly as `/run-daily-social` (and `/gk-social:run-daily-social` in the `/` picker).
- **Recommended Models (Included in Claude Pro & Max):** **Claude Opus** (`opus`, default) or **Claude Sonnet** (`sonnet`) for daily post drafting and `gk:gk-researcher` scans.
- **Checkpoint State:** Ensure `clients/<slug>/` exists (`gk client init <slug>` if new), then run `gk flow start run-daily-social --client <slug>` (inspect or resume via `gk flow status --client <slug>`, fallback `./plugins/getknown-core/bin/gk`).
- **Primary Outputs:** `clients/<slug>/campaigns/<id>/drafts/draft-pack.json`, `clients/<slug>/tov/tov.md`, `clients/<slug>/campaigns/<id>/learnings.md`

## Ordered Execution Steps
1. **`draft-social-posts`:** Start `gk flow start run-daily-social --client <slug>` (if not already active), fork `/topic-radar` (`gk:gk-researcher`, `sonnet`) to write a `<= 1 KB` topic brief in `campaign-brief.json`, run `/draft-post` inline (`high`) for the target platforms (`linkedin`, `instagram`, `x`, or `telegram`), and advance `gk flow step draft-social-posts --client <slug>`.
2. **`evaluate-anti-slop`:** Advance `gk flow step evaluate-anti-slop --client <slug>` and verify every draft with `gk lint --file <file> --platform <platform>` before saving `draft-pack.json`.
3. **`generate-review-board`:** Advance `gk flow step generate-review-board --client <slug>` and open `/review-board` via `./plugins/getknown-core/bin/gk serve --daemon` (sharing the returned `/board?client=<slug>` URL, or exporting a local `.zip` via `gk publish-review-link --client <slug> --provider local`).
4. **`await-verdict`:** After human approval, advance `gk flow step await-verdict --client <slug>`, run `/what-worked` inline (`high`) to log campaign notes in `campaigns/<id>/learnings.md`, apply confirmed voice edits to `tov/tov.md` via `gk tov apply --verdict <verdict.json> --client <slug>`, and run `gk flow complete run-daily-social --client <slug>`.
