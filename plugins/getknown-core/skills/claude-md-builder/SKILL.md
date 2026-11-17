---
name: claude-md-builder
description: Use when generating or compacting workspace and client CLAUDE.md instruction files within strict line caps.
argument-hint: "[--client <slug>]"
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Edit, Write
---

# Layered `CLAUDE.md` Builder & Auditor (`/claude-md-builder`)

Keep instruction files short and concrete so Claude follows every brand rule without skimming oversized prompt files.

## How the Layered Instruction Files Work

1. **Personal Global File (`<= 60` lines):**
   - Holds personal writing habits across projects (plain English, zero AI filler words, never commit `.env` secrets, check spend before paid API runs).
   - Template: `${CLAUDE_PLUGIN_ROOT}/templates/claude-md-global.tmpl.md` (repo fallback `./plugins/getknown-core/templates/claude-md-global.tmpl.md`).

2. **Root Studio File (`./CLAUDE.md`, `<= 120` lines):**
   - Defines client folder isolation (`clients/<slug>/`, ignoring `demo-brand` once a real brand exists), schema locations, and **only** the Outcome Workflows whose plugin directories are installed in `./plugins/`.
   - Template: `${CLAUDE_PLUGIN_ROOT}/templates/claude-md-root.tmpl.md` (repo fallback `./plugins/getknown-core/templates/claude-md-root.tmpl.md`).

3. **Per-Client File (`./clients/<client-slug>/CLAUDE.md`, `<= 150` lines):**
   - Scoped to one brand (for example `acme-cloud` or an agency prospect): target audience ICP, core offer, positioning, hard taboos, active channels, and pointers to `brand/tokens.json` and `tov/tov.md`.
   - Keep detailed hex values in `brand/tokens.json` and full post examples in `tov/winners/` so the client instruction sheet stays `<= 150` lines.
   - Template: `${CLAUDE_PLUGIN_ROOT}/templates/claude-md-client.tmpl.md` (repo fallback `./plugins/getknown-core/templates/claude-md-client.tmpl.md`).

## Step-by-Step Execution

1. **Collect Client Inputs:**
   - `Client Name` and `client-slug` (initialize folder via `./plugins/getknown-core/bin/gk client init <client-slug>` if new)
   - `Primary Website URL`
   - `Target Audience / ICP` (1 to 2 sentences)
   - `Core Offer & Positioning` (2 to 3 bullets)
   - `Hard Taboos` (claims or phrasing this brand never uses)
2. **Render From Template (Tier-Aware):**
   - Inspect `./plugins/` and include only the workflows present in this pack when populating `claude-md-client.tmpl.md` or `claude-md-root.tmpl.md`.
3. **Verify Line Caps:**
   - Confirm line count stays within caps (`<= 60` global, `<= 120` studio root, `<= 150` per-client) before writing `clients/<slug>/CLAUDE.md`.
