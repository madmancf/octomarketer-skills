---
name: build-infographic
description: Use when rendering a 1080x1350 LinkedIn infographic (#01 comparison-grid, #02 step-by-step-flow, #03 iceberg-breakdown) as crisp PNG/PDF and 30fps animated MP4 in brand tokens.
argument-hint: "<data-brief> [--client <slug>] [--template #01|#02|#03|comparison-grid|step-by-step-flow|iceberg-breakdown]"
context: fork
background: false
agent: gk:gk-renderer
effort: medium
allowed-tools: Bash(gk *), Bash(~/.local/bin/gk *), Bash(./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Animated Infographic Builder (`/build-infographic`)

Structure marketing data into scannable `1080x1350` (`4:5`) visual nodes styled with `./brand/tokens.json` (or `clients/<client>/brand/tokens.json`), then export both crisp static PNG/PDF cards (`gk export-png`, `gk export-pdf`) and a `30fps` animated MP4 (`gk render-video`).

## Shared Template Studio Catalog (`#01..#03` in `template-registry.json`)

| Template `#` | Canonical Slug | Template Path | Best For |
| :--- | :--- | :--- | :--- |
| **`#01`** | `comparison-grid` | `${CLAUDE_PLUGIN_ROOT}/templates/comparison-grid/index.html` | Side-by-side comparison matrix with animated status pills and metric bars (`240` frames / `8.0s` @ `30fps`). |
| **`#02`** | `step-by-step-flow` | `${CLAUDE_PLUGIN_ROOT}/templates/step-by-step-flow/index.html` | 4 to 6 step numbered pipeline with timing and command badges (`240` frames / `8.0s` @ `30fps`). |
| **`#03`** | `iceberg-breakdown` | `${CLAUDE_PLUGIN_ROOT}/templates/iceberg-breakdown/index.html` | "Visible Deliverable Above the Waterline vs. System Below" layered breakdown (`240` frames / `8.0s` @ `30fps`). |

*(Catalog source of truth: `plugins/getknown-core/templates/template-registry.json`.)*

## Bidirectional Template Handshake (`#01..#03`)

- **If the user already named a `#NN` number (`#01`, `#02`, `#03`) or `<slug>` (`comparison-grid`, `step-by-step-flow`, `iceberg-breakdown`) in chat or `$ARGUMENTS`:** Resolve that template immediately and proceed straight to Step 1 without asking again.
- **If the user did NOT pick a template yet:** Start the local Studio server in background mode via `gk serve --daemon` (fallback `~/.local/bin/gk serve --daemon` or `./plugins/getknown-core/bin/gk serve --daemon`), show the clickable visual gallery link `http://127.0.0.1:<port>/templates?pack=gk-motion` (default `http://127.0.0.1:4318/templates?pack=gk-motion`), list `#01 comparison-grid`, `#02 step-by-step-flow`, and `#03 iceberg-breakdown` in one short summary, and ask which `#NN` or `<slug>` they want before rendering.

## Step-by-Step Workflow

1. **Gather & Condense Verified Facts:**
   - Pull verified numbers from `campaign-brief.json` or the user's brief (never invent fake benchmarks).
   - Keep text tight (`<= 60` chars per heading, `<= 120` chars per card body) so mobile feeds stay sharp.
2. **Populate the Chosen Template with Brand Tokens:**
   - Copy `${CLAUDE_PLUGIN_ROOT}/templates/<archetype>/index.html` (repo fallback `./plugins/03-animated-infographics/templates/<archetype>/index.html`) into `campaigns/<sprint>/assets/infographic-<slug>.html` (or `clients/<client>/campaigns/<sprint>/assets/infographic-<slug>.html`).
   - Bind `brand/tokens.json` (`colors.*`, `typography.*`, `radius`) and escape any embedded JSON `</script>` tags.
3. **Export Crisp PNG + `30fps` MP4 (`gk export-png` & `gk render-video`):**
   - Always pass explicit `4:5` stage dimensions and `8s` / `240`-frame duration (`fallback: ~/.local/bin/gk` or `./plugins/getknown-core/bin/gk`):
     ```bash
     gk export-png \
       --html clients/<client>/campaigns/<sprint>/assets/infographic-<slug>.html \
       --out clients/<client>/campaigns/<sprint>/exports/infographic-<slug>.png \
       --width 1080 \
       --height 1350

     gk render-video \
       --html clients/<client>/campaigns/<sprint>/assets/infographic-<slug>.html \
       --out clients/<client>/campaigns/<sprint>/exports/infographic-<slug>.mp4 \
       --width 1080 \
       --height 1350 \
       --duration 8 \
       --frames 240 \
       --fps 30 \
       --allow-silent
     ```
