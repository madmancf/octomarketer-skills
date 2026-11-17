# `gk-agency` (05-agency-growth)

Agency Prospect Audit & Content Repurposing: turn any public website URL into a 5-slide branded audit deck, 2 sample social posts, and 1 benchmark graphic before sales calls, or repurpose one webinar into a full campaign sprint.

- **Plugin Manifest:** [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/05-agency-growth/.claude-plugin/plugin.json))
- **Models:** **Claude Opus 5.5** (`claude-opus-5-5`) for strategy, voice, decks, and creative direction; **Claude Sonnet 5.5** (`claude-sonnet-5-5`, `high` effort) for diagnostics, daily drafts, and subagent runs.

## Workflow Commands

- [`/run-competitor-audit`](./commands/run-competitor-audit.md) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/05-agency-growth/commands/run-competitor-audit.md)): Use when running a 5-minute 7-channel competitor or prospect teardown and generating a prospect-branded audit deck, 2 sample posts, and 1 benchmark infographic.

## Skills (2)

| Skill | Description | Source |
|---|---|---|
| `/client-audit-pack` | Use when generating a 5-minute prospect pitch pack: 7-channel website teardown, prospect-branded HTML/PDF/PPTX audit deck (#10 standalone-audit-deck), 2 sample posts, and 1 static benchmark infographic (#11 standalone-infographic). | [SKILL.md](./skills/client-audit-pack/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/05-agency-growth/skills/client-audit-pack/SKILL.md) |
| `/repurpose-pack` | Use when turning a webinar transcript, course lesson, or long-form video into a multi-format social and content campaign matched to your installed pack. | [SKILL.md](./skills/repurpose-pack/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/05-agency-growth/skills/repurpose-pack/SKILL.md) |
