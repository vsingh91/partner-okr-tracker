# ML H2 2026 — weekly refresh log

One entry per weekly refresh, newest first. This file is the raw material for the end-of-quarter retrospective: what moved, what shipped, what we flagged. Frozen dashboard copies live in [`archive/`](archive/index.html).

**How to update (every refresh):** copy `index.html` to `archive/YYYY-MM-DD.html`, add the row to `archive/index.html`, append the entry below, commit together with the refresh.

---

## Aug 20, 2026 (data: weeks Aug 3–9 and Aug 10–16)

**Completion 22.9%** (+3.7 vs Aug 7 refresh) · on pace, slightly behind (23.7% expected)

- **Cost is the story of the week:** $0.1825 per automated interaction, biggest drop since launch (−14.6%). Real spend-side efficiency (daily spend −17% at flat volume), timed with two cheaper-model tests going live. No initiative credited yet, both were A/Bs. Tail of the week rebounded to ~$0.174.
- **Latency improved a fourth straight week:** P75 12.93s support+sales, 13.65s SA, median 10.53s. Traces to the earlier shipped work (handover merge, QA-step removal). Queued upside: tool-omission prompt A/B conclusive, full-prod rollout in progress.
- **Quality guardrail easing but breached:** completed-week bad rate 17.9% (from 20.0%), first improvement in five completed weeks, ~3pt over baseline. Partial 15.8% read is merchant mix, not real. Watch: tone-of-voice complaints doubled (small sample). Reason shares switched to multi-select basis this week.
- **Shipped:** V3 Reasoning quality improvement (A/B winner live for all traffic Aug 18) · Intent & Spam model discovery (completed Aug 14; levers moving to implementation since wk Aug 17: input processing, deterministic no-reply rule, spam-model retraining plan).
- **Skill involvement 24.85%** (complete week), ~27% daily; merchant adoption best week since mid-July (35.3%). Skills quality flat at 86%, below launch level.
- **Support SR 33.57%** provisional (volume settling), band 32.6–35.0% since restatement. Now sourced from the digest's new Section 6.
- **SA:** conversion recovered to 14.47%; engagement 0.1187% genuinely declining (−3.4% over 3 weeks), the row is now slightly negative.
- **Model strategy consolidated:** Terra paused, both Gemini tracks out (3.7 Flash quality/latency, 3.5 Flash Lite chat latency despite −61% cost), all efforts on Luna, expanded to 50% of pre-GA (email+chat) Aug 20. Watch next week's cost and latency for the 50% effect.
- **Flags:** cost-source gap ($0.219 vs $0.233 for the Jul 27 week, under reconciliation) · intent workstream loses its committed engineer this week, handoff urgent · several Linear projects show Backlog/Paused while work is active.
- **Dashboard changes:** period labels on every metric · pinned levers on the cost card · archive mechanism added.

## Aug 7–8, 2026 (data: week Jul 27–Aug 2)

**Completion 19.2%** (recomputed after C&T refresh + SWAG review)

- **Support SR restated:** the 40.8% "target cleared" headline retracted; on the official billed/covered definition the series ran 31.9 → 33.5 and never approached 40%. The 40% EoH2 target needs re-anchoring at the next OKR review.
- **C&T skill involvement 24.4%** (Aug 7), up from 19.25%, driven by the Skills launch rollout, not ML in-flight work.
- **Cost $0.219** (volume-driven uptick) · latency re-sourced to the official dashboard: P75 13.46s combined, SA 14.54s.
- **Quality guardrail:** bad rate 20.0%, fourth consecutive worsening, ~5pt over baseline; wrong knowledge became the #1 reason. Cortex investigation launched Aug 9.
- **Dashboard rebuilt** to the story-first design (Aug 8): hero with pace verdict, what-moved recap, attribution rule (only shipped work gets metric credit), quality chart, metric cards.
- **SWAG review:** SA Engagement re-pointed to Tone of Voice, image recognition re-sized to 25, scope 225 pts.

## Jul 30, 2026 (data: week Jul 20–26)

**Completion ~15%** (old design)

- Support SR read 40.8%, clearing the 40% target — **later retracted** (Aug 7) as a definition mistake.
- Cost $0.213, latency P75 ~14.5s, quality guardrail worsening (~17.9% bad).
- SMS on V3 and scenario migration V2→V3 shipped in this period.
