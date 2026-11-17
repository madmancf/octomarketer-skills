---
name: slide-deck
description: Use when building viewport-locked 16:9 HTML, PDF, and PPTX presentation decks or 4:5 carousels styled in extracted client brand tokens.
argument-hint: "<deck-outline> [--client <slug>]"
context: fork
background: false
agent: gk:gk-renderer
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Brand Slide Deck & LinkedIn Carousel Builder (`/slide-deck`)

Build presentation-ready **16:9 slide decks** (`1920x1080`) and **4:5 LinkedIn swipe carousels** (`1080x1350`) styled from `clients/<client>/brand/tokens.json`, then export native editable PowerPoint (`.pptx`) and print-grade `.pdf` deliverables via `gk export-pptx` and `gk export-pdf`.

## Step 1: Choose Format & Slide Spine

Select the target format:
1. **`4:5` LinkedIn / Instagram Carousel (`1080x1350`, 6 to 10 slides):**
   - **Slide 1 (Hook Cover):** Specific claim, eyebrow pill, and swipe cue in `colors.accent`.
   - **Slides 2-8 (Core Breakdown):** One idea per slide, max 35 words per slide, visual comparison or numbered step badge.
   - **Slide 9 (Recap Sheet):** Scannable checklist readers save.
   - **Slide 10 (CTA Card):** Clear next step and brand sign-off.
2. **`16:9` Keynote / Client Pitch Deck (`1920x1080`, 8 to 15 slides):**
   - Executive summary, problem teardown, before/after benchmark grid, 30-day roadmap, and offer scope.

## Step 2: Generate Self-Contained HTML Deck

Write the deck to `clients/<client>/campaigns/<sprint>/assets/slide-deck.html` with:
- CSS variables bound to `clients/<client>/brand/tokens.json` (`colors.*`, `typography.*`, `radius`) and verified WCAG contrast pairs from `brand/design.md`.
- Keyboard arrow navigation (`Left` / `Right` / `Space`), slide counter, and `@media print` page-break rules (`@page { size: ...; margin: 0; }`, `break-after: page`).

## Step 3: Export Editable `.pptx` & Crisp `.pdf` (`gk export-pptx` / `gk export-pdf`)

Run the deterministic export subcommands (fallback `./plugins/getknown-core/bin/gk`):

- **For `16:9` Keynote / Client Pitch Decks (`1920x1080`):**
```bash
gk export-pptx \
  --html clients/<client>/campaigns/<sprint>/assets/slide-deck.html \
  --format 16:9 \
  --out clients/<client>/campaigns/<sprint>/exports/slide-deck.pptx

gk export-pdf \
  --html clients/<client>/campaigns/<sprint>/assets/slide-deck.html \
  --out clients/<client>/campaigns/<sprint>/exports/slide-deck.pdf
```

- **For `4:5` LinkedIn / Instagram Carousels (`1080x1350`):**
```bash
gk export-pptx \
  --html clients/<client>/campaigns/<sprint>/assets/slide-deck.html \
  --format 4:5 \
  --out clients/<client>/campaigns/<sprint>/exports/carousel-4x5.pptx

gk export-pdf \
  --html clients/<client>/campaigns/<sprint>/assets/slide-deck.html \
  --out clients/<client>/campaigns/<sprint>/exports/carousel-4x5.pdf
```
