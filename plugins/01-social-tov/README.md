# `gk-social` (01-social-tov)

Social Content & Brand Voice Engine: industry topic radar, plain-English drafting for LinkedIn, Instagram, X, and Telegram, visual Approval Board review, and voice learning from approved edits.

- **Plugin Manifest:** [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/.claude-plugin/plugin.json))
- **Models:** **Claude Opus 5.5** (`claude-opus-5-5`) for strategy, voice, decks, and creative direction; **Claude Sonnet 5.5** (`claude-sonnet-5-5`, `high` effort) for diagnostics, daily drafts, and subagent runs.

## Workflow Commands

- [`/run-daily-social`](./commands/run-daily-social.md) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/commands/run-daily-social.md)): Use when running the daily social and channel copy workflow: topic radar scan, human-voice post drafting for LinkedIn, Instagram, X, or Telegram, Approval Board sign-off, and voice learning.

## Skills (3)

| Skill | Description | Source |
|---|---|---|
| `/draft-post` | Use when drafting LinkedIn, Instagram, X, or Telegram posts in the client Tone of Voice verified by readability checks. | [SKILL.md](./skills/draft-post/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/skills/draft-post/SKILL.md) |
| `/topic-radar` | Use when scanning industry news, RSS, Hacker News, Reddit, or optional connected research sources for high-signal content angles. | [SKILL.md](./skills/topic-radar/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/skills/topic-radar/SKILL.md) |
| `/what-worked` | Use after Approval Board sign-off to diff human edits against drafts, log campaign learnings, and apply confirmed voice rules. | [SKILL.md](./skills/what-worked/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/01-social-tov/skills/what-worked/SKILL.md) |
