---
description: Use when turning a brand teardown or raw talking-head take into a ready-to-publish 9:16 short-form video reel with PiP avatar and captions.
argument-hint: "<prospect-or-topic-url> [--client <slug>] [--resume <runId>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp *), Read, Grep, Glob, Edit, Write, Agent
---

# `/run-short-video` (`/gk-video:run-short-video`) · Outcome Workflow (`04-shortform-video-engine`)

## Flow Contract & Checkpoint Recovery
- **Owning Plugin:** `gk-video` (`04-shortform-video-engine`), available directly as `/run-short-video` (and `/gk-video:run-short-video` in the `/` picker).
- **Recommended Models (Included in Claude Pro & Max):** **Claude Opus 5.5** (`opus`, default) for beat-clock scripting; **Claude Sonnet 5.5** (`sonnet`, `high` effort) for proof harvesting and PiP compositing.
- **Checkpoint State:** Initialize `clients/<slug>/` if new (`gk client init <slug> --url <url>`), then run `gk flow start run-short-video --client <slug>` (inspect or resume via `gk flow status --client <slug>`, fallback `./plugins/getknown-core/bin/gk`).
- **Primary Outputs:** `clients/<slug>/campaigns/<id>/exports/reel-final.mp4`, `clients/<slug>/campaigns/<id>/drafts/reel-script.json`

## Ordered Execution Steps
1. **`splicebay-ingest`:** Ensure `clients/<slug>/` exists (`gk client init <slug> --url <url>`), start `gk flow start run-short-video --client <slug>` (if not already active), fork `gk teardown --client <slug> --url <url> --crawl-depth 2` and `/harvest-visual-proof` (`gk harvest-proof`) in parallel to `gk:gk-researcher` (`sonnet`), and advance `gk flow step splicebay-ingest --client <slug>`.
2. **`transcribe-audio`:** Advance `gk flow step transcribe-audio --client <slug>`, run `/brand-teardown-script` inline (`high`), capture or load the narrator take (`capture-avatar.html` or connected voiceover), and run `gk splicebay <video-or-audio-path> --client <slug>` for word timing, silence/retake trimming, and balanced spoken audio.
3. **`apply-camera-cuts`:** Advance `gk flow step apply-camera-cuts --client <slug>` and bind the 5-beat script (`3.2 words/sec` budget) and `<video id="avatar-video">` PiP cuts into `reel-9x16-pip.html`.
4. **`composite-shortform`:** Advance `gk flow step composite-shortform --client <slug>`, fork `/render-avatar-reel` (`gk:gk-renderer`, `sonnet`) to render `reel-final.mp4` (`gk render-video --width 1080 --height 1920 --fps 30 --duration 60`), register `exports/reel-final.mp4` (`assetPath`) in `clients/<slug>/campaigns/<id>/drafts/draft-pack.json` for rich Approval Board metadata, launch `./plugins/getknown-core/bin/gk serve --daemon` to share the `/board?client=<slug>` URL, run `/publish-shortform` after approval, and mark `gk flow complete run-short-video --client <slug>`.
