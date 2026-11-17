---
name: render-avatar-reel
description: Use when compositing a 60-second 9:16 short-form video with circular PiP avatar video or portrait, cleaned spoken audio, and synced captions.
argument-hint: "<campaign-id> [--client <slug>]"
context: fork
background: false
agent: gk:gk-renderer
effort: low
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(cp *), Read, Edit, Write
---

# 9:16 Avatar PiP Reel Compositor (`/render-avatar-reel`)

Combine the 5-beat script (`/brand-teardown-script`), captured website proof screenshots (`/harvest-visual-proof`), and narrator video or voiceover into a `1080x1920` (`30fps`, `60s` / `1800`-frame) vertical MP4 reel. The narrator appears **full-screen during Beat 1 (`00:00.0-00:03.5`), Beat 3 (`00:25.0-00:27.5`), and Beat 5 (`00:50.0-01:00.0`)**, and transitions into a **`280x280px` circular Picture-in-Picture bubble (`right: 48px, bottom: 260px`)** during proof beats.

## Single-Clock Compositor Rule

- **HTML + CSS (`${CLAUDE_PLUGIN_ROOT}/templates/reel-9x16-pip/index.html`) owns all 9:16 layout**, `<video id="avatar-video">` inside `#avatar-container`, `border-radius: 50%` circular PiP masking, and `window.__hyperframesSeek(frame)` beat transitions.
- **`gk render-video` serves the composition over a jailed local loopback server, seeks `window.__hyperframesSeek` and `<video>` frame-by-frame, balances spoken loudness, and muxes H.264/AAC MP4.**

## Step 1: Select & Clean Narrator Source

1. **Local Webcam & Mic Take (`capture-avatar.html`, `$0.00`):**
   - Start the Studio server via `./plugins/getknown-core/bin/gk serve --daemon` and open `<baseUrl>/plugins/04-shortform-video-engine/templates/capture-avatar.html` (template path `${CLAUDE_PLUGIN_ROOT}/templates/capture-avatar.html`).
   - Record or upload a `.webm` or `.mp4` take, then clean dead pauses and balance spoken audio via `./plugins/getknown-core/bin/gk splicebay <raw-take> --client <client> --out clients/<client>/campaigns/<sprint>/assets/clean-narrator.mp4`.
2. **Founder Portrait + Voiceover Audio (`$0.00`):**
   - Bind a real founder photo or `<video id="avatar-video">` inside `#avatar-container` paired with recorded voiceover audio matching the full reel duration.
3. **Optional Paid Voice & Avatar (`ELEVENLABS_API_KEY`, `HEYGEN_API_KEY`):**
   - Run `./plugins/getknown-core/bin/gk cost-check --client <client> --estimated-usd 0.25 --dry-run` (and `--reserve` once confirmed) first, generate the clip, and reference it in `reel-9x16-pip.html`.

## Step 2: Populate Reel Stage Template

Copy `${CLAUDE_PLUGIN_ROOT}/templates/reel-9x16-pip/index.html` (repo fallback `./plugins/04-shortform-video-engine/templates/reel-9x16-pip/index.html`) into `clients/<client>/campaigns/<sprint>/assets/reel-9x16-pip.html`, bind `clients/<client>/brand/tokens.json`, point `#avatar-video` (or portrait `<img>`) at the narrator asset, and embed `reel-script.json` with `<` escaped as `\u003c`.

## Step 3: Render Full `60s` MP4

Always pass `--duration 60` (or match the exact audio duration and frame count on `#stage`) so a 60-second `1800`-frame reel renders at `1x` speed:

```bash
./plugins/getknown-core/bin/gk render-video \
  --html clients/<client>/campaigns/<sprint>/assets/reel-9x16-pip.html \
  --audio clients/<client>/campaigns/<sprint>/assets/clean-narrator.mp4 \
  --out clients/<client>/campaigns/<sprint>/exports/reel-final.mp4 \
  --width 1080 \
  --height 1920 \
  --duration 60 \
  --frames 1800 \
  --fps 30
```
