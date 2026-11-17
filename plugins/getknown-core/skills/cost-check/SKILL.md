---
name: cost-check
description: Use before running optional external paid APIs to check or reserve estimated USD spend against per-run and daily safety limits.
argument-hint: "[--client <slug>] [--estimated-usd <num>] [--dry-run|--reserve]"
effort: low
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit
---

# Pre-Flight Spend Check (`/cost-check`)

Claude Code runs on your regular Claude Pro, Max, or Team subscription with zero Anthropic API key or extra token billing. Workspace spend caps (`$2.50` per-run and `$15.00` daily) enforce budget checks before paid suite workflows call optional external APIs such as Gemini Image, ElevenLabs, Firecrawl, HeyGen, OpenRouter, or Apify.

## Subscription Models vs. Optional Paid Add-Ons

| Operation | Subscription Model / Optional Paid Add-On | Typical Add-On Cost (USD) | Free / Included Default |
|---|---|---|---|
| **Claude Strategy & Writing** | **Claude Opus** (default strategy & decks) and **Claude Sonnet** (fast daily batches & lighter weekly allowance) | `$0.00` extra | Included in your `Claude.app` Pro, Max, or Team subscription |
| **Hero / Slide Image (1x)** | Gemini Image (`GOOGLE_API_KEY`) | `$0.02 - $0.04` / image | Brand-tokenized HTML/SVG/PNG (`gk export-png`, `$0.00`) |
| **Hero / Slide Image (1x)** | OpenRouter Flux / Recraft (`OPENROUTER_API_KEY`) | `$0.04 - $0.06` / image | Brand-tokenized HTML/SVG/PNG (`gk export-png`, `$0.00`) |
| **Protected Website Crawl** | Firecrawl (`FIRECRAWL_API_KEY`) | `$0.01 - $0.05` / audit | Local headless Chromium `gk teardown` or saved `.html` page (`$0.00`) |
| **60s Voiceover (~750 chars)** | ElevenLabs (`ELEVENLABS_API_KEY`) | `$0.02 - $0.24` / minute | Local mic take in `capture-avatar.html` or macOS `say` (`$0.00`) |
| **60s Talking Avatar Video** | HeyGen API (`HEYGEN_API_KEY`) | `$1.00 - $2.00` / minute | Webcam circular PiP take in `capture-avatar.html` (`$0.00`) |
| **Social Scrape (20 posts)** | Apify (`APIFY_API_TOKEN`) | `$0.05 - $0.15` / run | `yt-dlp` transcripts or pasted URLs (`$0.00`) |

## Step-by-Step Workflow

1. **Estimate Planned Add-On Spend:**
   - Count how many optional paid images, voiceovers, or external crawls the batch requests. Pure Claude copy, HTML slides, local `ffmpeg` video cuts, and headless Chromium screenshots always cost `$0.00` extra.
2. **Run Read-Only Budget Check First:**
   ```bash
   ./plugins/getknown-core/bin/gk cost-check --client <slug> --estimated-usd <num> --dry-run
   ```
3. **Show the Spend Summary & Pause Above `$0.50`:**
   - Display `estimatedUsd`, `spentTodayUsd`, `dailyCapUsd`, `remainingUsd`, `allowed: true|false`, and the `$0.00` local alternative.
   - If `allowed` is `false`, halt immediately before calling any paid endpoint. Whenever estimated external API spend exceeds **`$0.50`**, ask for explicit user confirmation first.
4. **Reserve Budget With `--reserve` Before Calling Paid Endpoints:**
   - Once approved (and `allowed: true`), record the spend reservation explicitly with `--reserve` (omitting `--reserve` only runs a read-only check):
   ```bash
   ./plugins/getknown-core/bin/gk cost-check --client <slug> --estimated-usd <num> --reserve
   ```
