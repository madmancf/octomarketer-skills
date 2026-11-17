---
name: provider-connector
description: Use when checking local tool readiness or connecting optional external API keys safely without pasting secrets into chat.
argument-hint: "[--client <slug>]"
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read
---

# Provider & Optional Add-On Connector (`/provider-connector`)

Every installed workflow in your pack runs in **free local mode (`$0.00`)** using your regular Claude Pro, Max, or Team subscription (**Claude Opus 5.5** and **Claude Sonnet 5.5**), and connects to optional external services only when you configure keys on your machine.

## Local Default vs. Optional Connected Services

| Area | Free Local Default (`$0.00`, Zero Signup) | Optional Connected Services |
|---|---|---|
| **1. Website & SPA Funnel Audits** | `gk teardown --crawl-depth 2` (bundled headless Chromium DOM + 7-channel heuristic rubric) & `gk harvest-proof` | **Firecrawl** (`FIRECRAWL_API_KEY`), **Exa / Perplexity** (`EXA_API_KEY`, `PERPLEXITY_API_KEY`), **Apify** (`APIFY_API_TOKEN`) |
| **2. SEO & Keyword Data** | Local title, meta, headings, OpenGraph, and JSON-LD check | **Ahrefs** (`AHREFS_API_KEY`), **DataForSEO** (`DATAFORSEO_LOGIN` + `DATAFORSEO_PASSWORD`) |
| **3. Brand Tokens, Decks & Graphics** | `gk brand-extract` + `gk export-pptx` (`.pptx`), `gk export-pdf` (`.pdf`), `gk export-png` (`.png`) | **OpenRouter** (`OPENROUTER_API_KEY`), **Fal / Replicate** (`FAL_KEY`, `REPLICATE_API_TOKEN`), **Gemini Image** (`GOOGLE_API_KEY`) |
| **4. Short-Form Video & Voice** *(when `04-shortform-video-engine` is installed)* | `capture-avatar.html` recorder + `gk splicebay` (`ffmpeg` silence cuts + local `whisper-cli` word timing when model is downloaded) + `gk render-video` | **Splicebay Video Editor** (`SPLICEBAY_URL` + optional `SPLICEBAY_API_KEY`), **ElevenLabs** (`ELEVENLABS_API_KEY`), **HeyGen** (`HEYGEN_API_KEY`) |
| **5. Client Approval Links & Delivery** | Local `<campaign>-review-pack.zip` (with optional passcode encryption) via `gk publish-review-link --provider local` | **Cloudflare Pages** (`CF_PAGES_TOKEN` + `CF_ACCOUNT_ID`), **Vercel** (`VERCEL_TOKEN`), **Postiz** (`POSTIZ_API_KEY`), **Clay**, **Instantly** |

## Step 1: Check Current Readiness

Inspect `./plugins/` to see which pack modules are installed, then run the read-only health check:
```bash
./plugins/getknown-core/bin/gk provider-health
```

Summarize configured vs. unconfigured optional services (`status: "configured"`) and installed local media tools (`ffmpeg`, `whisper-cli`, `yt-dlp`) in plain English without dumping the raw JSON payload.

## Step 2: Choose Optional Add-Ons

Ask which setup the user wants:
- **Option A: Free Local Default (`$0.00`):** Zero keys needed. Every installed plugin works locally right away.
- **Option B: Cloud Client Approval Links (`CF_PAGES_TOKEN` + `CF_ACCOUNT_ID` or `VERCEL_TOKEN`):** Publishes passcode-encrypted HTTPS review links from the Approval Board.
- **Option C: Research & SEO (`FIRECRAWL_API_KEY`, `AHREFS_API_KEY`, `DATAFORSEO_LOGIN`, `DATAFORSEO_PASSWORD`, `EXA_API_KEY`, `APIFY_API_TOKEN`):** Adds keyword volume, SERP, and social crawl enrichment.
- **Option D: Voice, Image & Video Add-Ons (`GOOGLE_API_KEY`, `OPENROUTER_API_KEY`, `FAL_KEY`, `ELEVENLABS_API_KEY`, `HEYGEN_API_KEY`, `SPLICEBAY_URL`):** Adds AI hero art, synthetic voiceovers/avatars, or an optional companion Splicebay server (when `04-shortform-video-engine` is installed).

## Step 3: Save Keys Locally Without Pasting Into Chat

**Hard Security Rule:** Never ask the user to paste an API key into chat, and never pass a secret key as a CLI command-line argument (which exposes secrets in chat transcripts and process history).

Give the user these two safe local options:
1. **Text Editor Option:** Copy `.env.example` to `.env.local` in Finder, open `.env.local` in TextEdit, paste `KEY=VALUE`, and save.
2. **Terminal Stdin Option (`0600` owner-only permissions):** Have the user run this in their own Mac Terminal window:
   ```bash
   printf '%s' 'KEY=VALUE' | ./plugins/getknown-core/bin/gk provider-health --set-stdin
   ```

Once the user saves the file, run read-only `./plugins/getknown-core/bin/gk provider-health` to verify the provider status is `"configured"`.
