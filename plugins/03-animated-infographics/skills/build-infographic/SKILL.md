---
name: build-infographic
description: Use when rendering a 1080x1350 LinkedIn infographic as crisp PNG/PDF and 30fps animated MP4 in client brand tokens.
argument-hint: "<data-brief> [--client <slug>] [--template comparison-grid|step-by-step-flow|iceberg-breakdown]"
context: fork
background: false
agent: gk:gk-renderer
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Animated Infographic Builder (`/build-infographic`)

Structure marketing data into scannable `1080x1350` (`4:5`) visual nodes styled with `clients/<client>/brand/tokens.json`, then export both crisp static PNG/PDF cards (`gk export-png`, `gk export-pdf`) and a `30fps` animated MP4 (`gk render-video`).

## Available Built-In Infographic Templates (`${CLAUDE_PLUGIN_ROOT}/templates/`)

1. **`comparison-grid` (`${CLAUDE_PLUGIN_ROOT}/templates/comparison-grid/index.html`):**
   - Side-by-side comparison matrix with animated status pills and metric bars (`240` frames / `8.0s` @ `30fps`).
2. **`step-by-step-flow` (`${CLAUDE_PLUGIN_ROOT}/templates/step-by-step-flow/index.html`):**
   - 4 to 6 step numbered pipeline with timing and command badges (`240` frames / `8.0s` @ `30fps`).
3. **`iceberg-breakdown` (`${CLAUDE_PLUGIN_ROOT}/templates/iceberg-breakdown/index.html`):**
   - "Visible Deliverable Above the Waterline vs. System Below" layered breakdown (`240` frames / `8.0s` @ `30fps`).

## Step-by-Step Workflow

1. **Gather & Condense Verified Facts:**
   - Pull verified numbers from `campaign-brief.json` or the user's brief (never invent fake benchmarks).
   - Keep text tight (`<= 60` chars per heading, `<= 120` chars per card body) so mobile feeds stay sharp.
2. **Populate the Chosen Template with Brand Tokens:**
   - Copy `${CLAUDE_PLUGIN_ROOT}/templates/<archetype>/index.html` (repo fallback `./plugins/03-animated-infographics/templates/<archetype>/index.html`) into `clients/<client>/campaigns/<sprint>/assets/infographic-<slug>.html`.
   - Bind `clients/<client>/brand/tokens.json` (`colors.*`, `typography.*`, `radius`) and escape any embedded JSON `</script>` tags.
3. **Export Crisp PNG + `30fps` MP4 (`gk export-png` & `gk render-video`):**
   - Always pass explicit `4:5` stage dimensions and `8s` / `240`-frame duration (`fallback: ./plugins/getknown-core/bin/gk`):
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
