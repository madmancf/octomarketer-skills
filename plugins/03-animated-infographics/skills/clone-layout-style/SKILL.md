---
name: clone-layout-style
description: Use when reverse-engineering a reference infographic grid, spacing rhythm, and motion curve without copying creator IP.
argument-hint: "<image-or-url> [--client <slug>]"
context: fork
background: false
agent: gk:gk-researcher
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Read, Edit, Write, WebFetch
---

# Creator Infographic Layout Cloner (`/clone-layout-style`)

Extract the grid skeleton, information density, and visual pacing of a high-performing reference infographic and map it onto `clients/<client>/brand/tokens.json`.

## Step 1: Inspect the Reference Infographic

Accept 1 to 3 reference images, screenshots, or post URLs from the user and record five structural mechanics:
1. **Canvas & Grid Topology:** Aspect ratio (`4:5` `1080x1350` or `1:1` `1080x1080`), header height ratio, column count, and card gap spacing.
2. **Information Hierarchy:** Word cap per node, badge numbering style (`01`, `02`, `03`), and icon-to-text ratio.
3. **Visual Connectors:** How the eye moves across the canvas (step arrows, comparison split line, concentric layers, or iceberg waterline).
4. **Contrast Polarity:** Where high-saturation accents draw the eye first, mapped to `colors.accent` and `colors.primary` from `clients/<client>/brand/tokens.json`.
5. **Motion Choreography:** How blocks animate in over an `8.0s` (`240`-frame @ `30fps`) loop (staggered card reveal, connector line draw, counter tick-up).

## Step 2: Save the Reusable Layout Recipe

Write the layout recipe to `clients/<client>/brand/infographic-recipes/<recipe-slug>.json` (or map it to `comparison-grid`, `step-by-step-flow`, or `iceberg-breakdown` under `${CLAUDE_PLUGIN_ROOT}/templates/`).

**Guardrail:** Never copy another creator's text, proprietary illustrations, logos, or color hexes. Re-skin all typography (`typography.headingFont`, `typography.bodyFont`), colors (`colors.*`), and card radii (`radius`) from `clients/<client>/brand/tokens.json`.
