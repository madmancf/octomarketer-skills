---
description: Use when brainstorming a campaign angle, directing a code-built Lemo-Opuscar or Remotion film, applying precision spring-physics UI and motion polish, or running a classic direct-response copywriting pass.
argument-hint: "[<goal-or-topic>] [--client <slug>] [--style <opuscar-style>] [--lens <copy-style>] [--resume <runId>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp *), Read, Grep, Glob, Edit, Write, Agent
---

# `/run-creative-director` (`/gk-director:run-creative-director`) · Outcome Workflow (`06-brainstorm-and-director`)

## Flow Contract & Checkpoint Recovery
- **Owning Plugin:** `gk-director` (`06-brainstorm-and-director`), available directly as `/run-creative-director` (and `/gk-director:run-creative-director` in the `/` picker).
- **Recommended Models (Included in Claude Pro & Max):** **Claude Opus 5.5** (`opus`, default) for creative direction, angle strategy, and multi-scene scripting; **Claude Sonnet 5.5** (`sonnet`, `high` effort) for fast daily variants, parallel subagent execution, and lighter use of your weekly subscription allowance.
- **Checkpoint State:** Ensure `clients/<slug>/` exists (`gk client init <slug>` if new), then run `gk flow start run-creative-director --client <slug>` (inspect or resume via `gk flow status --client <slug>`, fallback `./plugins/getknown-core/bin/gk`).
- **Primary Outputs:** `clients/<slug>/campaigns/<id>/campaign-brief.json` + finished deliverables in `clients/<slug>/campaigns/<id>/exports/`

## Ordered Execution Steps
1. **`brainstorm-angle`:** Start `gk flow start run-creative-director --client <slug>` (if not already active), run `/brainstorm-angle` inline (`high` effort) one question at a time to lock `topic`, `channels`, `goal`, and `sources` into `campaign-brief.json` (offering only execution tracks installed in `./plugins/`), and advance `gk flow step brainstorm-angle --client <slug>`.
2. **`execute-creative-track`:** Advance `gk flow step execute-creative-track --client <slug>` and execute the selected creative track:
   - **Copy & Campaign Messaging:** Run `/copy-legend` with the chosen craft lens (`classic-print`, `sales-letter`, `customer-voice`, `behavioral-reframe`, `scientific-proof`, `distinctive-reach`, `social-proof`, `focused-audience`, `guided-story`, or `shareable-benchmark`).
   - **Web Pages, Slide Decks & Interactive UI:** Run `/emil-design-polish` for precision spring-physics UI and motion polish (custom `cubic-bezier` curves, `scale(0.95)` entrances, `:active` press feedback, and a `| Before | After | Why |` review table).
   - **Code-Driven Film & Motion Graphics:** Fork `/opuscar-director` (`gk:gk-renderer`) or invoke `/lemo-opuscar` to direct across **`lemomo-ai/lemo-opuscar`** (`59` modular library styles `#12..#70` + `98` film anthology showcase specs, such as `#24` `dark-keynote`, `#35` `iso-infographic`, `#60` `swiss-motion`, `#62` `telestrator`, `#19` `caption-news`, `#18` `briefing-board`, `#61` `teardown`, with custom client styles saved in `clients/<slug>/brand/styles/`), **Remotion**, or **`gk render-video`**.
   - **Multi-Channel or Multi-Prospect Batch:** Run `/parallel-sprint` to dispatch isolated `gk:gk-researcher` and `gk:gk-renderer` subagents via `Agent`.
3. **`evaluate-anti-slop`:** Advance `gk flow step evaluate-anti-slop --client <slug>` and verify all copy and script deliverables with `gk lint --file <draft-path> --platform linkedin`.
4. **`generate-review-board`:** Advance `gk flow step generate-review-board --client <slug>`, start the Studio server in background mode via `./plugins/getknown-core/bin/gk serve --daemon` to share the `/board?client=<slug>` URL, and mark `gk flow complete run-creative-director --client <slug>`.
