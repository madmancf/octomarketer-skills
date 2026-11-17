---
name: claude-md-builder
description: Backwards-compatible alias for /claude-md: create, update, or compact global (<=60 lines), project (<=120 lines), and per-client (<=150 lines) CLAUDE.md instruction files.
argument-hint: "[--global | --project | --client <slug>]"
effort: medium
allowed-tools: Bash(gk *), Bash(~/.local/bin/gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Edit, Write
---

# Layered `CLAUDE.md` Builder & Auditor (`/claude-md-builder` -> `/claude-md`)

Backwards-compatible alias synced with `/claude-md` (`${CLAUDE_PLUGIN_ROOT}/skills/claude-md/SKILL.md`) for **Claude Opus 5.5** (`opus`) and **Claude Sonnet 5.5** (`sonnet`, `high` effort).

## Governed Instruction Files & Line Caps

1. **Personal Global File (`~/.claude/CLAUDE.md`, `<= 60` lines):**
   - Personal identity, cross-project plain-English writing habits, privacy rules (never commit `.env` or paste API keys), and spend checks.
   - Template: `${CLAUDE_PLUGIN_ROOT}/templates/claude-md-global.tmpl.md` (`gk claude-md --global`).
2. **Project / Root File (`./CLAUDE.md`, `<= 120` lines):**
   - Brand summary, pointers to `./brand/design.md` and `./tov/tov.md`, Always-Active vs `0`-token `/`-invocable skill table (`#01..#70` template hints), and locked guardrails (or multi-client `clients/<slug>/` routing when using `claude-md-root.tmpl.md`).
   - CLI: `gk claude-md --project` (syncs `.claude/settings.json` active packs automatically).
3. **Per-Client Agency File (`./clients/<client-slug>/CLAUDE.md`, `<= 150` lines):**
   - Scoped to one client brand (`gk client init <client-slug>`): audience ICP, core offer, positioning, hard taboos, and pointers to `brand/tokens.json` and `tov/tov.md`.
   - Template: `${CLAUDE_PLUGIN_ROOT}/templates/claude-md-client.tmpl.md`.

## Step-by-Step Execution

1. **Collect Brand / Client Inputs:** Brand name, website URL, 1 to 2 sentence ICP, 2 to 3 offer bullets, and hard taboos.
2. **Render & Sync Skill Profile:** Populate the matching template (filtering workflows to installed plugins when inside a partial release pack, or syncing `<!-- SKILL_PROFILE:START -->` via `gk claude-md --project`).
3. **Verify Line Caps:** Confirm strict caps (`<= 60` global, `<= 120` project/root, `<= 150` per-client) before finishing.
