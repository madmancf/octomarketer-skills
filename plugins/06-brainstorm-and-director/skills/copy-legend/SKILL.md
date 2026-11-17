---
name: copy-legend
description: Use when drafting or rewriting headlines, landing pages, emails, or social posts through proven direct-response and editorial copywriting lenses.
argument-hint: "<draft-or-topic> [--lens classic-print|sales-letter|customer-voice|behavioral-reframe|scientific-proof|distinctive-reach|social-proof|focused-audience|guided-story|shareable-benchmark] [--client <slug>]"
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Classic Direct-Response & Editorial Copywriting Lenses (`/copy-legend`)

Apply 10 proven copywriting and behavioral conversion structures inside one skill while keeping every claim grounded in your brand's real voice and verified facts.

## Available Craft & Conversion Lenses

| Lens Identifier | Craft Style | Structural Mechanism Applied to the Draft |
| :--- | :--- | :--- |
| **`classic-print`** | **Classic Direct-Response Print** | **Research-first editorial authority.** Factual headline with concrete numbers and outcome, story-driven captions under visuals, zero unsupported adjectives, read-aloud rhythm. |
| **`sales-letter`** | **Long-Form Sales Letter** | **Personal letter & concrete stakes.** Opens on a specific scene or dollar-and-cents problem, short paragraphs, direct transitions, clear risk-reversed offer. |
| **`customer-voice`** | **Voice-of-Customer Conversion** | **Verbatim buyer language.** Pulls exact buyer complaints from `sources/` or `tov/winners/`, uses Problem-Agitate-Solve, and writes outcome button copy ("Get [Outcome]"). |
| **`behavioral-reframe`** | **Behavioral Value Reframe** | **Perceived effort & certainty.** Finds why buyers hesitate even when the math works and reframes perceived effort, certainty, or status. |
| **`scientific-proof`** | **Process & Receipt Specificity** | **Documented mechanism.** Names the exact hours, checks, or steps behind the deliverable with concrete numbers instead of vague claims. |
| **`distinctive-reach`** | **Category Entry & Distinctive Cues** | **Mental availability.** Anchors to clear category buying moments and repeats recognizable visual and verbal brand cues. |
| **`social-proof`** | **Practitioner Proof & Authority** | **Earned credibility.** Establishes practitioner authority, peer receipts, and shared identity before the call to action. |
| **`focused-audience`** | **Focused Practitioner Point of View** | **Specific audience selection.** Clear contrast between how serious operators work and the default manual habit. |
| **`guided-story`** | **Customer-as-Hero 3-Step Plan** | **Clarity arc.** Buyer -> Problem -> Guide -> 3-Step Plan -> Direct Call to Action -> Cost of Waiting -> Concrete Outcome. |
| **`shareable-benchmark`** | **Team-Shareable Benchmark** | **Organic pass-along utility.** Embeds a concrete benchmark or checklist readers forward inside team chat channels. |

*(Legacy shorthand `--legend` parameter aliases passed by existing scripts map automatically to the matching craft style above.)*

## Execution Rules

1. **Client Voice First, Structural Lens Second:**
   - Load `clients/<slug>/tov/tov.md` and `clients/<slug>/CLAUDE.md` first.
   - Apply the chosen lens's **argument structure**, keeping modern client vocabulary and verified facts only.
2. **Verify Every Draft With `gk lint`:**
   ```bash
   ./plugins/getknown-core/bin/gk lint --file clients/<slug>/campaigns/<sprint>/drafts/post.md --platform linkedin
   ```
3. **Side-by-Side Output:**
   - Show **Original vs. Lens Rewrite + 1-line Structural Reason**, save to `draft-pack.json`, and launch `/review-board` (`gk serve --daemon`).
