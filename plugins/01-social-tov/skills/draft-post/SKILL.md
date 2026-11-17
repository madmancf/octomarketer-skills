---
name: draft-post
description: Use when drafting LinkedIn, Instagram, X, or Telegram posts in the client Tone of Voice verified by readability checks.
argument-hint: "<topic-or-brief> [--client <slug>] [--platform linkedin|instagram|x|telegram]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Social & Channel Post Drafter (`/draft-post`)

Write clear, human-sounding posts for LinkedIn, Instagram, X, and Telegram grounded in `clients/<client>/tov/tov.md`, `CLAUDE.md`, and `tov/winners/`, verified by `gk lint` before opening the Approval Board.

## Step 1: Load Client Voice Memory & Campaign Brief

Read these files before drafting:
1. `clients/<client>/CLAUDE.md` (Audience ICP, live offer details, pricing, hard taboos, and active channels; never target channels the client does not run)
2. `clients/<client>/tov/tov.md` (Sentence cadence, hook patterns, real vocabulary, and learned `L-*` edit rules)
3. `clients/<client>/tov/winners/` (At least 1 winning post or `[Example]` reference to match cadence)
4. `clients/<client>/tov/anti-examples/` (Rejected phrasing patterns to avoid)
5. `clients/<client>/campaigns/<sprint>/campaign-brief.json` (Verified facts and source URLs; never invent study numbers or unverified benchmarks)

## Step 2: Draft Platform-Native Copy

Write channel-specific drafts rather than cross-posting identical copy:
- **LinkedIn (`linkedin`):** Concrete 2-line hook (`<= 210 chars` before the "see more" fold), short 1 to 3 sentence paragraphs, real proof or teardown steps, direct closing question.
- **Instagram (`instagram`):** Opening hook (`<= 125 chars` before the caption fold) that complements the carousel or `9:16` reel without repeating the cover headline word for word.
- **X / Threads (`x`):** High-density single post (`<= 280 chars`) or concise thread built around concrete receipts.
- **Telegram (`telegram`):** Direct channel post (`<= 180 chars` lead line before preview truncation), short scannable paragraphs or plain numbered takeaways, concrete links or receipts, and zero hashtag walls.

## Step 3: Run Readability & Anti-Slop Check

Verify every non-empty draft file via `gk lint`:

```bash
./plugins/getknown-core/bin/gk lint \
  --file clients/<client>/campaigns/<sprint>/drafts/post.md \
  --platform linkedin
```

What `gk lint` enforces:
1. **Readability & Punctuation:** Flesch reading ease `>= 47.0`, zero em-dash punctuation in automated drafts, zero negative-contrast cliches (`"It isn't X. It's Y."`), and zero AI filler words (`delve`, `crucial`, `robust`, `nuanced`, `multifaceted`, `tapestry`, `underscore`, `underscores`, `pivotal`, `seamless`, `game-changer`, `game-changing`, `transformative`, `leverage`, `utilize`, `synergy`, `testament`, `beacon`, `realm`, `unleash`, `elevate`, `supercharge`).
2. **Structural & Bullet Checks:** Blocks empty inputs, throat-clearing openers, copula avoidance (`serves as a`), false ranges, promotional inflation, stacked hedges, and bold-label bullet spam.
3. **Platform Fold & Length Caps:** Enforces LinkedIn `<= 210` char fold, Instagram `<= 125` char fold, Telegram scannability, and platform max character limits.

## Step 4: Save Draft Pack & Open Approval Board

Write the validated batch to `clients/<client>/campaigns/<sprint>/drafts/draft-pack.json` (with unreviewed items set to `verdict: "pending"`) matching `${GETKNOWN_CORE_ROOT:-./plugins/getknown-core}/schemas/draft-pack.schema.json` (or `./schemas/draft-pack.schema.json`), then launch `./plugins/getknown-core/bin/gk serve --daemon` and share the `/board?client=<client>` URL.
