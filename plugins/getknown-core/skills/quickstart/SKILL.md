---
name: quickstart
description: Use when setting up any new or existing project folder: asks brand URL/materials and frequent job types, configures Always-Active vs 0-token on-demand skills, extracts Brand and Tone-of-Voice .md files, writes ./CLAUDE.md, and stops cleanly.
argument-hint: "[<website-url>] [--active <csv-of-packs>]"
effort: high
allowed-tools: Bash(gk *), Bash(~/.local/bin/gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(node plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp clients/* clients/*), Read, Grep, Glob, Edit, Write, WebFetch, WebSearch
---

# `/quickstart` (`/gk:quickstart`) · Guided Per-Project Setup

## Purpose
Initializes any brand or marketing project folder on **Claude Opus 5.5** (`claude-opus-5-5` / `opus`) or **Claude Sonnet 5.5** (`claude-sonnet-5-5` / `sonnet`, `high` effort): tailors which skill packs stay Always-Active in project context vs `0`-token `/`-invocable wrappers, extracts project Brand and Tone-of-Voice `.md` files, generates `./CLAUDE.md` (`<= 120` lines) via `/claude-md`, and **stops cleanly**.

## Workflow Steps

1. **Verify Node.js 20+ & Collect Project Inputs (1 Focused Prompt):**
   ```bash
   command -v node
   ```
   - If `command -v node` exits non-zero, stop immediately and tell the user in plain English: *"Download and open the standard Node.js 20+ installer (`.pkg` on Mac, `.msi` on Windows) from https://nodejs.org, reopen `Claude.app`, and type `/quickstart` again. No Terminal setup is needed."*
   - Resolve the `gk` CLI (`gk` on `PATH`, `~/.local/bin/gk`, `~/.octomarketer/plugins/getknown-core/bin/gk`, or `./plugins/getknown-core/bin/gk`).
   - If not already supplied in `$ARGUMENTS`, ask the user for two things in one concise message:
     1. **Brand URL & Materials:** Their primary website URL plus any optional brand notes or 2 to 5 real writing samples.
     2. **Frequent Job Types for THIS Project** (frequent packs become **Always-Active** so plain-English chat triggers them; unselected packs stay **`0` startup context tokens** and remain available anytime via `/<skill-name>`):
        - **Daily Social & Brand Voice** -> `gk-social`
        - **Slide Decks, Carousels, Banners & Launch Pages** -> `gk-design`
        - **Animated Data Infographics** -> `gk-motion`
        - **Short-Form 9:16 Video Reels** -> `gk-video`
        - **Competitor & Client Website Audits / Repurposing** -> `gk-agency`
        - **Creative Direction, Angles & Copy Lenses** -> `gk-director`
        - **Lemo-Opuscar 59 Commercial Motion Styles** -> `lemo-opuscar`

2. **Configure Per-Project Skill Context Profile (`gk project-skills`):**
   - Run `gk project-skills` with the selected CSV of frequent packs:
     ```bash
     gk project-skills --active <selected-csv>
     ```
     *(Fallback: `~/.local/bin/gk project-skills --active <selected-csv>` or `node ./plugins/getknown-core/bin/gk project-skills --active <selected-csv>`.)*
   - This keeps `gk` core active, enables `--active` packs in `./.claude/settings.json`, disables unselected packs (`0` startup tokens), and writes thin `user-invocable: true` + `disable-model-invocation: true` wrappers into `./.claude/skills/<skill>/SKILL.md`.

3. **Extract Project Brand `.md` + Tone-of-Voice `.md` Files:**
   - Create `./brand/` and `./tov/` in the project folder (or `clients/<slug>/{brand,tov}/` in a multi-client workspace).
   - Run Brand extraction (`/brand-extract` / `gk brand-extract`) to save verified colors, typography, contrast pairs, and offer notes in `./brand/design.md` (and `tokens.json` when extracted from a live URL).
   - Run Tone-of-Voice extraction (`/tov-extract` / `gk tov`) from the user's real website copy and writing samples to create `./tov/tov.md` (`<= 250` lines).

4. **Write Project `./CLAUDE.md` via `/claude-md` & Verify, Then STOP CLEANLY:**
   - Invoke `/claude-md` (`gk claude-md --project`) to write `./CLAUDE.md` (`<= 120` lines) containing the brand summary, `./brand/design.md` + `./tov/tov.md` pointers, Always-Active vs `/`-only skill table with `#01..#70` template hints, and locked guardrails:
     ```bash
     gk claude-md --project --brand-name "<Brand Name>" --url "<https://brand-url>" --icp "<Target Audience>" --offer "<Core Offer>"
     gk verify-setup --json
     ```
   - Share a short plain-English readiness confirmation (plus the `OCTOMARKETER_VERIFY_V1` block when completing setup verification) and remind the user they can re-run `gk project-skills --active ...` anytime.

## Hard Stop Guardrails (Mandatory)
- **NEVER generate fake starter social posts or placeholder campaigns during `/quickstart`.**
- **NEVER start `gk serve` or open the review `/board` during `/quickstart`.** Stop cleanly as soon as `./CLAUDE.md`, Brand `.md`, Tone-of-Voice `.md`, and `./.claude/settings.json` are verified.
