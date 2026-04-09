---
name: okr-update
description: Generate and push weekly OKR status updates to Linear for ML team initiatives. Pulls data from Granola meeting notes, Notion All Hands doc, and Linear.
argument-hint: [initiative: partner|evoli|quality|all]
disable-model-invocation: true
---

# Weekly OKR Update

Generate and push a weekly OKR status update for the specified initiative(s).

**Initiative argument:** `$ARGUMENTS`

## Initiatives

| Key | Initiative | Linear ID |
|-----|-----------|-----------|
| `partner` | [ML] Deliver on ≥80% of partner team objectives (SWAG allocation) | `c318074d-106d-492c-98b4-4482a65b78df` |
| `evoli` | [ML] Complete technical imp. for Evoli architecture evaluation | `fe48d34f-f732-4a49-bcae-cf9a9e73414c` |
| `quality` | [KR Quality] Maintain p50 merchant quality score of 62% | `5a6e30e9-bfa4-4c49-a417-c81889f1c0a9` |
| `all` | Update all three initiatives sequentially | |

If no argument is provided, ask the user which initiative to update.

## Data Sources

### Primary: Notion ML All Hands doc
URL: https://www.notion.so/gorgias/ML-all-hands-9b5b1ca09f9d404d94594c7b2fdd537c

This is the main source. Find the most recent weekly rewind section. Within it:
- **OKR updates toggle**: Contains the partner team OKR completion table and merchant quality analysis
- **Project updates toggle**: Contains per-project status updates (who, why, what was done)

### Secondary: Granola meeting notes
- **For `partner`**: Use the most recent "ML all hands" meeting summary for additional context on project highlights
- **For `evoli`**: Use ALL "[ML] Evoli daily" meetings from the current week (Mon-Fri) for detailed progress
- **For `quality`**: Not needed (Notion has all the data)

### Reference: Previous Linear update
Always fetch the most recent status update for the initiative being updated, to match format and style.

## Instructions per Initiative

### `partner` - Partner Team Objectives

1. Fetch the OKR updates section from Notion All Hands doc
2. Fetch the Project updates section from Notion All Hands doc
3. Fetch the most recent "ML all hands" Granola meeting summary for enrichment
4. Fetch the previous Linear status update for format reference

**Structure:**
1. Progress tracker link: `https://docs.google.com/spreadsheets/d/1zTLuvLtqjcXPjIQ9fUWkuTjfI_NLf6hF3Qw4aAAv22I/edit?gid=1311664627#gid=1311664627`
2. Baseline/target line + weighted completion %
3. Summary table (Partner team | H1 Goal | ML SWAG allocated in Q1 | Progress). No extra notes or quality section.
4. Key Highlights section split into MLA initiatives and MLE initiatives
   - Each initiative gets a status emoji, a Notion-linked title, and 2-3 bullets
   - Exclude Evoli project updates (those go in the `evoli` initiative)

**Status emoji legend:**
🟡 In progress, 🟡🟢 Close to completion, 🟢 Completed, 🔴 At risk / on pause, ⚪ On hold

### `evoli` - Evoli Architecture

1. Fetch the Evoli project update from Notion All Hands doc
2. Fetch ALL "[ML] Evoli daily" Granola meetings for the current week
3. Fetch the previous Linear status update for format reference
4. If evaluation reports exist in Notion for the current week, fetch and summarize them

**Structure:**
1. KR title line
2. Progress % with date
3. **Latest Offline Eval Results section** (if reports exist, place prominently at top):
   - Release readiness report first, then detailed V3 vs V2 report
   - 3-4 bullet summary per report, linking to the Notion page
4. Weekly progress split into MLE and MLA sections
5. Next Steps section
6. Reference databases section at bottom:
   - [Evaluations DB](https://www.notion.so/gorgias/3131ae2178f58005a984f9e96cea0235?v=3131ae2178f580f3a4df000caa9127b0): Lists every scenario in a given offline eval run, with the number of tickets, detected failures, and MLA review breakdown (real failures, code-related failures, judge false negatives, and simulated shopper failures)
   - [Failures DB](https://www.notion.so/gorgias/3131ae2178f580f5a2faf8dd97c2c759?v=3131ae2178f580f28387000c0a70c824): Logs V3 failure modes identified from evaluations (e.g. not following guidance, hallucinating beyond knowledge), grouping tickets by issue to drive prompt/code fixes and track resolution across iterations

### `quality` - Merchant Quality

1. Fetch the merchant quality section from the OKR updates in Notion All Hands doc
2. Fetch the previous Linear status update for format reference

**Structure:**
1. Reference link to [Merchant quality rate definition](https://www.notion.so/gorgias/Merchant-quality-rate-revamp-for-2026-2ce1ae2178f5809eb22fd5ada1aa1cb0) at the top
2. H1 target + current score with WoW change
2. TL;DR blockquote summarizing whether the change is real or driven by pool composition shifts
3. Week-over-week comparison: pool size change, entries/exits with medians. Mention the qualifying threshold (minimum 5 ratings in a rolling 28-day window) so readers understand what "the pool" means.
4. Continuing merchant analysis (how much did quality move for merchants that stayed?)
5. Support vs Sales quality table
6. "Why the pool is shrinking" explanation

**Writing note for this initiative:** Avoid stats jargon like "compositional", "intent mix shifts", or "aggregate quality rate". Explain mechanisms in plain language (e.g. "rose mechanically because low-quality merchants dropped out").

## Writing Rules

These are mandatory. Do not deviate.

- **No semicolons.** Use commas instead.
- **No em dashes (—).** Use commas, colons, or periods instead.
- **Leadership-friendly language.** Every bullet must be understandable by someone unfamiliar with the initiative. No internal system names, no technical jargon, no implementation details that don't signal meaningful progress. Ask yourself: "Would a VP reading this for the first time understand this bullet?"
- **Concise.** 2-3 bullets per initiative in highlights sections. Lead with what changed and why it matters.
- **Preserve formatting.** Match the emoji usage, heading levels, bold/italic patterns, and link style of previous updates.

## Workflow

1. Gather all data from sources listed above
2. Draft the full update and show it to the user for review
3. Wait for user approval or edits
4. Only push to Linear after explicit confirmation
5. Set health to `onTrack` unless the user specifies otherwise
