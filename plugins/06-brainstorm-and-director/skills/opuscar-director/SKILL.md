---
name: opuscar-director
description: Use when directing code-generated films, animated explainers, or parameterized ad batches using Lemo-Opuscar (99 upstream styles), Remotion, or the HTML stage compositor.
argument-hint: "[<topic-or-script>] [--engine opuscar|remotion|html] [--style <style-name>] [--client <slug>]"
context: fork
background: false
agent: gk:gk-renderer
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(npx *), Bash(node *), Bash(python3 *), Bash(uv *), Bash(ffmpeg *), Bash(whisper-cli *), Read, Grep, Glob, Edit, Write
---

# Code-Driven Film & Motion Director (`/opuscar-director`)

Direct code-to-video jobs on **Claude Opus** (`opus`) or `gk:gk-renderer` (**Claude Sonnet**, `sonnet`) across **`lemomo-ai/lemo-opuscar` (`99` upstream film styles, invoked via `/lemo-opuscar`)**, **Remotion (`remotion` + `@remotion/captions`)**, and **HTML stage video (`gk render-video`)**, bound to `clients/<slug>/brand/tokens.json`.

## Step 1: Pick the Right Video Engine

| Job Type | Engine | How It Runs |
| :--- | :--- | :--- |
| **Brand Trailers, Evidence Films, Launch Keynote Shorts (15 to 60s)** | **`lemomo-ai/lemo-opuscar`** (`/lemo-opuscar`) | `99` upstream code-built styles in 2D Canvas, 2.5D, and WebGL with procedural `python3 >= 3.11` audio + `ffmpeg`. |
| **Parameterized React Ad Batches & Word-Synced Captions** | **Remotion** (optional `remotion`, `@remotion/cli`, `@remotion/captions`, `@remotion/transitions`) | React `<Composition>` + `useCurrentFrame()` + `spring()` + `@remotion/captions` synced to `whisper-cli` word timestamps. |
| **4:5 LinkedIn Animated Infographics & 9:16 PiP Reels** | **HTML Stage Compositor** (`gk render-video`) | Single `.html` stage (`window.__hyperframesSeek(frame)` + local `Plus Jakarta Sans` `.woff2`) served over jailed loopback HTTP and captured at `30fps` via bundled `Google Chrome for Testing` + `ffmpeg`. |

## Step 2: Directing With `lemomo-ai/lemo-opuscar` (`99` Upstream Styles)

### Check Local Tools & Companion Plugin
Run `./plugins/getknown-core/bin/gk setup-machine`. If `lemo-opuscar@lemolab` is not installed yet:
```bash
claude plugin marketplace add lemomo-ai/lemo-opuscar
claude plugin install lemo-opuscar@lemolab
```
Once installed, invoke `/lemo-opuscar` (or direct scenes from `gk:gk-renderer`).

### Verified Style Slugs for Marketers & Agencies
1. **Launch Keynote & Product Trailers:**
   - `dark-keynote`, `swiss-motion`, `glass-product`, `desktop-flythrough`, `whiteboard`, `chalkboard`, `transit-map`, `memphis-diorama`, `isometric-picture-book`.
2. **Evidence & Audit Films (sourced from `campaigns/<id>/sources/`):**
   - `briefing-board`, `data-physical`, `teardown`, `satellite-briefing`, `lidar-survey`, `white-model`, `microscope`, `archive-lighttable`.
3. **Documentary & News Cutdowns (built from live `gk harvest-proof` screenshots and verified metrics):**
   - `telestrator`, `caption-news`, `visual-investigation`, `news-package`, `countdown`, `kino-montage`.

### Custom Client Brand Styles
1. Read `clients/<slug>/brand/tokens.json` (`colors.*`, `typography.*`) and `clients/<slug>/tov/tov.md`.
2. Pick the closest verified base slug (such as `dark-keynote`, `swiss-motion`, `caption-news`, or `telestrator`), render 1 comparison frame for review, save custom style overrides strictly inside `clients/<slug>/brand/styles/<style-slug>/` (never write outside the client workspace into user-home folders), and export the final MP4 into `clients/<slug>/campaigns/<id>/exports/`.

## Step 3: Directing With Remotion
1. Install optional Remotion packages (`npm install --save-optional remotion @remotion/cli @remotion/captions @remotion/transitions`) if not yet in `node_modules/`.
2. Transcribe spoken audio locally via `whisper-cli` (or `./plugins/getknown-core/bin/gk splicebay <video-or-audio> --client <slug>`) for word-level timestamps.
3. Pass `clients/<slug>/brand/tokens.json` into the Remotion `<Composition>` props and render via `npx remotion render` into `clients/<slug>/campaigns/<id>/exports/`.
