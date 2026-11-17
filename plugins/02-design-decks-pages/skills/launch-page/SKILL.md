---
name: launch-page
description: Use when building a conversion-focused lead-magnet, webinar, or course landing page (#07 conversion-launch-page) exported as a self-contained HTML bundle.
argument-hint: "<offer-brief> [--template #07|conversion-launch-page] [--client <slug>]"
context: fork
background: false
agent: gk:gk-renderer
effort: high
allowed-tools: Bash(gk *), Bash(~/.local/bin/gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Campaign Launch Page Builder (`/launch-page`)

Build responsive, self-contained HTML campaign landing pages, workshop pages, or agency case-study pages (`#07`) styled from `./brand/tokens.json` (or `clients/<client>/brand/tokens.json`).

## Shared Template Studio Catalog (`#07` in `template-registry.json`)

- **`#07` `conversion-launch-page`** (`pack: "gk-design"`, catalog: `plugins/getknown-core/templates/template-registry.json`): Responsive 6-section conversion landing page (`390x844` mobile & `1440x900` desktop).

## Bidirectional Template Handshake (`#07`)

- **If the user already named `#07` / `conversion-launch-page` or supplied their concrete offer brief in chat:** Execute immediately without redundant prompting.
- **If the user has not picked a template yet (or wants to inspect `gk-design` templates `#04..#07` first):** Start `gk serve --daemon` (fallback `~/.local/bin/gk` or `./plugins/getknown-core/bin/gk`), share `http://127.0.0.1:<port>/templates?pack=gk-design` (default `http://127.0.0.1:4318/templates?pack=gk-design`), and ask which `#NN` or `<slug>` (such as `#07 conversion-launch-page`) they want.

## Step 1: Load Brand Tokens, Voice & Offer

Read (from `./` or `clients/<client>/`):
- `brand/tokens.json` & `brand/design.md`
- `tov/tov.md`
- `CLAUDE.md`

## Step 2: Assemble the 6-Section Conversion Spine

Write `clients/<client>/campaigns/<sprint>/assets/launch-page.html` (or `./campaigns/<sprint>/assets/launch-page.html`) with `0px` horizontal overflow at both `390x844` mobile and `1440x900` desktop:
1. **Above-the-Fold Hero:** Eyebrow pill badge (`colors.accent`), concrete outcome headline (`typography.headingFont`), 2-sentence subhead, primary CTA button, and preview card.
2. **Problem Breakdown:** 3-card comparison grid showing what the manual workflow costs in hours or missed deals.
3. **Deliverables & Scope:** Numbered breakdown of exact deliverables, timeline, and format.
4. **Proof & Credentials:** Verified credentials, real customer outcomes, and concrete artifacts (zero invented statistics).
5. **Who This Fits:** Direct qualification checklist.
6. **FAQ & Final CTA Block:** Clear answers to top buyer questions and primary checkout or booking CTA.

## Step 3: Readability, Export & Live Preview

- Lint visible page copy with `gk lint --file clients/<client>/campaigns/<sprint>/assets/launch-page.html --platform linkedin` (`gk lint` strips `<style>`, `<script>`, and HTML markup automatically before checking prose readability and filler words).
- Optionally export a full-page shareable PDF or PNG preview via `gk export-pdf` or `gk export-png`, and preview live on `/board` via `gk serve --daemon`.
