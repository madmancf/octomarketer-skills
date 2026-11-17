# `gk-video` (04-shortform-video-engine)

Short-Form Video & Talking-Head PiP Reel Engine (9:16): write 60-second website teardown scripts, capture live proof screenshots, trim silences and retakes locally on your Mac, render 1080x1920 Picture-in-Picture reels, and package platform captions.

- **Plugin Manifest:** [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/.claude-plugin/plugin.json))
- **Models:** **Claude Opus 5.5** (`claude-opus-5-5`) for strategy, voice, decks, and creative direction; **Claude Sonnet 5.5** (`claude-sonnet-5-5`, `high` effort) for diagnostics, daily drafts, and subagent runs.

## Workflow Commands

- [`/run-short-video`](./commands/run-short-video.md) ([Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/commands/run-short-video.md)): Use when turning a brand teardown or raw talking-head take into a ready-to-publish 9:16 short-form video reel with PiP avatar and captions.

## Skills (5)

| Skill | Description | Source |
|---|---|---|
| `/brand-teardown-script` | Use when scripting a 60-second 9:16 brand teardown video scored by the 4-factor hook retention model and 3.2 words/sec beat budget. | [SKILL.md](./skills/brand-teardown-script/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/brand-teardown-script/SKILL.md) |
| `/harvest-visual-proof` | Use when capturing high-DPI website, headline, and pricing proof screenshots for a short-form teardown video or audit deck. | [SKILL.md](./skills/harvest-visual-proof/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/harvest-visual-proof/SKILL.md) |
| `/publish-shortform` | Use when packaging approved 9:16 reels with platform-native captions into a local review-pack.zip or publishing via configured social APIs. | [SKILL.md](./skills/publish-shortform/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/publish-shortform/SKILL.md) |
| `/render-avatar-reel` | Use when compositing a 60-second 9:16 short-form video with circular PiP avatar video or portrait, cleaned spoken audio, and synced captions. | [SKILL.md](./skills/render-avatar-reel/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/render-avatar-reel/SKILL.md) |
| `/splicebay-studio` | Use when cutting spoken retakes, trimming dead air, and balancing spoken audio locally or via an optional Splicebay Video Editor server. | [SKILL.md](./skills/splicebay-studio/SKILL.md) · [Raw](https://raw.githubusercontent.com/madmancf/octomarketer-skills/main/plugins/04-shortform-video-engine/skills/splicebay-studio/SKILL.md) |
