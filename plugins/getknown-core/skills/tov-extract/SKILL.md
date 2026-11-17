---
name: tov-extract
description: Use when analyzing 3 to 20 sample posts or transcripts to build a structured Tone-of-Voice profile in your brand folder.
argument-hint: "[--client <slug>] [--from <path>] [--from-url <url>]"
context: fork
background: false
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Grep, Glob, Edit, Write, WebFetch
---

# Tone of Voice Extractor (`/tov-extract`)

Extract measurable writing mechanics from 3 to 20 real posts, pages, or transcripts and compile `clients/<client>/tov/tov.md` (`<= 250` lines) non-destructively.

## Inputs to Collect

Ensure `clients/<client>/` exists (`./plugins/getknown-core/bin/gk client init <client>` if new; never overwrite `demo-brand`), then collect real samples:
- High-performing LinkedIn, Instagram, X, or Telegram posts (or `clients/<client>/tov/voice-seed-pack.json` saved from the Setup Guide)
- Live founder or brand website copy (`--from-url <url>`) or workshop/podcast transcripts
- 1 to 3 rejected drafts ("never write like this")

## Step 1: Extract the 6 Voice Mechanics

Analyze the samples across six concrete mechanics:
1. **Sentence Cadence & Length:** Average words per sentence, short 2 to 5 word lines after longer sentences, and paragraph spacing.
2. **Hook Patterns:** How the opening 2 lines start (an audit metric, a specific mistake, a direct question, or a founder observation).
3. **Proof Habits:** How claims are backed up (named roles, exact numbers, live screenshots, concrete deliverables).
4. **Signature Vocabulary:** Everyday phrases the author uses on their live site and posts vs. corporate buzzwords they avoid (never ban words or structures the author uses as part of their real voice).
5. **Closing Style:** How posts close without formulaic engagement bait.
6. **Draft Quality Guardrails:** Combine client-specific taboos with `${CLAUDE_PLUGIN_ROOT}/references/anti-slop-gate.md` (repo fallback `./plugins/getknown-core/references/anti-slop-gate.md`) so automated drafts pass `gk lint`.

## Step 2: Save Voice Profile, Examples & Compile `tov.md`

1. Write `clients/<client>/tov/tov-profile.json` (`"schemaVersion": "1.2.3"`) validated against `${CLAUDE_PLUGIN_ROOT}/schemas/tov-profile.schema.json` (or `./plugins/getknown-core/schemas/tov-profile.schema.json`), preserving any existing custom author/locale fields or learned `L-*` rules unless a full reset was explicitly requested.
2. Save annotated winning posts to `clients/<client>/tov/winners/winner-01.md` (labeled `[Example]` if synthetic) and rejected examples to `clients/<client>/tov/anti-examples/slop-01.md`.
3. Compile `clients/<client>/tov/tov.md` (`<= 250` lines) via the `gk tov` CLI (direct `Edit` on `tov/tov.md` is denied by `.claude/settings.json`):
   ```bash
   ./plugins/getknown-core/bin/gk tov init --client <client> --from clients/<client>/tov/tov-profile.json
   ```

## Step 3: Sample Hook Check

Write a 60-word sample hook on a live topic, verify it with `./plugins/getknown-core/bin/gk lint --file <sample.md> --platform linkedin`, and ask: *"Does this sound like you on a good day, or what should we tighten?"*
