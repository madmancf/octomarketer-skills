---
name: topic-radar
description: Use when scanning industry news, RSS, Hacker News, Reddit, or optional connected research sources for high-signal content angles.
argument-hint: "[<topic>] [--client <slug>]"
context: fork
background: false
agent: gk:gk-researcher
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write, WebFetch, WebSearch
---

# Industry Topic Radar & Brief Builder (`/topic-radar`)

Gather concrete industry signals, competitor positioning shifts, and buyer questions across local and optional connected sources, then save `campaign-brief.json`.

## Step 1: Select Signal Sources (Free Local First)

Check configured services via `./plugins/getknown-core/bin/gk provider-health --client <client>` and gather signals in order:
1. **Free Local & Public Web Sources (`$0.00`):**
   - User-supplied links, newsletter excerpts, client call notes, or competitor URLs.
   - Public web search and RSS or news headlines in the client's market.
   - Local `yt-dlp` video transcripts when `yt-dlp` is installed on `$PATH`.
2. **Optional Connected Research Sources:**
   - Run `./plugins/getknown-core/bin/gk cost-check --client <client> --estimated-usd 0.10 --dry-run` (and `--reserve` once confirmed) before calling paid scraping services (`APIFY_API_TOKEN`, `EXA_API_KEY`, `PERPLEXITY_API_KEY`).

## Step 2: Score & Filter Candidate Topics

Score each raw finding against `clients/<client>/CLAUDE.md` and `tov/tov.md`:
- **Specificity Check:** Does it name a real company, number, workflow change, or concrete mistake? Reject vague "AI is changing marketing" angles.
- **Practitioner Angle:** What direct experience does our client bring to this topic?
- **Visual Potential:** Can this topic anchor a `comparison-grid` or `iceberg-breakdown` infographic (when `03-animated-infographics` is installed) or a swipe carousel (`/slide-deck`)?

## Step 3: Write Campaign Brief

Save the selected campaign brief to `clients/<client>/campaigns/<sprint>/campaign-brief.json` matching `${GETKNOWN_CORE_ROOT:-./plugins/getknown-core}/schemas/campaign-brief.schema.json` (or `./schemas/campaign-brief.schema.json`): `campaignId`, `clientSlug`, `schemaVersion` (`"1.3.0"`), `topic`, `channels`, `goal`, and `sources`.

Ask the user which topic angle to turn into channel drafts via `/draft-post`.
