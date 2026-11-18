---
name: claude-md
description: Use when creating, updating, or compacting global (~/.claude/CLAUDE.md, <=60 lines) or project-bound (./CLAUDE.md, <=120 lines) instruction files, brand summaries, ToV pointers, and active vs on-demand skill profiles.
argument-hint: "[--global | --project] [<instructions-or-facts>]"
effort: medium
allowed-tools: Bash(gk *), Bash(~/.local/bin/gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Edit, Write
---

# Dedicated `CLAUDE.md` Governance Skill (`/claude-md`)

Keep both global and project instruction files crisp, grounded, and strictly within line caps so **Claude Opus 5.5** (`claude-opus-5-5` / `opus`) and **Claude Sonnet 5.5** (`claude-sonnet-5-5` / `sonnet`, `high` effort) follow every rule without skimming bloated prompt files.

## Two Governed Scopes (Never Mix Them)

1. **Global Personal Layer (`~/.claude/CLAUDE.md`, `<= 60` lines):**
   - **What belongs here:** Personal identity and role, cross-project writing preferences (plain English, Flesch `>= 47.0`, zero AI filler words, zero em-dashes in social copy), privacy & spend discipline (never paste API keys into chat, never commit `.env` or `.env.local`, run `gk cost-check` before optional paid APIs), and model preferences (**Claude Opus 5.5** vs **Claude Sonnet 5.5** on `high` effort).
   - **What never belongs here:** Brand-specific offers, client colors, or project-specific campaign details.
   - **Template & CLI:** `${CLAUDE_PLUGIN_ROOT}/templates/claude-md-global.tmpl.md` or `gk claude-md --global [--name "..."] [--role "..."] [--prefs "..."]`.

2. **Project-Bound Layer (`./CLAUDE.md`, `<= 120` lines):**
   - **What belongs here:**
     1. **Brand Summary:** Project/brand name, website URL, target audience ICP (1 to 2 sentences, with `(full dossier in ./brand/icp.md)` when `./brand/icp.md` exists), and core offer (2 to 3 concrete bullets).
     2. **Authoritative File Pointers:** Pointers to `./brand/design.md` (`./brand/tokens.json`), `./brand/icp.md` (when generated via `/icp`), and `./tov/tov.md` (`<= 250` lines) instead of duplicating hex palettes, full ICP tables, or full post examples inside `./CLAUDE.md`.
     3. **Active vs `/`-Only Skill Profile (`<!-- SKILL_PROFILE:START -->` .. `<!-- SKILL_PROFILE:END -->`):** Lists Always-Active packs + `#01..#70` template hints (so natural chat works immediately) alongside `0`-token on-demand `/<skill>` wrappers (`disable-model-invocation: true`).
     4. **Locked Guardrails:** Readability gate (`gk lint`), `/claude-md` routing rule, and `$0.00` local default / spend caps.
   - **Multi-Client Agency Subfolders (Optional):** When running a multi-client workspace under `./clients/<slug>/`, keep root `./CLAUDE.md <= 120` lines (`claude-md-root.tmpl.md`) and per-client `./clients/<slug>/CLAUDE.md <= 150` lines (`claude-md-client.tmpl.md`).
   - **CLI Helper:** `gk claude-md --project [--brand-name "..."] [--url "..."] [--icp "..."] [--offer "..."]` (automatically syncs the skill profile from `.claude/settings.json`).

## Execution Steps

1. **Identify Scope (`--global` vs `--project`):**
   - Default to `--project` (`./CLAUDE.md`) unless the user explicitly asks to set or revise their cross-project personal preferences (`--global`).
2. **Read Current File & Preserve Locked Sections:**
   - Read the existing `CLAUDE.md` first. Preserve `<!-- STUDIO:LOCKED:START -->` / `<!-- STUDIO:RULES:START -->` guardrails and sync `<!-- SKILL_PROFILE:START -->` with `.claude/settings.json`.
3. **Write & Verify Strict Line Caps:**
   - Run `gk claude-md --project --check` (or `gk claude-md --global --check`, fallback `~/.local/bin/gk` or `./plugins/getknown-core/bin/gk`) after editing to verify `<= 60` lines (global) and `<= 120` lines (project).
