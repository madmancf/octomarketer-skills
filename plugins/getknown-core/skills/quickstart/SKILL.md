---
name: quickstart
description: Use when starting a fresh marketing studio workspace to verify Node and local tools, register pack plugins, and open the Studio in your browser.
argument-hint: "[--client <slug>]"
effort: low
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(node plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp clients/* clients/*), Read, Edit, Write
---

# `/quickstart` (`/gk:quickstart`) · Guided First-Run Studio Setup

## Purpose
Checks that Node.js is installed (~2 to 3 minutes on your first run; instant after that), registers the plugins included in this pack, verifies local browser and media tools, checks a starter sample post when present, and starts the Studio web server in the background.

## Workflow Steps
1. Verify Node.js 20+ is installed first, then register this pack's plugins and run the machine and provider readiness checks:
   ```bash
   command -v node
   ```
   - If `command -v node` exits non-zero, stop immediately and tell the user in plain English: *"Download and open the standard Node.js 20+ installer (`.pkg` on Mac, `.msi` on Windows) from https://nodejs.org, reopen `Claude.app`, and type `/quickstart` again. No Terminal setup is needed."*
   - Once `node` is present, run:
   ```bash
   node ./plugins/getknown-core/bin/gk setup-machine --install
   ./plugins/getknown-core/bin/gk --version
   ./plugins/getknown-core/bin/gk provider-health
   ```
   *(If invoked from an installed plugin cache without `./plugins/`, run `node "${CLAUDE_PLUGIN_ROOT}/bin/gk" setup-machine --install` and `"${CLAUDE_PLUGIN_ROOT}/bin/gk" provider-health`.)*
2. If a real client winner post or `clients/demo-brand/tov/winners/winner-01.md` exists, verify readability with `gk lint` (in `agency-pack` folders where `clients/` starts empty, skip straight to Step 3 and invite the user to run `/run-brand-setup` for their first brand):
   ```bash
   ./plugins/getknown-core/bin/gk lint --file clients/demo-brand/tov/winners/winner-01.md --platform linkedin
   ```
3. Start the local Studio server in background daemon mode (`--daemon` returns immediately with JSON URLs and reuses an already-running server without blocking):
   ```bash
   ./plugins/getknown-core/bin/gk serve --daemon
   ```
4. **Present a Concise 4-Line Marketer Summary (Never Dump Raw JSON):**
   - Summarize readiness in 4 short plain-English bullets: (a) Node & local export status, (b) optional video/audio tool status if video plugins are in `./plugins/`, (c) `$0.00` Claude Pro/Max local mode active, and (d) note that opening a new chat tab refreshes `/` plugin picker labels if plugins were newly registered, while `/run-*` commands work immediately.
   - Share the clickable Studio URLs returned by `gk serve --daemon` (defaulting to `http://127.0.0.1:4318/explainer`, `http://127.0.0.1:4318/setup`, `http://127.0.0.1:4318/manuals`, and `http://127.0.0.1:4318/board`).
   - Inspect `./plugins/` and list **only** the Outcome Workflows actually installed in this pack:
     - **Brand & Voice Setup**: `/run-brand-setup` (`/gk:run-brand-setup`)
     - **Daily Social & Voice** *(when `01-social-tov` is present)*: `/run-daily-social` (`/gk-social:run-daily-social`)
     - **Slide Decks, Banners & Pages** *(when `02-design-decks-pages` is present)*: `/run-deck-or-page` (`/gk-design:run-deck-or-page`)
     - **Animated Data Infographics** *(when `03-animated-infographics` is present)*: `/run-data-motion` (`/gk-motion:run-data-motion`)
     - **Short-Form Video Reels** *(when `04-shortform-video-engine` is present)*: `/run-short-video` (`/gk-video:run-short-video`)
     - **Prospect & Competitor Audits** *(when `05-agency-growth` is present)*: `/run-competitor-audit` (`/gk-agency:run-competitor-audit`)
     - **Creative Director & Angles** *(when `06-brainstorm-and-director` is present)*: `/run-creative-director` (`/gk-director:run-creative-director`)
