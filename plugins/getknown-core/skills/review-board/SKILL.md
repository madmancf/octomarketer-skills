---
name: review-board
description: Use when opening the browser Approval Board, exporting local or encrypted client review packs, and applying saved human approval decisions.
argument-hint: "[--client <slug>] [--campaign <id>]"
effort: low
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Human Approval Board (`/review-board`)

Give marketers and clients a visual browser board to edit posts inline (preserving paragraph breaks), preview videos, decks, PDFs, and infographics, score each draft (`Approve`, `Revise`, `Skip`), and export local or passcode-encrypted review packs.

## Mode A: Open the Approval Board or Export a Review Pack

1. Confirm `clients/<client>/campaigns/<sprint>/drafts/draft-pack.json` matches `${CLAUDE_PLUGIN_ROOT}/schemas/draft-pack.schema.json` (fallback `./plugins/getknown-core/schemas/draft-pack.schema.json`), with new unreviewed items defaulting to `verdict: "pending"`.
2. Start the Studio server in background daemon mode so it never blocks your session, and read `boardUrl` / `baseUrl` from its JSON output:
   ```bash
   ./plugins/getknown-core/bin/gk serve --daemon
   ```
   Share `<baseUrl>/board?client=<client>&campaign=<sprint>` (default `http://127.0.0.1:4318/board?client=<client>&campaign=<sprint>`) with the user.
3. **Exporting or Publishing a Client Review Pack:**
   - **Local Offline Bundle (`$0.00`, runs immediately without upload prompts):**
     ```bash
     ./plugins/getknown-core/bin/gk publish-review-link --client <client> --campaign <sprint> --provider local [--password <passcode>] [--no-attribution]
     ```
   - **Encrypted Cloud Link (`vercel` or `cloudflare`, prompts for confirmation first):**
     ```bash
     ./plugins/getknown-core/bin/gk publish-review-link --client <client> --campaign <sprint> --provider cloudflare
     ```
4. Tell the user:
   - *"Open the Approval Board link, edit any draft inline, choose `Approve`, `Revise`, or `Skip`, then click **Save Review Decisions** and **Copy Reply for Claude.app**."*

## Mode B: Apply Saved Approval Decisions

When the user replies after clicking **Save Review Decisions** (writing `clients/<client>/.getknown-approval.json` or `approval-decisions.json`) or pastes a verdict payload:

1. Validate the payload against `${CLAUDE_PLUGIN_ROOT}/schemas/review-verdict.schema.json` (fallback `./plugins/getknown-core/schemas/review-verdict.schema.json`).
2. Process each entry in `items[]`:
   - **`approved`**: Save publish-ready copy to `clients/<client>/campaigns/<sprint>/approved/<id>.md` using `editedText` (and optional `note`).
   - **`revise` or `changes_requested`**: Read `editedText` and `note`, rewrite the draft to address the feedback, verify with `gk lint --file <draft> --platform linkedin`, and update `draft-pack.json`.
   - **`skip` or `rejected`**: Save the rejected phrasing in `clients/<client>/tov/anti-examples/rejected-<id>.md` with any `note`.
3. Update `clients/<client>/tov/tov.md` from confirmed human edits (`learnRuleConfirmed: true` where `editedText` actually changed, skipping `fact_fix_skip_tov`) via:
   ```bash
   ./plugins/getknown-core/bin/gk tov apply --verdict clients/<client>/.getknown-approval.json --client <client>
   ```
