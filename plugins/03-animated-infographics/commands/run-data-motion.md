---
description: Use when creating LinkedIn creator infographics or 30fps animated data visuals in 1080x1350 4:5 format.
argument-hint: "[<topic-or-reference-url>] [--client <slug>] [--template comparison-grid|step-by-step-flow|iceberg-breakdown] [--resume <runId>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp *), Read, Grep, Glob, Edit, Write, Agent
---

# `/run-data-motion` (`/gk-motion:run-data-motion`) · Outcome Workflow (`03-animated-infographics`)

## Flow Contract & Checkpoint Recovery
- **Owning Plugin:** `gk-motion` (`03-animated-infographics`), available directly as `/run-data-motion` (and `/gk-motion:run-data-motion` in the `/` picker).
- **Recommended Models (Included in Claude Pro & Max):** **Claude Opus 5.5** (`opus`, default) for data hierarchy; **Claude Sonnet 5.5** (`sonnet`, `high` effort) on `gk:gk-renderer`.
- **Checkpoint State:** Ensure `clients/<slug>/` exists (`gk client init <slug>` if new), then run `gk flow start run-data-motion --client <slug>` (inspect or resume via `gk flow status --client <slug>`, fallback `./plugins/getknown-core/bin/gk`).
- **Primary Outputs:** `clients/<slug>/campaigns/<id>/exports/{infographic.png,infographic.pdf,infographic.mp4}`

## Ordered Execution Steps
1. **`validate-metrics`:** Start `gk flow start run-data-motion --client <slug>` (if not already active), optionally fork `/clone-layout-style` (`gk:gk-researcher`, `sonnet`) to extract structural grid proportions from a reference visual, lock verified data claims and node copy inline, and advance `gk flow step validate-metrics --client <slug>`.
2. **`generate-motion-scene`:** Advance `gk flow step generate-motion-scene --client <slug>` and fork `/build-infographic` (`gk:gk-renderer`, `sonnet`) to populate the `1080x1350` (`4:5`) HTML stage with `clients/<slug>/brand/tokens.json`.
3. **`render-preview-loop`:** Advance `gk flow step render-preview-loop --client <slug>` and render the `8s` (`240`-frame @ `30fps`) MP4 via `gk render-video --html <composition.html> --out <infographic.mp4> --width 1080 --height 1350 --duration 8 --frames 240 --fps 30 --allow-silent`.
4. **`export-motion-assets`:** Advance `gk flow step export-motion-assets --client <slug>`, export crisp `1080x1350` PNG and PDF deliverables via `gk export-png` and `gk export-pdf`, register exported deliverables (`assetPath` and `deliverablePaths`) in `clients/<slug>/campaigns/<id>/drafts/draft-pack.json` for rich Approval Board metadata, start the Studio server via `./plugins/getknown-core/bin/gk serve --daemon` to share the `/board?client=<slug>` URL, and mark `gk flow complete run-data-motion --client <slug>`.
