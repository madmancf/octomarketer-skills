---
name: brand-teardown-script
description: Use when scripting a 60-second 9:16 brand teardown video scored by the 4-factor hook retention model and 3.2 words/sec beat budget.
argument-hint: "<prospect-url-or-topic> [--client <slug>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Bash(mkdir *), Read, Edit, Write
---

# Brand Marketing Teardown & 60s Script Engine (`/brand-teardown-script`)

Analyze a target brand's live marketing funnel and write a 60-second (`1800`-frame @ `30fps`) spoken script built for the `${CLAUDE_PLUGIN_ROOT}/templates/reel-9x16-pip/index.html` single-clock compositor.

## Step 1: Analyze the Target Brand's Marketing Funnel

Ensure `clients/<client>/` exists (`./plugins/getknown-core/bin/gk client init <client> --url <url>` if new), then inspect verified facts from `clients/<client>/brand/teardown-report.json` (or run `./plugins/getknown-core/bin/gk teardown --client <client> --url <url> --crawl-depth 2`) across four mechanics:
1. **Hook Mechanic:** What specific headline, price point, or offer earns attention in the first 3.5 seconds?
2. **Acquisition Loop:** How do their live pages, product tours, or case studies convert visitors?
3. **Conversion Lever:** What CTA structure, pricing tier, or proof closes the buyer?
4. **Viewer Takeaway:** One concrete tactic the viewer can apply right away.

## Step 2: Map to the 5-Beat Camera Clock (130 to 150 Words Max)

Structure the script into the 5 camera-cut beats used by `${CLAUDE_PLUGIN_ROOT}/templates/reel-9x16-pip/index.html`:

| Beat | Timecode (`30fps`) | Camera Mode | Word Budget | Purpose |
|---|---|---|---|---|
| **Beat 1: Hook** | `00:00.0 - 00:03.5` (Frames `0-105`) | **`fullscreen`** (`1080x1920`) | `8 - 12` words | Direct opening claim looking straight into the lens. |
| **Beat 2: Teardown Part 1** | `00:03.5 - 00:25.0` (Frames `106-750`) | **`pip`** (`280x280` circle at `right: 48px, bottom: 260px`) | `45 - 55` words | Walk through proof cards #1 and #2 on the main canvas while the narrator sits in the circular PiP. |
| **Beat 3: Midpoint Reset** | `00:25.0 - 00:27.5` (Frames `751-825`) | **`fullscreen`** (`1080x1920`) | `6 - 10` words | Full-screen face cut to reset attention at the midpoint. |
| **Beat 4: Teardown Part 2** | `00:27.5 - 00:50.0` (Frames `826-1500`) | **`pip`** (`280x280` circle) | `45 - 55` words | Show proof snapshots #3 and #4 (live pricing, offer details, real proof) on the main stage. |
| **Beat 5: Payoff & CTA** | `00:50.0 - 01:00.0` (Frames `1501-1800`) | **`fullscreen`** (`1080x1920`) | `20 - 25` words | Full-screen narrator payoff and call to action. |

## Step 3: Readability & Beat-Budget Validation

1. Save the structured beat-clock JSON to `clients/<client>/campaigns/<sprint>/drafts/reel-script.json`.
2. Verify spoken copy with `./plugins/getknown-core/bin/gk lint --file <script-md> --platform instagram` and validate the `<= 3.2 words/sec` beat budget via `./plugins/getknown-core/bin/gk splicebay --transcript clients/<client>/campaigns/<sprint>/drafts/reel-script.json --client <client>`.
3. Run `/harvest-visual-proof` next to capture live website proof screenshots.
