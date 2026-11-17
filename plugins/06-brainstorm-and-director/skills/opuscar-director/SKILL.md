---
name: opuscar-director
description: Use when directing code-generated films, animated explainers, or parameterized ad batches using Lemo-Opuscar (59 modular library styles #12..#70 + 98 film anthology showcase specs), Remotion, or the HTML stage compositor.
argument-hint: "[<topic-or-script>] [--engine opuscar|remotion|html] [--style #12..#70|<style-slug>] [--client <slug>]"
context: fork
background: false
agent: gk:gk-renderer
effort: high
allowed-tools: Bash(gk *), Bash(~/.local/bin/gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(npx *), Bash(node *), Bash(python3 *), Bash(uv *), Bash(ffmpeg *), Bash(whisper-cli *), Read, Grep, Glob, Edit, Write
---

# Code-Driven Film & Motion Director (`/opuscar-director`)

Direct code-to-video jobs on **Claude Opus 5.5** (`claude-opus-5-5` / `opus`) or `gk:gk-renderer` (**Claude Sonnet 5.5**, `claude-sonnet-5-5` / `sonnet`, `high` effort) across **`lemomo-ai/lemo-opuscar` (59 modular library styles `#12..#70` + 98 film anthology showcase specs, invoked via `/lemo-opuscar`)**, **Remotion (`remotion` + `@remotion/captions`)**, and **HTML stage video (`gk render-video`)**, bound to `brand/tokens.json` (`./brand/tokens.json` or `clients/<slug>/brand/tokens.json`).

## Bidirectional Template Handshake (`#12..#70` in `template-registry.json`)

- **Shared Catalog:** `plugins/getknown-core/templates/template-registry.json` assigns `#12`..`#70` across all **59 modular `lemo-opuscar` library styles** (plus the **98 film anthology showcase specs** under `anthology98`).
- **If the user already named a `#12..#70` number (such as `#24` or `#35`) or a real `<slug>` (such as `dark-keynote` or `iso-infographic`) in chat or `$ARGUMENTS`:** Resolve that style immediately and begin directing without redundant questions.
- **If the user did NOT pick a `#NN` number or `<slug>` yet:** Start the local Studio server via `gk serve --daemon` (fallback `~/.local/bin/gk` or `./plugins/getknown-core/bin/gk`), share the clickable visual gallery URL `http://127.0.0.1:<port>/templates?pack=lemo-opuscar` (default `http://127.0.0.1:4318/templates?pack=lemo-opuscar`), highlight 3 to 5 curated `#NN <slug>` picks matching their brief, and ask which `#NN` or `<slug>` they want!

## Step 1: Pick the Right Video Engine

| Job Type | Engine | How It Runs |
| :--- | :--- | :--- |
| **Brand Trailers, Evidence Films, Launch Keynote Shorts (15 to 60s)** | **`lemomo-ai/lemo-opuscar`** (`/lemo-opuscar`) | **59 modular library styles (`#12..#70`)** (+ **98 film anthology showcase specs**) in 2D Canvas, 2.5D, and WebGL with procedural `python3 >= 3.11` audio + `ffmpeg`. |
| **Parameterized React Ad Batches & Word-Synced Captions** | **Remotion** (optional `remotion`, `@remotion/cli`, `@remotion/captions`, `@remotion/transitions`) | React `<Composition>` + `useCurrentFrame()` + `spring()` + `@remotion/captions` synced to `whisper-cli` word timestamps. |
| **4:5 LinkedIn Animated Infographics & 9:16 PiP Reels** | **HTML Stage Compositor** (`gk render-video`) | Single `.html` stage (`#01..#03` or `#08`, `window.__hyperframesSeek(frame)` + local `Plus Jakarta Sans` `.woff2`) served over jailed loopback HTTP and captured at `30fps` via bundled `Google Chrome for Testing` + `ffmpeg`. |

## Step 2: Directing With `lemomo-ai/lemo-opuscar` (59 Modular Library Styles `#12..#70` + 98 Anthology Specs)

### Check Local Tools & Companion Plugin
Run `gk diagnose --json` (or `gk setup-machine`). If `lemo-opuscar@lemolab` is not installed yet:
```bash
claude plugin marketplace add lemomo-ai/lemo-opuscar
claude plugin install lemo-opuscar@lemolab
```
Once installed, invoke `/lemo-opuscar` (or direct scenes from `gk:gk-renderer`).

### Verified Curated Style Numbers & Slugs (`#12..#70`, On-Disk Ground Truth)
1. **Launch Keynote, Product & Data Explainers:**
   - `#24` `dark-keynote`, `#35` `iso-infographic`, `#60` `swiss-motion`, `#29` `glass-product`, `#38` `living-screencast`, `#49` `pictogram-motion`, `#69` `whiteboard`, `#16` `blueprint`, `#26` `dataviz`, `#45` `one-line`.
2. **Evidence, Dossier & Audit Films (sourced from `campaigns/<id>/sources/`):**
   - `#18` `briefing-board`, `#25` `data-physical`, `#61` `teardown`, `#53` `satellite-briefing`, `#37` `lidar-survey`, `#68` `white-model`, `#41` `microscope`, `#12` `archive-lighttable`, `#30` `halftone-dossier`.
3. **Documentary, News & Editorial Cutdowns (built from live `gk harvest-proof` screenshots and verified metrics):**
   - `#62` `telestrator`, `#19` `caption-news`, `#66` `visual-investigation`, `#43` `news-package`, `#22` `countdown`, `#36` `kino-montage`, `#51` `risograph`, `#57` `silkscreen-poster`.

*(All 59 library styles `#12` `archive-lighttable` through `#70` `woodcut` plus the 98 Oscar film anthology showcase specs are browsable visually at `/templates?pack=lemo-opuscar`.)*

### Custom Brand Styles
1. Read `brand/tokens.json` (`colors.*`, `typography.*`) and `tov/tov.md`.
2. Pick the closest verified base slug (such as `#24` `dark-keynote`, `#35` `iso-infographic`, `#60` `swiss-motion`, `#19` `caption-news`, or `#62` `telestrator`), render 1 comparison frame for review, save custom style overrides strictly inside `./brand/styles/<style-slug>/` or `clients/<slug>/brand/styles/<style-slug>/` (never write outside the project workspace into user-home folders), and export the final MP4 into `campaigns/<id>/exports/`.

## Step 3: Directing With Remotion
1. Install optional Remotion packages (`npm install --save-optional remotion @remotion/cli @remotion/captions @remotion/transitions`) if not yet in `node_modules/`.
2. Transcribe spoken audio locally via `whisper-cli` (or `gk splicebay <video-or-audio> --client <slug>`) for word-level timestamps.
3. Pass `brand/tokens.json` into the Remotion `<Composition>` props and render via `npx remotion render` into `campaigns/<id>/exports/`.
