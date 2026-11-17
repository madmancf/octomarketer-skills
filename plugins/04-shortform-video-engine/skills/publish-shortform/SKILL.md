---
name: publish-shortform
description: Use when packaging approved 9:16 reels with platform-native captions into a local review-pack.zip or publishing via configured social APIs.
argument-hint: "<campaign-id> [--client <slug>]"
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Multi-Platform Short-Form Publish Pack (`/publish-shortform`)

Package an approved `1080x1920` (`9:16`) MP4 reel with platform-native captions and cover crop notes into a local `<sprint>-review-pack.zip` for `$0.00`, with optional API publishing when social credentials are configured.

## Local Default & Optional Connected Publishing

| Option | What It Does | Setup |
|---|---|---|
| **Local Publish Bundle (Default)** | Writes per-platform captions + `approved/shortform-publish-pack.md` and exports `<sprint>-review-pack.zip` via `gk publish-review-link --provider local` | `$0.00` (Zero API keys required) |
| **Splicebay Video Editor Social Publish** | Publishes to connected Instagram Reels, TikTok (`is_aigc` flag), or YouTube Shorts when OAuth is configured on a running Splicebay server | Optional `SPLICEBAY_URL` + `SPLICEBAY_API_KEY` |
| **Postiz API** | Queues approved posts and reels to a self-hosted or cloud Postiz workspace | Optional `POSTIZ_API_KEY` |

## Step 1: Safe-Zone, Audio & Pacing Verification

Verify `exports/reel-final.mp4` and `drafts/reel-script.json`:
- **Format & Audio:** `1080x1920` (`9:16`), `30fps`, H.264 + AAC balanced spoken audio.
- **Bottom Safe Zone:** Captions and circular PiP sit at `bottom >= 250px` clear of TikTok, Reels, and Shorts UI chrome.
- **Right-Rail Safe Zone:** Headline text stays `>= 120px` clear of right-rail action icons during full-screen cuts.
- **Beat Pacing:** Confirm spoken cadence stays `<= 3.2 words/sec` across all 5 beats.

## Step 2: Draft & Lint Platform-Native Captions

Draft platform-specific captions and check each caption with `gk lint` against its target platform rules:
1. **Instagram Reels (`--platform instagram`):** Opening hook line `<= 125 chars` before the caption fold, concise body copy, and `4:5` profile-grid cover crop notes.
2. **TikTok:** Direct 1 to 2 line caption with 3 to 5 plain-language search terms (and `is_aigc` disclosure when synthetic voice or avatar assets are used).
3. **YouTube Shorts:** Searchable `< 60 char` title plus a 1-line pinned comment CTA.

Assemble the verified captions into `clients/<client>/campaigns/<sprint>/approved/shortform-publish-pack.md`.

## Step 3: Export Local Review Bundle

Export the standalone local review `.zip` (`--provider local` runs offline without cloud upload prompts; `--provider vercel` or `--provider cloudflare` prompts for confirmation before uploading):
```bash
./plugins/getknown-core/bin/gk publish-review-link --client <client> --campaign <sprint> --provider local
```
If `SPLICEBAY_URL` or `POSTIZ_API_KEY` is configured in `gk provider-health`, ask for explicit user confirmation of the target platform and publish timestamp before sending any external publish request.
