---
name: slide-deck
description: Use when building viewport-locked 16:9 HTML/PDF/PPTX presentation decks (#04 exec-deck-16x9) or 4:5 carousels (#05 social-carousel-4x5) styled in extracted brand tokens.
argument-hint: "<deck-outline> [--template #04|#05|exec-deck-16x9|social-carousel-4x5] [--client <slug>]"
context: fork
background: false
agent: gk:gk-renderer
effort: high
allowed-tools: Bash(gk *), Bash(~/.local/bin/gk *), Bash(./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Brand Slide Deck & LinkedIn Carousel Builder (`/slide-deck`)

Build presentation-ready **16:9 slide decks** (`1920x1080`, `#04`) and **4:5 LinkedIn swipe carousels** (`1080x1350`, `#05`) styled from `./brand/tokens.json` (or `clients/<client>/brand/tokens.json`), then export native editable PowerPoint (`.pptx`) and print-grade `.pdf` deliverables via `gk export-pptx` and `gk export-pdf`.

## Shared Template Studio Catalog (`#04..#05` in `template-registry.json`)

| Template `#` | Canonical Slug | Format | Best For |
| :--- | :--- | :--- | :--- |
| **`#04`** | `exec-deck-16x9` | `16:9` (`1920x1080`, 8 to 15 slides) | Keynote / Executive & Client Pitch Deck (summary, problem teardown, benchmark grid, 30-day roadmap, offer scope). |
| **`#05`** | `social-carousel-4x5` | `4:5` (`1080x1350`, 6 to 10 slides) | LinkedIn / Instagram Swipe Carousel (hook cover, 1-idea breakdown cards, saveable recap sheet, CTA card). |

*(Catalog source of truth: `plugins/getknown-core/templates/template-registry.json`.)*

## Bidirectional Template Handshake (`#04..#05`)

- **If the user already named `#04` / `exec-deck-16x9` (or `16:9` pitch deck) or `#05` / `social-carousel-4x5` (or `4:5` carousel) in chat or `$ARGUMENTS`:** Execute immediately without redundant prompting.
- **If the user did NOT pick a template yet:** Start the local Studio server via `gk serve --daemon` (fallback `~/.local/bin/gk` or `./plugins/getknown-core/bin/gk`), share `http://127.0.0.1:<port>/templates?pack=gk-design` (default `http://127.0.0.1:4318/templates?pack=gk-design`), and ask whether they want **`#04` `exec-deck-16x9`** or **`#05` `social-carousel-4x5`**.

## Step 1: Structure the Chosen Spine

1. **`#05` `social-carousel-4x5` (`1080x1350`, 6 to 10 slides):**
   - **Slide 1 (Hook Cover):** Specific claim, eyebrow pill, and swipe cue in `colors.accent`.
   - **Slides 2-8 (Core Breakdown):** One idea per slide, max 35 words per slide, visual comparison or numbered step badge.
   - **Slide 9 (Recap Sheet):** Scannable checklist readers save.
   - **Slide 10 (CTA Card):** Clear next step and brand sign-off.
2. **`#04` `exec-deck-16x9` (`1920x1080`, 8 to 15 slides):**
   - Executive summary, problem teardown, before/after benchmark grid, 30-day roadmap, and offer scope.

## Step 2: Generate Self-Contained HTML Deck

Write the deck to `clients/<client>/campaigns/<sprint>/assets/slide-deck.html` (or `./campaigns/<sprint>/assets/slide-deck.html`) with:
- CSS variables bound to `brand/tokens.json` (`colors.*`, `typography.*`, `radius`) and verified WCAG contrast pairs from `brand/design.md`.
- Keyboard arrow navigation (`Left` / `Right` / `Space`), slide counter, and `@media print` page-break rules (`@page { size: ...; margin: 0; }`, `break-after: page`).

## Step 3: Export Editable `.pptx` & Crisp `.pdf` (`gk export-pptx` / `gk export-pdf`)

Run the deterministic export subcommands (fallback `~/.local/bin/gk` or `./plugins/getknown-core/bin/gk`):

- **For `#04` `exec-deck-16x9` (`1920x1080`):**
```bash
gk export-pptx \
  --html clients/<client>/campaigns/<sprint>/assets/slide-deck.html \
  --format 16:9 \
  --out clients/<client>/campaigns/<sprint>/exports/slide-deck.pptx

gk export-pdf \
  --html clients/<client>/campaigns/<sprint>/assets/slide-deck.html \
  --out clients/<client>/campaigns/<sprint>/exports/slide-deck.pdf
```

- **For `#05` `social-carousel-4x5` (`1080x1350`):**
```bash
gk export-pptx \
  --html clients/<client>/campaigns/<sprint>/assets/slide-deck.html \
  --format 4:5 \
  --out clients/<client>/campaigns/<sprint>/exports/carousel-4x5.pptx

gk export-pdf \
  --html clients/<client>/campaigns/<sprint>/assets/slide-deck.html \
  --out clients/<client>/campaigns/<sprint>/exports/carousel-4x5.pdf
```
