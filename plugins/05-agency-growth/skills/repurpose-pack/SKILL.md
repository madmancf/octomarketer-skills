---
name: repurpose-pack
description: Use when turning a webinar transcript, course lesson, or long-form video into a multi-format social and content campaign matched to your installed pack.
argument-hint: "<transcript-path> [--client <slug>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(cp *), Read, Grep, Glob, Edit, Write, Agent
---

# Multi-Format Content Repurposing Engine (`/repurpose-pack`)

Extract verified claims, frameworks, and stories from one long-form webinar, workshop, or podcast transcript and build a coordinated multi-asset campaign sprint tailored to the plugins installed in `./plugins/`.

## Step 1: Mine the Long-Form Source & Check Installed Pack Plugins

First inspect `./plugins/` so you only invoke creative skills present in the current pack (`full-suite` vs. `agency-pack`). Then accept a transcript file, video URL (fetched via `yt-dlp` when installed), markdown article, or slide deck, and extract:
1. **3 Specific Claims or Metrics** (with exact quotes or timestamps from the source).
2. **1 Step-by-Step Process** (4 to 5 concrete steps for a swipe carousel and benchmark infographic).
3. **1 Teardown Story or Case Study** (for a founder case-study breakdown or short-form script).

## Step 2: Generate the Pack-Matched Sprint Deliverables

Write all assets into `clients/<client>/campaigns/<sprint>/` matching the active channels in `clients/<client>/CLAUDE.md`:
1. **3 LinkedIn Posts** (`draft-pack.json`: 1 contrarian claim, 1 process breakdown, 1 case-study lesson; run `/draft-post` when `01-social-tov` is installed, or draft directly against `tov/tov.md` + `gk lint`).
2. **2 Short-Form Channel Posts** (`draft-pack.json`: Instagram, X, or Telegram notes matched to the client's active channels).
3. **1 `4:5` LinkedIn Swipe Carousel** (`assets/carousel-deck.html` + `.pdf` + `.pptx` via `/slide-deck` in `02-design-decks-pages`).
4. **1 Infographic Card:**
   - If `03-animated-infographics` is installed in `./plugins/`, build an animated `4:5` infographic (`assets/infographic-flow.html` + `.png` / `30fps` `.mp4`) via `/build-infographic`.
   - If `03-animated-infographics` is **not** installed (`agency-pack`), populate `./plugins/05-agency-growth/templates/standalone-infographic.html` into `assets/infographic-benchmark.html` and export crisp `.png` via `gk export-png`.
5. **1 Video Script or Executive Brief:**
   - If `04-shortform-video-engine` is installed in `./plugins/`, write a 60s `9:16` beat-clock reel script (`drafts/reel-script.json`) via `/brand-teardown-script`.
   - If `04-shortform-video-engine` is **not** installed (`agency-pack`), write a 1-page executive summary brief (`assets/executive-brief.md`) or direct a trailer brief via `/opuscar-director` (`06-brainstorm-and-director`) instead of referencing uninstalled reel skills.

## Step 3: Readability Check & Approval Board

- Check every post and script via `./plugins/getknown-core/bin/gk lint --file <draft-path> --platform linkedin`.
- Start the Studio server in background daemon mode via `./plugins/getknown-core/bin/gk serve --daemon` and share the `/board?client=<client>` URL so the user reviews the full batch in one place.
