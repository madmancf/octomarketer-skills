---
name: brand-extract
description: Use when given a website URL or local HTML file to extract brand colors, fonts, and WCAG 2.2 AA contrast pairs into your brand folder.
argument-hint: "<url> [--client <slug>]"
context: fork
background: false
agent: gk:gk-researcher
effort: low
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Edit, Write, WebFetch
---

# Brand System Extractor (`/brand-extract`)

Extract a reusable design system from any explicit live website URL (including client-rendered React, Next.js, and Vite SPAs via bundled headless Chromium DOM inspection) and save it to `clients/<client>/brand/tokens.json` and `clients/<client>/brand/design.md`.

## Step 1: Resolve Target Client & Explicit Website URL

1. Identify the active client slug (for example `acme-cloud`; never overwrite `demo-brand`) and an explicit `--url <https://...>` (never guess `https://<slug>.com` when no URL was given).
2. Ensure `clients/<client>/` is initialized first:
   ```bash
   ./plugins/getknown-core/bin/gk client init "<CLIENT_SLUG>" --url "<TARGET_URL>"
   ```

## Step 2: Run Brand Token Extraction

```bash
./plugins/getknown-core/bin/gk brand-extract \
  --client "<CLIENT_SLUG>" \
  --url "<TARGET_URL>"
```

## Step 3: Validate Against `brand-tokens.schema.json`

Verify that `clients/<client>/brand/tokens.json` matches `${CLAUDE_PLUGIN_ROOT}/schemas/brand-tokens.schema.json` (or `./schemas/brand-tokens.schema.json`):
- `clientSlug`, `sourceUrl`, `extractedAt`, `radius` (for example `0.75rem`)
- `colors.primary`, `colors.accent`, `colors.secondary` extracted from live rendered DOM styles and CSS variables
- `colors.brandBlack` (dark luminance `< 0.25`, such as `#0F172A`), `colors.surfaceDark`, `colors.surfaceDarkAlt`
- `colors.backgroundLight`, `colors.borderLight`
- `typography.headingFont`, `typography.bodyFont`, and `typography.weights`
- If zero brand colors matched on the target URL (`fallbackUsed: true`, `preserveExactBrandHex: false`), flag the fallback clearly so the user can confirm their exact hex values.

## Step 4: Verify `brand/design.md`

Confirm `clients/<client>/brand/design.md` records verified WCAG 2.2 contrast ratios, badge text pairings, dark vs. light card surfaces, and spacing rules for the creative skills installed in `./plugins/` (`/brand-banners`, `/slide-deck`, `/launch-page`, and when installed, `/build-infographic` and `/render-avatar-reel`).
