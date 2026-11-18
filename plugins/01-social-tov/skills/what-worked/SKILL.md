---
name: what-worked
description: Use after Approval Board sign-off to diff human edits against drafts, log campaign learnings, and apply confirmed voice rules.
argument-hint: "<verdict-json-path> [--client <slug>]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Post-Sprint Voice Retrospective (`/what-worked`)

Capture real human edits from the Approval Board into `tov/tov.md` and `campaigns/<sprint>/learnings.md` without ever mutating `CLAUDE.md`.

## Step 1: Compare First Drafts vs. Approved Finals

Inspect `clients/<client>/campaigns/<sprint>/drafts/draft-pack.json` and the saved approval verdict JSON (`clients/<client>/.getknown-approval.json`, `approval-decisions.json`, or pasted verdict payload):
1. **Inline Edits Diff:** Check `items[]` where `editedText` actually differs from `originalText` and `learnRuleConfirmed` is `true` (unchanged `Was === Now` items and factual corrections tagged `fact_fix_skip_tov` never add voice rules).
2. **Revision & Skip Patterns:** Check items marked `revise` (`changes_requested`) or `skip` (`rejected`) and note the exact phrasing that missed the mark.
3. **Live Engagement Signals (Optional):** Ask which published post drove the strongest replies, saves, or qualified inquiries.

## Step 2: Update Voice Profile & Campaign Learnings

1. **Promote Winners:** Save the top 1 to 2 approved posts into `clients/<client>/tov/winners/winner-<date>.md` with 3 concise notes on why the hook and sentence cadence worked.
2. **Log Anti-Examples:** Save rejected drafts in `clients/<client>/tov/anti-examples/` with the phrasing to avoid next sprint.
3. **Apply Confirmed Voice Edits Safely:** Direct `Edit` on `clients/*/tov/tov.md` is blocked by workspace guardrails, so apply confirmed verdict rules strictly via the `gk` CLI (`<= 250` lines; skips no-op unchanged items automatically):
   ```bash
   ./plugins/getknown-core/bin/gk tov apply --verdict clients/<client>/.getknown-approval.json --client <client>
   ```
4. **Write Sprint Learnings to `campaigns/<sprint>/learnings.md`:** Record positioning insights, offer angles, and audience takeaways in `clients/<client>/campaigns/<sprint>/learnings.md` (or `./campaigns/<sprint>/learnings.md`). When recurring buyer pains, triggers, or disqualifiers surface across approved campaigns, suggest an optional `/icp` refresh to merge confirmed evidence into `brand/icp.md` (`## 10. Open Team Questions & Learnings Log`). **Never edit or mutate `clients/<client>/CLAUDE.md` or root `CLAUDE.md` during `/what-worked`** (use `/claude-md` only when the user explicitly asks to revise `CLAUDE.md`).
