---
description: Use when building branded social banner packs, 16:9 HTML/PDF/PPTX slide decks, or lead-magnet and webinar landing pages.
argument-hint: "--mode <banners|deck|launch-page|pack> [--client <slug>] [--resume <runId>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp *), Read, Grep, Glob, Edit, Write, Agent
---

# `/run-deck-or-page` (`/gk-design:run-deck-or-page`) · Outcome Workflow (`02-design-decks-pages`)

## Flow Contract & Checkpoint Recovery
- **Owning Plugin:** `gk-design` (`02-design-decks-pages`), available directly as `/run-deck-or-page` (and `/gk-design:run-deck-or-page` in the `/` picker).
- **Recommended Models (Included in Claude Pro & Max):** **Claude Opus 5.5** (`opus`, default) for narrative outline; **Claude Sonnet 5.5** (`sonnet`, `high` effort) on `gk:gk-renderer` for HTML/PPTX/PDF/PNG generation.
- **Checkpoint State:** Ensure `clients/<slug>/` exists (`gk client init <slug>` if new), then run `gk flow start run-deck-or-page --client <slug>` (inspect or resume via `gk flow status --client <slug>`, fallback `./plugins/getknown-core/bin/gk`).
- **Primary Outputs:** `clients/<slug>/campaigns/<id>/assets/{slide-deck.html,launch-page.html,banners.html}` and `exports/{slide-deck.pptx,slide-deck.pdf,banners-*.png}`

## Ordered Execution Steps
1. **`extract-brief`:** Start `gk flow start run-deck-or-page --client <slug>` (if not already active), draft the narrative outline, slide-by-slide copy, or page wireframe inline (`high`), verify copy with `gk lint --file <file> --platform linkedin`, confirm the outline with the user, and advance `gk flow step extract-brief --client <slug>`.
2. **`apply-design-tokens`:** Advance `gk flow step apply-design-tokens --client <slug>` and load `clients/<slug>/brand/tokens.json` and `brand/design.md` for verified contrast pairs and brand typography.
3. **`render-html-artifact`:** Advance `gk flow step render-html-artifact --client <slug>`, fork the selected visual builder (`/brand-banners`, `/slide-deck`, or `/launch-page`) to `gk:gk-renderer` (`sonnet`), export deliverables via `gk export-pptx`, `gk export-pdf`, or `gk export-png`, and register each exported deliverable (`assetPath` and `deliverablePaths`) inside `clients/<slug>/campaigns/<id>/drafts/draft-pack.json` so `/board` renders rich review cards alongside auto-discovered files.
4. **`export-review-pack`:** Advance `gk flow step export-review-pack --client <slug>`, start the Studio server in background mode via `./plugins/getknown-core/bin/gk serve --daemon` to share the live `/board?client=<slug>` URL, package the local bundle via `gk publish-review-link --client <slug> --provider local`, and mark `gk flow complete run-deck-or-page --client <slug>`.
