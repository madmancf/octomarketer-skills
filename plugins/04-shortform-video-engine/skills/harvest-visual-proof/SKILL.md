---
name: harvest-visual-proof
description: Use when capturing high-DPI website, headline, and pricing proof screenshots for a short-form teardown video or audit deck.
argument-hint: "<target-url> [--client <slug>]"
context: fork
background: false
agent: gk:gk-researcher
effort: low
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Edit, Write, WebFetch
---

# Visual Proof & B-Roll Harvester (`/harvest-visual-proof`)

Capture real, high-DPI website screenshots and verified funnel facts for `reel-9x16-pip/index.html` and agency audit decks using bundled headless `Google Chrome for Testing`.

## Step 1: Read Beat Visual Cues

Ensure `clients/<client>/` exists (`./plugins/getknown-core/bin/gk client init <client> --url <target-url>` if new), then load `clients/<client>/campaigns/<sprint>/drafts/reel-script.json` and list the 4 visual proof slots needed during **Beat 2 (`00:03.5 - 00:25.0`)** and **Beat 4 (`00:27.5 - 00:50.0`)**.

## Step 2: Capture Live Website Screenshots & Audit Data

Run both commands against an explicit `<target-url>` (using bundled `Google Chrome for Testing`, never branded Chrome):
1. **Capture High-DPI Proof Screenshots:**
   ```bash
   ./plugins/getknown-core/bin/gk harvest-proof \
     --client <client> \
     --url <target-url> \
     --out clients/<client>/campaigns/<sprint>/assets/proof
   ```
2. **Extract Verified Headlines, Pricing & Subpages:**
   ```bash
   ./plugins/getknown-core/bin/gk teardown --client <client> --url <target-url> --crawl-depth 2
   ```
3. **Optional Paid Graphics (`GOOGLE_API_KEY` / `OPENROUTER_API_KEY`):**
   - Only if a beat needs an extra diagram via Gemini Image or OpenRouter, run `./plugins/getknown-core/bin/gk cost-check --client <client> --estimated-usd 0.05 --dry-run` (and `--reserve` once confirmed) first. Never fabricate website quotes or invent unverified benchmark numbers.

## Step 3: Save Proof Manifest

Confirm all captured PNG proof snapshots sit under `clients/<client>/campaigns/<sprint>/assets/proof/` and update `reel-script.json` with their relative paths for `/render-avatar-reel`.
