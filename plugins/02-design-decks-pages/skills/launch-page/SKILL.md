---
name: launch-page
description: Use when building a conversion-focused lead-magnet, webinar, or course landing page exported as a self-contained HTML bundle.
argument-hint: "<offer-brief> [--client <slug>]"
context: fork
background: false
agent: gk:gk-renderer
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Campaign Launch Page Builder (`/launch-page`)

Build responsive, self-contained HTML campaign landing pages, workshop pages, or agency case-study pages styled from `clients/<client>/brand/tokens.json`.

## Step 1: Load Brand Tokens, Voice & Offer

Read:
- `clients/<client>/brand/tokens.json` & `brand/design.md`
- `clients/<client>/tov/tov.md`
- `clients/<client>/CLAUDE.md`

## Step 2: Assemble the 6-Section Conversion Spine

Write `clients/<client>/campaigns/<sprint>/assets/launch-page.html` with `0px` horizontal overflow at both `390x844` mobile and `1440x900` desktop:
1. **Above-the-Fold Hero:** Eyebrow pill badge (`colors.accent`), concrete outcome headline (`typography.headingFont`), 2-sentence subhead, primary CTA button, and preview card.
2. **Problem Breakdown:** 3-card comparison grid showing what the manual workflow costs in hours or missed deals.
3. **Deliverables & Scope:** Numbered breakdown of exact deliverables, timeline, and format.
4. **Proof & Credentials:** Verified credentials, real customer outcomes, and concrete artifacts (zero invented statistics).
5. **Who This Fits:** Direct qualification checklist.
6. **FAQ & Final CTA Block:** Clear answers to top buyer questions and primary checkout or booking CTA.

## Step 3: Readability, Export & Live Preview

- Lint visible page copy with `./plugins/getknown-core/bin/gk lint --file clients/<client>/campaigns/<sprint>/assets/launch-page.html --platform linkedin` (`gk lint` strips `<style>`, `<script>`, and HTML markup automatically before checking prose readability and filler words).
- Optionally export a full-page shareable PDF or PNG preview via `gk export-pdf` or `gk export-png`, and preview live on the Approval Board via `./plugins/getknown-core/bin/gk serve --daemon`.
