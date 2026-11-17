---
name: setup-marketer
description: Use when setting up a marketing studio folder, creating brand workspaces, checking local Mac or Windows tools, or configuring Claude Desktop.
argument-hint: "[--client <slug>] [--install]"
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp *), Bash(git *), Read, Edit, Write
---

# Marketer Workspace & Machine Setup (`/setup-marketer`)

Set up a clean marketing studio folder (~2 to 3 minutes on your first run; instant after that), register this pack's plugins, verify local export and media tools, and launch the Studio web view.

## Step 1: Check Node.js & Verify Workspace Folder Layout

First verify `command -v node`. If Node.js 20+ is missing, direct the user to download the standard `.pkg` (macOS) or `.msi` (Windows) installer at https://nodejs.org before running Studio scripts.

If the current folder does not yet have `clients/` and `CLAUDE.md`, scaffold from `${CLAUDE_PLUGIN_ROOT}/workspace-template/` (repo fallback `./plugins/getknown-core/workspace-template/`). To create a brand folder cleanly, run `./plugins/getknown-core/bin/gk client init <brand-slug> --name "<Brand Name>"`.

Confirm the workspace layout and line caps:
1. **Studio Root (`./CLAUDE.md`, `<= 120` lines):** Workspace router, client isolation rules (`clients/demo-brand/` is ignored automatically once a real brand exists), and the Outcome Workflows installed in `./plugins/`.
2. **Per-Client Folder (`clients/<slug>/`):**
   - `clients/<slug>/CLAUDE.md` (`<= 150` lines: audience, offer, guardrails)
   - `clients/<slug>/brand/{tokens.json,design.md,assets/,styles/}`
   - `clients/<slug>/tov/{tov.md,winners/,anti-examples/}` (`tov.md <= 250` lines)
   - `clients/<slug>/campaigns/<YYYY-MM-sprintN>/{sources/,drafts/,assets/,exports/}`

## Step 2: Check Local Tools & Register Pack Plugins

Run the machine readiness check:
```bash
node ./plugins/getknown-core/bin/gk setup-machine
```

To install optional workspace packages, verify bundled `Google Chrome for Testing`, and register the local plugin marketplace:
```bash
node ./plugins/getknown-core/bin/gk setup-machine --install
```
- **Pack-Aware Media Tools:** `ffmpeg` and `whisper-cpp` (`brew install ffmpeg whisper-cpp yt-dlp` on macOS) are only needed when `03-animated-infographics` or `04-shortform-video-engine` is installed in `./plugins/`. `agency-pack` runs PDF, PowerPoint, and PNG exports without `ffmpeg`.
- If plugins were newly registered, start a fresh chat tab in `Claude.app` to refresh `/` plugin menu labels (bare `/run-*` commands work immediately).

## Step 3: `Claude.app` (`</> Code` Tab) Checklist

Walk through these settings (shown visually on the Setup Guide page):
1. **Open the `</> Code` Tab:** Open `Claude.app`, click **`</> Code`** at the top, and select your unzipped studio folder inside `Documents` (outside `Downloads`).
2. **Keep Mode on `Local` + `Open folder...`:** Keep the session dropdown under the message box on **`Local`** so drafts and exports save directly into your folder.
3. **Select `Accept edits`:** Choose **`Accept edits`** in the permission dropdown. `.claude/settings.json` pre-approves local `gk` commands and local `.zip` exports, prompts before cloud uploads (`vercel` / `cloudflare`) or `undo`, and protects `.env` / `.env.local` secrets while leaving `.env.example` readable.
4. **Pick Your Model (Included in Claude Pro & Max):** Choose the latest **Claude Opus** (`opus`) model in `Claude.app` for brand strategy, voice guides, slide decks, and creative direction, or **Claude Sonnet** (`sonnet`) for fast daily post batches, hook variations, and background subagents (**Claude Haiku** `haiku` is also available for quick checks).

## Step 4: Verify Secret Guard & Start Background Studio Server

```bash
./plugins/getknown-core/bin/gk secret-guard
./plugins/getknown-core/bin/gk provider-health
./plugins/getknown-core/bin/gk serve --daemon
```
Summarize readiness in 3 to 4 plain-English bullets (do not dump raw JSON) and share the live `/setup`, `/manuals`, and `/board` URLs returned by `gk serve --daemon`.
