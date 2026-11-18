# Octomarketer Skills & Plugin Reference (`Claude Code for Marketers`)

Public plugin, skill, workflow command, and subagent reference for the **Claude Code for Marketers** 2-Day Intensive. This repository contains **7 plugins**, **32 skills**, **7 workflow commands**, and **2 subagents** with internal CLI runtimes, client fixtures, and local media bundles stripped out.

## Model Configuration (`Claude Opus 5.5` + `Claude Sonnet 5.5`)

| Role | Model | ID / Alias | When to Use |
|---|---|---|---|
| **Strategy, Voice & Creative Direction** | **Claude Opus 5.5** | `claude-opus-5-5` (`opus`) | Brand positioning, Tone-of-Voice synthesis (`/tov-extract`), `CLAUDE.md` design, 16:9 slide decks, launch pages, and campaign direction. |
| **Diagnostics, Batches & Subagents** | **Claude Sonnet 5.5** (`high` effort) | `claude-sonnet-5-5` (`sonnet`) | Machine readiness checks, daily social post batches, website extraction (`gk-researcher`), and HTML/video composition (`gk-renderer`). |

## Project Skill Loading: Always-Active Packs vs. 0-Token `/` Skills

- **Always-Active Project Packs:** Enabled in project `settings.json` (`enabledPlugins`) for packs you run every day in a brand folder, letting plain-English chat requests trigger skills directly.
- **On-Demand `/` Skills (`0` startup tokens):** Packs you use occasionally stay disabled at startup and expose lightweight project skill wrappers with `user-invocable: true` and `disable-model-invocation: true`, costing zero startup context tokens until you invoke `/<skill>`.

## Plugins (7)

| Plugin ID | Folder | Skills | Workflow Command | Reference |
|---|---|---|---|---|
| `gk` | [`plugins/getknown-core`](./plugins/getknown-core/README.md) | 12 | `/run-brand-setup` | [plugin.json](./plugins/getknown-core/.claude-plugin/plugin.json) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/.claude-plugin/plugin.json) |
| `gk-social` | [`plugins/01-social-tov`](./plugins/01-social-tov/README.md) | 3 | `/run-daily-social` | [plugin.json](./plugins/01-social-tov/.claude-plugin/plugin.json) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/.claude-plugin/plugin.json) |
| `gk-design` | [`plugins/02-design-decks-pages`](./plugins/02-design-decks-pages/README.md) | 3 | `/run-deck-or-page` | [plugin.json](./plugins/02-design-decks-pages/.claude-plugin/plugin.json) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/02-design-decks-pages/.claude-plugin/plugin.json) |
| `gk-motion` | [`plugins/03-animated-infographics`](./plugins/03-animated-infographics/README.md) | 2 | `/run-data-motion` | [plugin.json](./plugins/03-animated-infographics/.claude-plugin/plugin.json) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/03-animated-infographics/.claude-plugin/plugin.json) |
| `gk-video` | [`plugins/04-shortform-video-engine`](./plugins/04-shortform-video-engine/README.md) | 5 | `/run-short-video` | [plugin.json](./plugins/04-shortform-video-engine/.claude-plugin/plugin.json) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/.claude-plugin/plugin.json) |
| `gk-agency` | [`plugins/05-agency-growth`](./plugins/05-agency-growth/README.md) | 2 | `/run-competitor-audit` | [plugin.json](./plugins/05-agency-growth/.claude-plugin/plugin.json) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/05-agency-growth/.claude-plugin/plugin.json) |
| `gk-director` | [`plugins/06-brainstorm-and-director`](./plugins/06-brainstorm-and-director/README.md) | 5 | `/run-creative-director` | [plugin.json](./plugins/06-brainstorm-and-director/.claude-plugin/plugin.json) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/06-brainstorm-and-director/.claude-plugin/plugin.json) |

## Skills by Plugin (32 Total)

### `gk` · [`plugins/getknown-core`](./plugins/getknown-core/README.md)

| Skill | Description | Links |
|---|---|---|
| `/brand-extract` | Use when given a website URL or local HTML file to extract brand colors, fonts, and WCAG 2.2 AA contrast pairs into your brand folder. | [SKILL.md](./plugins/getknown-core/skills/brand-extract/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/brand-extract/SKILL.md) |
| `/claude-md` | Use when creating, updating, or compacting global (~/.claude/CLAUDE.md, <=60 lines) or project-bound (./CLAUDE.md, <=120 lines) instruction files, brand summaries, ToV pointers, and active vs on-demand skill profiles. | [SKILL.md](./plugins/getknown-core/skills/claude-md/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/claude-md/SKILL.md) |
| `/claude-md-builder` | Backwards-compatible alias for /claude-md: create, update, or compact global (<=60 lines), project (<=120 lines), and per-client (<=150 lines) CLAUDE.md instruction files. | [SKILL.md](./plugins/getknown-core/skills/claude-md-builder/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/claude-md-builder/SKILL.md) |
| `/cost-check` | Use before running optional external paid APIs to check or reserve estimated USD spend against per-run and daily safety limits. | [SKILL.md](./plugins/getknown-core/skills/cost-check/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/cost-check/SKILL.md) |
| `/discover-claude-code` | Use when onboarding a marketer to Claude Desktop, explaining brand folders, slash commands, and visual browser pages. | [SKILL.md](./plugins/getknown-core/skills/discover-claude-code/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/discover-claude-code/SKILL.md) |
| `/icp` | Use when building, auditing, or updating a brand's Ideal Customer Profile (ICP), buyer segments, JTBD triggers, verbatim buyer language, and qualification scorecard from existing brand materials, call notes, CRM data, or website. | [SKILL.md](./plugins/getknown-core/skills/icp/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/icp/SKILL.md) |
| `/panic-undo` | Use when the user wants to preview or roll back the last change to their voice file, brand design guide, instruction sheet, or campaign drafts. | [SKILL.md](./plugins/getknown-core/skills/panic-undo/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/panic-undo/SKILL.md) |
| `/provider-connector` | Use when checking local tool readiness or connecting optional external API keys safely without pasting secrets into chat. | [SKILL.md](./plugins/getknown-core/skills/provider-connector/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/provider-connector/SKILL.md) |
| `/quickstart` | Use when setting up any new or existing project folder: asks brand URL/materials and frequent job types, configures Always-Active vs 0-token on-demand skills, extracts Brand and Tone-of-Voice .md files, writes ./CLAUDE.md, and stops cleanly. | [SKILL.md](./plugins/getknown-core/skills/quickstart/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/quickstart/SKILL.md) |
| `/review-board` | Use when opening the browser Approval Board, exporting local or encrypted client review packs, and applying saved human approval decisions. | [SKILL.md](./plugins/getknown-core/skills/review-board/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/review-board/SKILL.md) |
| `/setup-marketer` | Use when setting up a marketing studio folder, creating brand workspaces, checking local Mac or Windows tools, or configuring Claude Desktop. | [SKILL.md](./plugins/getknown-core/skills/setup-marketer/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/setup-marketer/SKILL.md) |
| `/tov-extract` | Use when analyzing 3 to 20 sample posts or transcripts to build a structured Tone-of-Voice profile in your brand folder. | [SKILL.md](./plugins/getknown-core/skills/tov-extract/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/tov-extract/SKILL.md) |

### `gk-social` · [`plugins/01-social-tov`](./plugins/01-social-tov/README.md)

| Skill | Description | Links |
|---|---|---|
| `/draft-post` | Use when drafting LinkedIn, Instagram, X, or Telegram posts in the client Tone of Voice verified by readability checks. | [SKILL.md](./plugins/01-social-tov/skills/draft-post/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/skills/draft-post/SKILL.md) |
| `/topic-radar` | Use when scanning industry news, RSS, Hacker News, Reddit, or optional connected research sources for high-signal content angles. | [SKILL.md](./plugins/01-social-tov/skills/topic-radar/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/skills/topic-radar/SKILL.md) |
| `/what-worked` | Use after Approval Board sign-off to diff human edits against drafts, log campaign learnings, and apply confirmed voice rules. | [SKILL.md](./plugins/01-social-tov/skills/what-worked/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/skills/what-worked/SKILL.md) |

### `gk-design` · [`plugins/02-design-decks-pages`](./plugins/02-design-decks-pages/README.md)

| Skill | Description | Links |
|---|---|---|
| `/brand-banners` | Use when generating branded social media banners (#06 social-banner-sheet: 1200x628, 1080x1350, 1080x1080, 1080x1920) in HTML/SVG and exporting high-DPI PNGs. | [SKILL.md](./plugins/02-design-decks-pages/skills/brand-banners/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/02-design-decks-pages/skills/brand-banners/SKILL.md) |
| `/launch-page` | Use when building a conversion-focused lead-magnet, webinar, or course landing page (#07 conversion-launch-page) exported as a self-contained HTML bundle. | [SKILL.md](./plugins/02-design-decks-pages/skills/launch-page/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/02-design-decks-pages/skills/launch-page/SKILL.md) |
| `/slide-deck` | Use when building viewport-locked 16:9 HTML/PDF/PPTX presentation decks (#04 exec-deck-16x9) or 4:5 carousels (#05 social-carousel-4x5) styled in extracted brand tokens. | [SKILL.md](./plugins/02-design-decks-pages/skills/slide-deck/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/02-design-decks-pages/skills/slide-deck/SKILL.md) |

### `gk-motion` · [`plugins/03-animated-infographics`](./plugins/03-animated-infographics/README.md)

| Skill | Description | Links |
|---|---|---|
| `/build-infographic` | Use when rendering a 1080x1350 LinkedIn infographic (#01 comparison-grid, #02 step-by-step-flow, #03 iceberg-breakdown) as crisp PNG/PDF and 30fps animated MP4 in brand tokens. | [SKILL.md](./plugins/03-animated-infographics/skills/build-infographic/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/03-animated-infographics/skills/build-infographic/SKILL.md) |
| `/clone-layout-style` | Use when reverse-engineering a reference infographic grid, spacing rhythm, and motion curve without copying creator IP. | [SKILL.md](./plugins/03-animated-infographics/skills/clone-layout-style/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/03-animated-infographics/skills/clone-layout-style/SKILL.md) |

### `gk-video` · [`plugins/04-shortform-video-engine`](./plugins/04-shortform-video-engine/README.md)

| Skill | Description | Links |
|---|---|---|
| `/brand-teardown-script` | Use when scripting a 60-second 9:16 brand teardown video scored by the 4-factor hook retention model and 3.2 words/sec beat budget. | [SKILL.md](./plugins/04-shortform-video-engine/skills/brand-teardown-script/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/brand-teardown-script/SKILL.md) |
| `/harvest-visual-proof` | Use when capturing high-DPI website, headline, and pricing proof screenshots for a short-form teardown video or audit deck. | [SKILL.md](./plugins/04-shortform-video-engine/skills/harvest-visual-proof/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/harvest-visual-proof/SKILL.md) |
| `/publish-shortform` | Use when packaging approved 9:16 reels with platform-native captions into a local review-pack.zip or publishing via configured social APIs. | [SKILL.md](./plugins/04-shortform-video-engine/skills/publish-shortform/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/publish-shortform/SKILL.md) |
| `/render-avatar-reel` | Use when compositing a 60-second 9:16 short-form video (#08 reel-9x16-pip, #09 capture-avatar-stage) with circular PiP avatar video or portrait, cleaned spoken audio, and synced captions. | [SKILL.md](./plugins/04-shortform-video-engine/skills/render-avatar-reel/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/render-avatar-reel/SKILL.md) |
| `/splicebay-studio` | Use when cutting spoken retakes, trimming dead air, and balancing spoken audio locally or via an optional Splicebay Video Editor server. | [SKILL.md](./plugins/04-shortform-video-engine/skills/splicebay-studio/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/splicebay-studio/SKILL.md) |

### `gk-agency` · [`plugins/05-agency-growth`](./plugins/05-agency-growth/README.md)

| Skill | Description | Links |
|---|---|---|
| `/client-audit-pack` | Use when generating a 5-minute prospect pitch pack: 7-channel website teardown, prospect-branded HTML/PDF/PPTX audit deck (#10 standalone-audit-deck), 2 sample posts, and 1 static benchmark infographic (#11 standalone-infographic). | [SKILL.md](./plugins/05-agency-growth/skills/client-audit-pack/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/05-agency-growth/skills/client-audit-pack/SKILL.md) |
| `/repurpose-pack` | Use when turning a webinar transcript, course lesson, or long-form video into a multi-format social and content campaign matched to your installed pack. | [SKILL.md](./plugins/05-agency-growth/skills/repurpose-pack/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/05-agency-growth/skills/repurpose-pack/SKILL.md) |

### `gk-director` · [`plugins/06-brainstorm-and-director`](./plugins/06-brainstorm-and-director/README.md)

| Skill | Description | Links |
|---|---|---|
| `/brainstorm-angle` | Use before drafting any campaign, landing page, deck, or video to run a 1-question-at-a-time interview that locks topic, channels, goal, and sources into a campaign brief. | [SKILL.md](./plugins/06-brainstorm-and-director/skills/brainstorm-angle/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/06-brainstorm-and-director/skills/brainstorm-angle/SKILL.md) |
| `/copy-legend` | Use when drafting or rewriting headlines, landing pages, emails, or social posts through proven direct-response and editorial copywriting lenses. | [SKILL.md](./plugins/06-brainstorm-and-director/skills/copy-legend/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/06-brainstorm-and-director/skills/copy-legend/SKILL.md) |
| `/emil-design-polish` | Use when building or reviewing landing pages, slide decks, interactive HTML boards, or UI animations with precision spring-physics UI and motion polish. | [SKILL.md](./plugins/06-brainstorm-and-director/skills/emil-design-polish/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/06-brainstorm-and-director/skills/emil-design-polish/SKILL.md) |
| `/opuscar-director` | Use when directing code-generated films, animated explainers, or parameterized ad batches using Lemo-Opuscar (59 modular library styles #12..#70 + 98 film anthology showcase specs), Remotion, or the HTML stage compositor. | [SKILL.md](./plugins/06-brainstorm-and-director/skills/opuscar-director/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/06-brainstorm-and-director/skills/opuscar-director/SKILL.md) |
| `/parallel-sprint` | Use when running multi-channel campaign launches, multi-prospect agency teardowns, or batch asset production across isolated parallel subagents. | [SKILL.md](./plugins/06-brainstorm-and-director/skills/parallel-sprint/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/06-brainstorm-and-director/skills/parallel-sprint/SKILL.md) |

## Workflow Commands (7)

| Command | Plugin | Description | Source |
|---|---|---|---|
| `/run-brand-setup` | `gk` | Use when setting up a new client workspace, extracting brand tokens from a website, seeding Tone of Voice, and checking providers. | [run-brand-setup.md](./plugins/getknown-core/commands/run-brand-setup.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/commands/run-brand-setup.md) |
| `/run-daily-social` | `gk-social` | Use when running the daily social and channel copy workflow: topic radar scan, human-voice post drafting for LinkedIn, Instagram, X, or Telegram, Approval Board sign-off, and voice learning. | [run-daily-social.md](./plugins/01-social-tov/commands/run-daily-social.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/commands/run-daily-social.md) |
| `/run-deck-or-page` | `gk-design` | Use when building branded social banner packs, 16:9 HTML/PDF/PPTX slide decks, or lead-magnet and webinar landing pages. | [run-deck-or-page.md](./plugins/02-design-decks-pages/commands/run-deck-or-page.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/02-design-decks-pages/commands/run-deck-or-page.md) |
| `/run-data-motion` | `gk-motion` | Use when creating LinkedIn creator infographics or 30fps animated data visuals in 1080x1350 4:5 format. | [run-data-motion.md](./plugins/03-animated-infographics/commands/run-data-motion.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/03-animated-infographics/commands/run-data-motion.md) |
| `/run-short-video` | `gk-video` | Use when turning a brand teardown or raw talking-head take into a ready-to-publish 9:16 short-form video reel with PiP avatar and captions. | [run-short-video.md](./plugins/04-shortform-video-engine/commands/run-short-video.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/commands/run-short-video.md) |
| `/run-competitor-audit` | `gk-agency` | Use when running a 5-minute 7-channel competitor or prospect teardown and generating a prospect-branded audit deck, 2 sample posts, and 1 benchmark infographic. | [run-competitor-audit.md](./plugins/05-agency-growth/commands/run-competitor-audit.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/05-agency-growth/commands/run-competitor-audit.md) |
| `/run-creative-director` | `gk-director` | Use when brainstorming a campaign angle, directing a code-built Lemo-Opuscar or Remotion film, applying precision spring-physics UI and motion polish, or running a classic direct-response copywriting pass. | [run-creative-director.md](./plugins/06-brainstorm-and-director/commands/run-creative-director.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/06-brainstorm-and-director/commands/run-creative-director.md) |

## Isolated Subagents (2)

| Subagent | Plugin | Description | Source |
|---|---|---|---|
| `gk-renderer` | `gk` | Use for forked HTML/SVG banner generation, 16:9 slide decks, CRO launch pages, 1080x1350 animated infographics, and 9:16 PiP video rendering. | [gk-renderer.md](./plugins/getknown-core/agents/gk-renderer.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/agents/gk-renderer.md) |
| `gk-researcher` | `gk` | Use for forked brand CSS/HTML extraction, 7-channel web/social teardowns, topic radar scans, visual proof harvesting, and layout vision deconstruction. | [gk-researcher.md](./plugins/getknown-core/agents/gk-researcher.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/agents/gk-researcher.md) |

## Machine-Readable Manifests

- [`public-files-manifest.json`](./public-files-manifest.json) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/public-files-manifest.json)): Maps every plugin ID, skill slug, command, and agent to its exact GitHub blob and raw URLs.
- [`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/.claude-plugin/marketplace.json)): Claude Code plugin marketplace catalog.
- [`plugins/getknown-core/templates/template-catalog-summary.md`](./plugins/getknown-core/templates/template-catalog-summary.md) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/templates/template-catalog-summary.md)): Markdown summary of all **70** numbered visual templates (`#01`..`#70`).
