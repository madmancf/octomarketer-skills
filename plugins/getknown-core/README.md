# `gk` (getknown-core)

Core Studio Base Plugin: guided /quickstart setup, brand folder organizer, website color and font extractor, Brand Voice Guide builder, visual Approval Board, and automatic backup restore.

- **Plugin Manifest:** [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/.claude-plugin/plugin.json))
- **Models:** **Claude Opus 5.5** (`claude-opus-5-5`) for strategy, voice, decks, and creative direction; **Claude Sonnet 5.5** (`claude-sonnet-5-5`, `high` effort) for diagnostics, daily drafts, and subagent runs.

## Workflow Commands

- [`/run-brand-setup`](./commands/run-brand-setup.md) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/commands/run-brand-setup.md)): Use when setting up a new client workspace, extracting brand tokens from a website, seeding Tone of Voice, and checking providers.

## Skills (11)

| Skill | Description | Source |
|---|---|---|
| `/brand-extract` | Use when given a website URL or local HTML file to extract brand colors, fonts, and WCAG 2.2 AA contrast pairs into your brand folder. | [SKILL.md](./skills/brand-extract/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/brand-extract/SKILL.md) |
| `/claude-md` | Use when creating, updating, or compacting global (~/.claude/CLAUDE.md, <=60 lines) or project-bound (./CLAUDE.md, <=120 lines) instruction files, brand summaries, ToV pointers, and active vs on-demand skill profiles. | [SKILL.md](./skills/claude-md/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/claude-md/SKILL.md) |
| `/claude-md-builder` | Backwards-compatible alias for /claude-md: create, update, or compact global (<=60 lines), project (<=120 lines), and per-client (<=150 lines) CLAUDE.md instruction files. | [SKILL.md](./skills/claude-md-builder/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/claude-md-builder/SKILL.md) |
| `/cost-check` | Use before running optional external paid APIs to check or reserve estimated USD spend against per-run and daily safety limits. | [SKILL.md](./skills/cost-check/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/cost-check/SKILL.md) |
| `/discover-claude-code` | Use when onboarding a marketer to Claude Desktop, explaining brand folders, slash commands, and visual browser pages. | [SKILL.md](./skills/discover-claude-code/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/discover-claude-code/SKILL.md) |
| `/panic-undo` | Use when the user wants to preview or roll back the last change to their voice file, brand design guide, instruction sheet, or campaign drafts. | [SKILL.md](./skills/panic-undo/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/panic-undo/SKILL.md) |
| `/provider-connector` | Use when checking local tool readiness or connecting optional external API keys safely without pasting secrets into chat. | [SKILL.md](./skills/provider-connector/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/provider-connector/SKILL.md) |
| `/quickstart` | Use when setting up any new or existing project folder: asks brand URL/materials and frequent job types, configures Always-Active vs 0-token on-demand skills, extracts Brand and Tone-of-Voice .md files, writes ./CLAUDE.md, and stops cleanly. | [SKILL.md](./skills/quickstart/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/quickstart/SKILL.md) |
| `/review-board` | Use when opening the browser Approval Board, exporting local or encrypted client review packs, and applying saved human approval decisions. | [SKILL.md](./skills/review-board/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/review-board/SKILL.md) |
| `/setup-marketer` | Use when setting up a marketing studio folder, creating brand workspaces, checking local Mac or Windows tools, or configuring Claude Desktop. | [SKILL.md](./skills/setup-marketer/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/setup-marketer/SKILL.md) |
| `/tov-extract` | Use when analyzing 3 to 20 sample posts or transcripts to build a structured Tone-of-Voice profile in your brand folder. | [SKILL.md](./skills/tov-extract/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/skills/tov-extract/SKILL.md) |

## Subagents (2)

- [`gk-renderer`](./agents/gk-renderer.md) ([Blob](https://github.com/madmancf/octomarketer-skills/blob/main/plugins/getknown-core/agents/gk-renderer.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/agents/gk-renderer.md)): Use for forked HTML/SVG banner generation, 16:9 slide decks, CRO launch pages, 1080x1350 animated infographics, and 9:16 PiP video rendering.
- [`gk-researcher`](./agents/gk-researcher.md) ([Blob](https://github.com/madmancf/octomarketer-skills/blob/main/plugins/getknown-core/agents/gk-researcher.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/getknown-core/agents/gk-researcher.md)): Use for forked brand CSS/HTML extraction, 7-channel web/social teardowns, topic radar scans, visual proof harvesting, and layout vision deconstruction.
