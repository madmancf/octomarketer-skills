---
description: Use when setting up a new client workspace, extracting brand tokens from a website, seeding Tone of Voice, and checking providers.
argument-hint: "[<brand-url>] [--client <slug>] [--resume <runId>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp *), Read, Grep, Glob, Edit, Write, Agent
---

# `/run-brand-setup` (`/gk:run-brand-setup`) · Outcome Workflow (`getknown-core`)

## Flow Contract & Checkpoint Recovery
- **Owning Plugin:** `gk` (`getknown-core`), available directly as `/run-brand-setup` (and `/gk:run-brand-setup` in the `/` picker).
- **Recommended Models (Included in Claude Pro & Max):** **Claude Opus 5.5** (`opus`, default) for orchestration and voice synthesis; **Claude Sonnet 5.5** (`sonnet`, `high` effort) for forked token extraction.
- **Checkpoint State:** Initialize `clients/<slug>/` first (`gk client init <slug>`), then start `gk flow start run-brand-setup --client <slug>` (inspect or resume via `gk flow status --client <slug>`, fallback `./plugins/getknown-core/bin/gk`).
- **Primary Outputs:** `clients/<slug>/brand/{tokens.json,design.md,icp.md}`, `clients/<slug>/tov/tov.md`, `clients/<slug>/CLAUDE.md`

## Ordered Execution Steps
1. **`extract-brand-tokens`:** Run `gk --version`, initialize the client workspace first via `./plugins/getknown-core/bin/gk client init <slug> --url <url>` (so `clients/<slug>/{brand,tov/winners,tov/anti-examples,campaigns}` exists on disk), start checkpoint tracking via `./plugins/getknown-core/bin/gk flow start run-brand-setup --client <slug>`, fork `/brand-extract` (`gk:gk-researcher`, `sonnet`) to run `gk brand-extract --client <slug> --url <url>` and write `brand/tokens.json` and `brand/design.md`, and advance `gk flow step extract-brand-tokens --client <slug>`.
2. **`generate-tov-profile`:** Advance `gk flow step generate-tov-profile --client <slug>`, fork `/tov-extract` (`high`) on starter posts in `tov/winners/` (or `voice-seed-pack.json`), and compile `tov/tov.md` (`<= 250` lines) via `gk tov init --client <slug> --from clients/<slug>/tov/tov-profile.json`.
3. **`verify-client-setup`:** Advance `gk flow step verify-client-setup --client <slug>`, optionally run `/icp` (`opus`, recommended when website copy, call notes, or CRM exports are available) to synthesize `clients/<slug>/brand/icp.md`, run `/claude-md-builder` (`medium`), check `gk provider-health --client <slug>`, mark `gk flow complete run-brand-setup --client <slug>`, and start the Studio server in background mode via `./plugins/getknown-core/bin/gk serve --daemon` to share the live `/setup?client=<slug>` URL returned in JSON.
