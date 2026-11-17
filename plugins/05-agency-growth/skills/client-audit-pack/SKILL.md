---
name: client-audit-pack
description: Use when generating a 5-minute prospect pitch pack: 7-channel website teardown, prospect-branded HTML/PDF/PPTX audit deck, 2 sample posts, and 1 static benchmark infographic.
argument-hint: "<prospect-url> [--client <slug>] [--crawl-depth 1|2|3] [--no-attribution]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Bash(cp *), Read, Edit, Write, Agent
---

# 5-Minute Prospect Teardown & Audit Pack (`/client-audit-pack`)

Build a prospect-branded pitch kit from an explicit live URL in free local mode (`$0.00`), with optional SEO and outbound enrichment when BYOK keys are configured on your machine.

## Local & Connected Audit Inputs

| Step | Free Local Default (`$0.00`) | Optional Connected Services |
|---|---|---|
| **1. SPA & Multi-Page Site Audit** | `gk teardown --crawl-depth 2` (bundled headless Chromium DOM rendering for React/Vite SPAs + `sitemap.xml` + deduplicated internal `/pricing`, `/customers`, `/blog`, `/about` pages scored with the disclosed heuristic HTML rubric across 7 channels) | **Firecrawl** (`FIRECRAWL_API_KEY`), **Exa / Perplexity** (`EXA_API_KEY`, `PERPLEXITY_API_KEY`), **Apify** (`APIFY_API_TOKEN`) |
| **2. SEO & Schema Check** | Local title, meta description, H1/H2 hierarchy, OpenGraph, and JSON-LD schema audit | **Ahrefs** (`AHREFS_API_KEY`), **DataForSEO** (`DATAFORSEO_LOGIN` + `DATAFORSEO_PASSWORD`) |
| **3. Brand Tokens & Contrast** | `gk brand-extract` (live Chromium DOM probing + dark luminance guard on `brandBlack`, falling back cleanly if 0 brand hexes match) | Same local token extractor |
| **4. Shareable Delivery** | `gk publish-review-link --provider local` packages `pitch-audit-review-pack.zip` with `.pdf`/`.pptx`/`.png` deliverables (pass `--no-attribution` to strip suite header/footer badges on white-label agency pitches) | **Cloudflare Pages** / **Vercel**, **Clay**, **Instantly** |

## Step 1: Initialize Prospect Folder, Extract Brand Tokens & Run 7-Channel Audit

Initialize `clients/<prospect-slug>/` first and pass an explicit `--url <prospect-url>` (include `--no-attribution` when white-labeling for an agency prospect):

```bash
./plugins/getknown-core/bin/gk client init <prospect-slug> --url <prospect-url>
./plugins/getknown-core/bin/gk brand-extract --client <prospect-slug> --url <prospect-url>
./plugins/getknown-core/bin/gk teardown --client <prospect-slug> --url <prospect-url> --crawl-depth 2 [--no-attribution]
```

Then write `clients/<prospect-slug>/CLAUDE.md` (`<= 150` lines) and initialize `clients/<prospect-slug>/tov/tov.md` via `./plugins/getknown-core/bin/gk tov init --client <prospect-slug>`.

## Step 2: Build the 3 Pitch Deliverables

1. **5-Slide Branded Audit Deck (`standalone-audit-deck.html` + `.pdf` + `.pptx`):**
   - Populate `${CLAUDE_PLUGIN_ROOT}/templates/standalone-audit-deck.html` (repo fallback `./plugins/05-agency-growth/templates/standalone-audit-deck.html`) from `brand/teardown-report.json` (keep `data-attribution-element="1"` on header/footer attribution badges only, never on `<body>`; pass `--no-attribution` on white-label exports):
     - Slide 1: Positioning & Brand Token Snapshot (with verified WCAG 2.2 contrast ratios)
     - Slide 2: All 7 Channel Heuristic Rubric Scores & Funnel Gaps (preserving all 7 channel cards in both HTML and `.pptx`)
     - Slide 3: Content, Social Proof & Search Visibility Matrix
     - Slide 4: 30-Day Quick-Win Content Sprint Plan
     - Slide 5: Next Steps & Pilot Scope
   - Export PDF and PowerPoint copies via `gk export-pdf [--no-attribution]` and `gk export-pptx`.
2. **1 Static Benchmark Infographic (`standalone-infographic.html` + `.png`):**
   - Populate `${CLAUDE_PLUGIN_ROOT}/templates/standalone-infographic.html` comparing current 7-channel rubric scores against 30-day targets, and export PNG via `gk export-png`.
3. **2 Sample Social Posts (`draft-pack.json`):**
   - Write 1 LinkedIn teardown post and 1 second-channel post grounded in real findings from `teardown-report.json` (zero invented case-study metrics), verified with `gk lint --file <post-path> --platform linkedin`.

## Step 3: Package Local Review Bundle

```bash
./plugins/getknown-core/bin/gk publish-review-link --client <prospect-slug> --campaign pitch-audit --provider local [--no-attribution]
```
