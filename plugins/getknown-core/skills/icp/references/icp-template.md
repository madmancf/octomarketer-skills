# Canonical `brand/icp.md` Output Template (`/icp`)

Use this exact 10-section H2 structure when writing `./brand/icp.md` (standalone brand folder) or `clients/<slug>/brand/icp.md` (multi-client workspace). Keep `## 1. Quick-Reference Card` at or under `40` lines so downstream copy, social, deck, and landing-page skills can load `## 1` alone when context budget is tight.

```markdown
# Ideal Customer Profile: <Brand Name> (`<slug-or-folder>`)

> **Updated:** `<YYYY-MM-DD>` · **Stage:** `<Early Customer Profile (ECP - Hypothesis) | Validated ICP>` · **Track:** `<Track A: B2B | Track B: Creator/Prosumer/B2C | Track C: Multi-Product>`

## 1. Quick-Reference Card
- **10-Second Qualification Filter:** `<One-sentence pass/fail test a teammate can apply in 10 seconds>`
- **Valid For:** `<Offers, products, or motions covered by this profile>`
- **Not Valid For:** `<Adjacent segments, products, or motions explicitly out of scope>`
- **Top 3 Narrowing Traits:**
  1. `<Trait 1 with concrete range/context>` `[Verified | Inferred | Proxy: <src>]`
  2. `<Trait 2 with concrete workflow/stack signal>` `[Verified | Inferred | Proxy: <src>]`
  3. `<Trait 3 with concrete ownership/budget signal>` `[Verified | Inferred | Proxy: <src>]`
- **#1 Urgent Trigger ("What breaks next quarter if they do nothing?"):** `<Specific deadline, cost leak, or operational failure>`
- **#1 Verbatim Buyer Pain:** `"<Exact buyer quote or recurring problem phrase>"` `[<n>]`
- **#1 Non-Obvious Alternative:** `<Spreadsheets, manual scripts, agency Band-Aid, or doing nothing>`
- **#1 Hard Disqualifier:** `<Immediate walk-away signal and why>`
- **`X over Y` Copy & GTM Tradeoff Rules:**
  1. `<Concrete priority X> over <tempting distraction Y>`
  2. `<Concrete priority X> over <tempting distraction Y>`
  3. `<Concrete priority X> over <tempting distraction Y>`

## 2. Source Inventory & Evidence Basis
- **Value-Cohort Pre-Filter:** `<Which top-retention / fastest-TTV / highest-LTV cohort was profiled, who was excluded, and any inbound/warm-intro survivorship bias warning>`

| # | Source | Type | Date | Sample / Scope | Skew / Bias Note |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `[1]` | `<File path or URL>` | `<CRM / Transcript / Docs / Website / Reviews>` | `<YYYY-MM-DD>` | `<Exact count or scope>` | `<e.g., Website = self-portrait; warm-intro bias>` |

## 3. Target Segment & Attributes

<!-- For Track A (B2B Sales / Hybrid PLG / Agency), include Firmographic, Technographic, Behavioral tables + Segment Tiers + Verticals: -->
| Dimension | Attribute | Ideal Range / Signal | Provenance | Why It Matters |
| :--- | :--- | :--- | :--- | :--- |
| **Firmographic** | Company Size & Revenue Floor | `<Range or _Not enough data: only your CRM or team can confirm this._>` | `[Verified | Inferred | Team-Only Gap]` | `<Operational reason>` |
| **Firmographic** | Geography & Team Structure | `<Target geo & team shape>` | `[Verified | Inferred]` | `<Operational reason>` |
| **Technographic** | Core Stack & Incumbent Tools | `<Systems in place>` | `[Verified | Inferred | Proxy]` | `<Integration or switching hook>` |
| **Behavioral** | Build-vs-Buy & Buying Motion | `<Self-serve, founder-led, committee>` | `[Verified | Inferred]` | `<Sales cycle impact>` |

<!-- For Track B (Creator / Education / Indie / Prosumer / B2C), replace corporate firmographics with Super-Specific Who (3 hyper-narrow traits), High-Expectation Customer (HXC), Usage Context, and AI Posture (when relevant). -->

### Segment Tiers & Priority Verticals
- **Tier 1 (Core Beachhead):** `<Fastest close, highest retention, sharpest pain>`
- **Tier 2 (Expansion Fit):** `<Strong value, 1 missing accelerator or longer onboarding>`
- **Tier 3 (Opportunistic Inbound Only):** `<Accept self-serve if inbound, never spend outbound effort>`
- **Priority Verticals (Ranked by Evidence Count):** `<1. Vertical A (proof count + lead angle); 2. Vertical B (...)>`
- **Secondary Verticals:** `<Vertical + why secondary + angle when inbound arrives>`

## 4. Buying Roles & Internal Pitch

<!-- Track A: Champion + Economic Buyer + Primary Blocker (no two roles share the same deal function). Track B: Decision Maker + Peer/Community Influencer + Skepticism Trigger. -->
| Role | Title / Archetype | Core Win Metric | Personal Risk / Fear | How to Equip / Disarm |
| :--- | :--- | :--- | :--- | :--- |
| **Champion** | `<Role>` | `<Metric>` | `<What reputation or time they risk if this fails>` | `<Proof asset>` |
| **Economic Buyer** | `<Role>` | `<ROI / payback metric>` | `<Budget waste or shelfware fear>` | `<Payback proof>` |
| **Primary Blocker** | `<Security / IT / Finance / Incumbent owner>` | `<Risk avoidance>` | `<Late-stage objection that stalls deals>` | `<Pre-emptive answer>` |

- **Champion's 30-Second Internal Pitch (Spoken Word-for-Word to Boss / CFO):**
  > `"<2 to 3 plain-English sentences the Champion actually says in Slack or a budget check-in to get approval>"`

## 5. Jobs-to-be-Done, Triggers & Four Forces
- **Core Solution-Free Job Statement:** `"When <circumstance>, I want to <progress without naming our product>, so I can <concrete outcome>."`
- **Job Dimensions:**
  - **Functional:** `<Practical task completed faster or cleaner>`
  - **Emotional:** `<How they want to feel instead of current stress>`
  - **Social:** `<How peers, clients, or leadership perceive them>`
  - **Big Hire (Purchase / Signup) vs. Little Hire (Recurring Habit):** `<Initial buying moment vs weekly/daily repeat ritual>`
- **Almost-Triggered State (Passive Nurture):** `<Aware of friction, tolerating workarounds, what content earns trust before they shop>`

| Catalyst Trigger ("Why Now?") | Observable External / CRM Signal | Urgency |
| :--- | :--- | :--- |
| `<Trigger 1: what breaks next quarter if ignored>` | `<Public or behavioral signal>` | `High` |
| `<Trigger 2>` | `<Public or behavioral signal>` | `Medium` |

- **Four Forces of Switching (`Push + Pull > Habit + Anxiety`):**
  - **Push (Current Pain):** `<Cost of staying in current workflow>`
  - **Pull (Desired Outcome):** `<Concrete attraction of the new workflow>`
  - **Habit (Inertia to Beat):** `<Why spreadsheets, scripts, or status quo feel comfortable>`
  - **Anxiety (New-Tool Fear):** `<Migration effort, learning curve, lock-in, or quality fear>`
- **Non-Obvious Alternatives:** `<Spreadsheets, manual copy-paste, interns, agencies, or doing nothing alongside named software rivals>`
- **"Bad Experience" Ghost (Prior Vendor Trauma):** `<Previous burned-finger purchase or overhyped tool that makes this buyer skeptical on sight>`

## 6. Verbatim VoC Language Bank

| Underlying Solution-Free Need | Verbatim Buyer Phrase / Quote | Frequency | Source |
| :--- | :--- | :--- | :--- |
| `<Need 1, never a feature name>` | `"<Exact buyer wording>"` | `recurring | concentrated | isolated` | `[<n>]` |
| `<Need 2>` | `"<Exact buyer wording>"` | `recurring | concentrated | isolated` | `[<n>]` |

- **Words Buyers Use (Mirror in Hooks & Headlines):** `<Comma-separated concrete practitioner terms>`
- **Words Buyers Distrust (Vendor-Echo Slop to Ban):** `<Comma-separated hype phrases that trigger instant bounce>`

## 7. Watering Holes & Channel Uniformity
- **Value Homogeneity + Channel Uniformity Check:** `<Pass/Fail + 1-line proof that segment members value the outcome similarly and gather in reachable places>`
- **Named Communities & Subreddits:** `<Exact r/... or Slack/Discord communities>`
- **Newsletters, Podcasts & Voices Followed:** `<Named publications, creators, or shows>`
- **High-Intent Search & Outbound Signals:** `<Exact search queries, job-posting keywords, or tech-stack signals>`

## 8. Disqualifiers, Anti-ICP & Hard Exclusions
- **Hard Exclusions / Blacklists (Pre-Score Pass/Fail Gates):**
  - `<Compliance, geography, unsupported stack, or business-model exclusions; write "None confirmed" if none>`
- **Deal-Killing Disqualifiers & Anti-ICP Patterns (With Why):**
  1. **No Problem or Budget Owner:** `<Why deals stall when nobody owns the metric or budget>`
  2. **High-Churn Mismatch Segment:** `<Segment that signs up for novelty or wrong use case and churns fast>`
  3. **Custom-Service / Wrong-Motion Expectation:** `<Pattern + concrete reason>`

## 9. Gate + Confidence-Normalized Fit Scorecard
1. **Step A: Hard Gates (Must Pass All Before Scoring):**
   - `[ ]` Outside Hard Exclusions / Blacklists in `## 8`
   - `[ ]` Named problem owner exists (and budget path matches offer price)
2. **Step B: Weighted Static Fit (`100` Total Weight; Known-Weight Normalized):**

| Dimension | Weight | `1.0` (Strong Fit) | `0.5` (Partial Fit) | `0.0` (Mismatch) |
| :--- | ---: | :--- | :--- | :--- |
| Segment / Vertical Fit | `25` | `<Tier 1 criteria>` | `<Tier 2 criteria>` | `<Outside target>` |
| Scale / Stage / Complexity | `20` | `<Ideal band>` | `<Adjacent band>` | `<Below floor / wrong scale>` |
| Champion & Decision Owner | `20` | `<Direct pain + budget path>` | `<Pain owner, unclear sign-off>` | `<No owner>` |
| Workflow / Stack Readiness | `15` | `<Ready stack/inputs>` | `<Minor setup friction>` | `<Incompatible workflow>` |
| Active Catalyst Trigger | `15` | `<High-urgency trigger live>` | `<Almost-triggered state>` | `<Zero urgency>` |
| Channel / Onboarding Fit | `5` | `<Matches core delivery>` | `<Needs light adaptation>` | `<Requires custom rebuild>` |

- **Scoring Formula (Missing-Data Safe):**
  - `Score = round(100 * sum(weight * level) / sum(weight of known dimensions))`
  - `Confidence = sum(weight of known dimensions)%` (flag `< 50%` as `"Needs enrichment"` rather than penalizing unresearched prospects as zeros)
  - **Tier Bands:** `>= 80` = **Tier 1 (Prioritize)** · `50-79` = **Tier 2 (Nurture / Qualify)** · `< 50` = **Tier 3 (Deprioritize)**

## 10. Open Team Questions & Learnings Log

### High-Impact Team Questions (`<= 5` max, `<= 35` words each)
1. `<Plain-English question 1 on private deal floor, churn, or win/loss reality>`
2. `<Plain-English question 2>`

### Append-Only Campaign & Sales Learnings
| Date | Campaign / Source | Audience Observation | Status |
| :--- | :--- | :--- | :--- |
| `<YYYY-MM-DD>` | `<Initial synthesis or sprint ID>` | `<What converted, resonated, or disqualified>` | `active` |

<!-- Optional for Track C only:
## Product Override: <Product Name>
- **Delta From Portfolio Floor:** `<Only attributes, triggers, roles, or disqualifiers that differ>`
-->
```
