---
name: brainstorm-angle
description: Use before drafting any campaign, landing page, deck, or video to run a 1-question-at-a-time interview that locks topic, channels, goal, and sources into a campaign brief.
argument-hint: "[<idea-or-offer>] [--client <slug>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Glob, Edit, Write
---

# Campaign & Offer Angle Brainstorming (`/brainstorm-angle`)

Run a focused positioning interview before drafting copy, slides, or video scripts so your campaign starts with a concrete claim and verified facts.

## Hard Rules

1. **Lock the angle before writing deliverables.** Jumping straight from a broad topic ("write a post about our product") to finished copy produces generic output.
2. **Ask ONE question per turn.** Offer 3 specific options (recommended option first with 1 sentence on why) and wait for the answer.
3. **Read the client's existing files & installed pack plugins first.** Inspect `./plugins/` and load `clients/<slug>/CLAUDE.md`, `clients/<slug>/tov/tov.md`, and `clients/<slug>/brand/tokens.json` before Question 1 (if no real client folder exists yet, ask for the brand name and initialize it via `./plugins/getknown-core/bin/gk client init <slug>`).

## The 4 Positioning Questions (One Per Turn)

### Question 1: Current Manual Workaround & Cost
- Identify what manual workaround the buyer uses today before buying this offer (for example: pasting brand hexes into chat tabs 20 times a week, waiting days on slide formatting, or rebuilding pitch decks by hand) and what it costs in hours or missed deals.
- Propose 3 concrete workarounds grounded in `clients/<slug>/CLAUDE.md`.

### Question 2: Specific Counter-Claim
- Identify why standard industry advice fails here, and state one specific claim backed by a number, named process, or before/after comparison.

### Question 3: Verifiable Proof & Sources
- Pick what the reader or viewer sees in the first 5 seconds:
  - A teardown metric from `sources/` or `brand/teardown-report.json`
  - A live screenshot (`gk harvest-proof`) or before/after comparison card
  - A named customer outcome with real numbers
- Mark any unconfirmed figure `[NEEDS_SOURCE]` rather than guessing.

### Question 4: Channel & Format Routing (Filtered by Installed `./plugins/`)
- Inspect `./plugins/` and offer **only** execution paths whose plugin folder is installed in this pack:
  - **Decks, Banners or Launch Page (`02-design-decks-pages`):** `/run-deck-or-page` + `/emil-design-polish` (precision UI & motion polish)
  - **Daily Social & Channel Sprint *(only when `01-social-tov` is in `./plugins/`)*:** `/run-daily-social`
  - **Prospect Audit & Pitch Kit *(only when `05-agency-growth` is in `./plugins/`)*:** `/run-competitor-audit`
  - **Animated Data Infographic *(only when `03-animated-infographics` is in `./plugins/`)*:** `/run-data-motion` (or code-built film via `/opuscar-director`)
  - **`9:16` Teardown Reel *(only when `04-shortform-video-engine` is in `./plugins/`)*:** `/run-short-video`

## Output: Save `campaign-brief.json`

Once confirmed, write `clients/<slug>/campaigns/<campaign-id>/campaign-brief.json` matching every required field of `${GETKNOWN_CORE_ROOT:-./plugins/getknown-core}/schemas/campaign-brief.schema.json` (or `./schemas/campaign-brief.schema.json`):
- `campaignId` (`^[a-z0-9-]+$`)
- `clientSlug` (`^[a-z0-9-]+$`)
- `schemaVersion`: `"1.3.0"`
- `topic`: the locked campaign angle and hook claim (`>= 5` chars)
- `channels`: array of active schema channels (`linkedin`, `instagram`, `x`, `tiktok`, `youtube-shorts`, `deck`, `landing-page`)
- `goal`: measurable target outcome and audience action (`>= 5` chars)
- `sources`: array of `{ "title": "...", "url": "...", "untrustedExcerpt": "..." }` proof objects
