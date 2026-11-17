---
name: brand-banners
description: Use when generating branded social media banners (#06 social-banner-sheet: 1200x628, 1080x1350, 1080x1080, 1080x1920) in HTML/SVG and exporting high-DPI PNGs.
argument-hint: "<campaign-brief> [--template #06|social-banner-sheet] [--client <slug>]"
context: fork
background: false
agent: gk:gk-renderer
effort: medium
allowed-tools: Bash(gk *), Bash(~/.local/bin/gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Brand Banner & Social Card Generator (`/brand-banners`)

Create promotional banners, event headers, LinkedIn link cards, and video cover frames in one pass using `./brand/tokens.json` (or `clients/<client>/brand/tokens.json`) and `brand/design.md`, then render crisp `2x` DPI PNG files via `gk export-png`.

## Shared Template Studio Catalog (`#06` in `template-registry.json`)

- **`#06` `social-banner-sheet`** (`pack: "gk-design"`, catalog: `plugins/getknown-core/templates/template-registry.json`): 4-aspect-ratio high-DPI social banner sheet (`1200x628`, `1080x1350`, `1080x1080`, `1080x1920`).

## Bidirectional Template Handshake (`#06`)

- **If the user already named `#06` / `social-banner-sheet` or gave their concrete banner brief/sizes in chat:** Execute immediately without extra prompting.
- **If the user has not chosen a design format yet (or wants to compare `#04..#07` visual layouts first):** Start `gk serve --daemon` (fallback `~/.local/bin/gk` or `./plugins/getknown-core/bin/gk`), share `http://127.0.0.1:<port>/templates?pack=gk-design` (default `http://127.0.0.1:4318/templates?pack=gk-design`), and ask which `#NN` or `<slug>` (such as `#06 social-banner-sheet`) they want.

## Step 1: Load Brand Tokens

Read `brand/tokens.json` and `brand/design.md` (inside `./brand/` or `clients/<client>/brand/`):
- Bind `colors.primary`, `colors.accent`, `colors.secondary`, `colors.brandBlack`, `colors.surfaceDark`, `colors.backgroundLight`, `typography.headingFont`, `typography.bodyFont`, and `radius`.
- Use local bundled `Plus Jakarta Sans` `.woff2` (or extracted client fonts) and verified WCAG 2.2 AA foreground/background pairs from `brand/design.md` so pill badges and headlines stay readable on both dark and light surfaces.

## Step 2: Build Multi-Aspect Banner Sheet (`4` Sizes)

Write a self-contained HTML banner sheet at `clients/<client>/campaigns/<sprint>/assets/banners.html` (or `./campaigns/<sprint>/assets/banners.html`) containing all 4 artboards:
1. **LinkedIn / X Landscape (`1200x628` / `16:9`)**
2. **Instagram / LinkedIn Portrait Card (`1080x1350` / `4:5`)**
3. **Square Feed Post (`1080x1080` / `1:1`)**
4. **Story / Reel Cover (`1080x1920` / `9:16`)**

## Step 3: Export Crisp PNG Deliverables

- Include a 2 to 4 word `UPPERCASE` eyebrow pill in `colors.accent`, a headline (`<= 8` words), and one clear focal element per banner.
- If the user requests an AI-generated hero image via configured BYOK keys (`GOOGLE_API_KEY`, `OPENROUTER_API_KEY`, or `FAL_KEY`), run `gk cost-check --client <client> --estimated-usd 0.05 --dry-run` (and `--reserve` once confirmed) first.
- Export high-DPI `.png` deliverables via `gk export-png` (works with bundled headless Chromium even without `node_modules`):
  ```bash
  gk export-png --html clients/<client>/campaigns/<sprint>/assets/banners.html --out clients/<client>/campaigns/<sprint>/exports/banner-1080x1350.png --width 1080 --height 1350
  gk export-png --html clients/<client>/campaigns/<sprint>/assets/banners.html --out clients/<client>/campaigns/<sprint>/exports/banner-1080x1080.png --width 1080 --height 1080
  ```
