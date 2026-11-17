---
description: Use when running a 5-minute 7-channel competitor or prospect teardown and generating a prospect-branded audit deck, 2 sample posts, and 1 benchmark infographic.
argument-hint: "<prospect-url> [--client <slug>] [--crawl-depth 1|2|3] [--no-attribution] [--resume <runId>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(command -v *), Bash(mkdir *), Bash(cp *), Read, Grep, Glob, Edit, Write, Agent
---

# `/run-competitor-audit` (`/gk-agency:run-competitor-audit`) · Outcome Workflow (`05-agency-growth`)

## Flow Contract & Checkpoint Recovery
- **Owning Plugin:** `gk-agency` (`05-agency-growth`), available directly as `/run-competitor-audit` (and `/gk-agency:run-competitor-audit` in the `/` picker).
- **Recommended Models (Included in Claude Pro & Max):** **Claude Opus 5.5** (`opus`, default) for teardown synthesis; **Claude Sonnet 5.5** (`sonnet`, `high` effort) for `gk:gk-researcher` SPA crawling and `gk:gk-renderer` deck/infographic output.
- **Checkpoint State:** Initialize `clients/<slug>/` first (`gk client init <slug> --url <prospect-url>`), then run `gk flow start run-competitor-audit --client <slug>` (inspect or resume via `gk flow status --client <slug>`, fallback `./plugins/getknown-core/bin/gk`).
- **Primary Outputs:** `clients/<slug>/brand/teardown-report.json`, `clients/<slug>/campaigns/<id>/exports/{standalone-audit-deck.html,standalone-audit-deck.pdf,standalone-audit-deck.pptx,pitch-audit-review-pack.zip}`

## Ordered Execution Steps
1. **`scrape-competitors`:** Initialize `clients/<slug>/` via `./plugins/getknown-core/bin/gk client init <slug> --url <prospect-url>`, start `gk flow start run-competitor-audit --client <slug>`, fork `gk brand-extract --client <slug> --url <prospect-url>` and `gk teardown --client <slug> --url <prospect-url> --crawl-depth 2` (passing `--no-attribution` when white-labeling for an agency pitch) in parallel to `gk:gk-researcher` (`sonnet`), and advance `gk flow step scrape-competitors --client <slug>`.
2. **`analyze-gaps`:** Advance `gk flow step analyze-gaps --client <slug>` and synthesize the 7-channel heuristic teardown findings (`scoringMethod: "heuristic-html-rubric"`) plus 2 rewritten sample posts inline (`high`), verified by `gk lint --file <post-file> --platform linkedin`.
3. **`generate-audit-deck`:** Advance `gk flow step generate-audit-deck --client <slug>`, fork `standalone-audit-deck.html` (`gk export-pdf` + `gk export-pptx`, forwarding `--no-attribution` if requested) and `standalone-infographic.html` (`gk export-png`) rendering to `gk:gk-renderer` (`sonnet`), and register exported deliverables (`assetPath` and `deliverablePaths`) alongside the sample posts in `clients/<slug>/campaigns/<id>/drafts/draft-pack.json` so `/board` displays rich metadata.
4. **`render-agency-report`:** Advance `gk flow step render-agency-report --client <slug>`, launch `./plugins/getknown-core/bin/gk serve --daemon` to share the `/board?client=<slug>` URL, package the local bundle via `gk publish-review-link --client <slug> --provider local` (forwarding `--no-attribution` if requested), and mark `gk flow complete run-competitor-audit --client <slug>`.
