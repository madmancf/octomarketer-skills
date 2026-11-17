---
name: discover-claude-code
description: Use when onboarding a marketer to Claude Desktop, explaining brand folders, slash commands, and visual browser pages.
argument-hint: "[--client <slug>]"
effort: low
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Read
---

# Discover Claude Desktop for Marketers (`/discover-claude-code`)

Walk a marketer through how `Claude.app` (`</> Code` tab) works on Day 1 and open the local visual Studio in the background.

## Step 1: Start the Background Studio Server

First check `command -v node` (if missing, direct the user to install the standard `.pkg` or `.msi` installer from https://nodejs.org). Then launch the Studio server in daemon mode so it returns immediately with live URLs:

```bash
./plugins/getknown-core/bin/gk serve --daemon
```

Share the returned `setupUrl` and `explainerUrl` (default `http://127.0.0.1:4318/explainer` and `http://127.0.0.1:4318/setup`) with the user.

## Step 2: Explain Real `Claude.app` Tabs, Controls & Models

1. **Why We Open Your Folder in the `</> Code` Tab:**
   - **Browser Chat (`claude.ai`):** Useful for quick standalone questions, though it cannot open your local folder or export local decks, banners, and videos.
   - **`</> Code` Tab (`Claude.app`):** Open `Claude.app`, click **`</> Code`** at the top, and select your unzipped studio folder (or open `START-HERE.html` first in Finder) so Claude reads your brand files and saves finished drafts directly inside your folder.

2. **Prompt-Bar Controls in `</> Code`:**
   - **Folder Mode (`Local` + `Open folder...`):** Keep the dropdown under the message box on **`Local`** and select your unzipped studio folder inside `Documents`.
   - **Permission Mode:** Modes under the message box are **`Manual`**, **`Accept edits`** (recommended), **`Plan`**, and **`Auto`**.
   - **Models (Included in Your Claude Pro or Max Subscription):** Choose **Claude Opus 5.5** (`claude-opus-5-5` / `opus`) in `Claude.app` for brand strategy, voice guides, flagship posts, slide decks, and creative direction. Switch to **Claude Sonnet 5.5** (`claude-sonnet-5-5` / `sonnet`, `high` effort) for diagnostics, fast daily post batches, hook variations, and lighter use of your weekly subscription allowance (**Claude Haiku 5.5** `haiku` is also available for quick checks).
   - **Plain English or Slash Commands:** Type a plain-English request (`"Audit https://example.com and build a 5-slide pitch deck"`) or a workflow command (`/run-brand-setup`, `/run-deck-or-page`, `/run-creative-director`, plus any pack-specific workflows in `./plugins/`).

3. **One Folder Per Brand (`clients/<brand-name>/`):**
   - Each brand keeps its own `CLAUDE.md` (`<= 150` lines), brand palette, voice profile (`<= 250` lines), and campaign folders without mixing assets across clients.

## Step 3: Next Step

Ask: *"Ready to check your tools and create your first brand folder? Type `/quickstart` or `/run-brand-setup` next."*
