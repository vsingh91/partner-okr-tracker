# ML H2 2026 — weekly refresh log

One entry per weekly refresh, newest first. This file is the raw material for the end-of-quarter retrospective: what moved, what shipped, what we flagged. Frozen dashboard copies live in [`archive/`](archive/index.html).

**How to update (every refresh):** copy `index.html` to `archive/YYYY-MM-DD.html`, add the row to `archive/index.html`, append the entry below, commit together with the refresh.

---

## Sep 10, 2026 (data: week Aug 24–30 complete for Skills and cost · quality week Aug 30–Sep 5 · latency and SA reads partial Sep 6–9)

**Completion 32.3%** (+1.5 pts since Sep 3; page chip +3.2 by its prior-entry arithmetic)

- **Shipped:** persisted-Skills reasoning (Released in Linear Sep 10; online QA 11/12 validated, offline eval 1/60 tickets with persistence-damaged reasoning). Shopping Assistant pre-fetch released to all merchants inside the SA latency initiative (−3.75s on the first turn, −23.5%; cost −21.7%; success rate stable). Neither credited yet.
- **Luna on email is measurable:** test cohorts (email, contact form, help center; Aug 27–Sep 6) read $0.036 vs $0.172 per automated interaction (−79%), success rate +1.3 pts, handover −2.8 pts, both significant; full email rollout ≈ −36% blended (Cortex estimate). Merchant feedback −2.8 pts is the gate: failure review says not handing over (39%), knowledge adherence (27%), unsupported claims (23%), wrong action (11%). Release order: Order / Promotion & Discount / Marketing / Account / Feedback (≈45% of traffic) → Product / Return / Shipping / Subscription / Exchange → Warranty / Wholesale. Other intent alone: shopper CSAT lower on Luna (3.6 vs 4.0), merchant feedback and handover better, success rate unreadable until billing settles. Other ≈ 5% of email tickets, ≈ 2–2.5% of all traffic.
- **Chat model:** Luna and Terra both out for chat (Terra on the SA prompt: −0.16s only, success rate −2.5 pts, cost −13%). Chat runs on OpenAI's priority tier (~$0.10 per automated chat interaction for ~1s); A/B on the default tier Sep 8–18. Flex tier proposed for email. Post-training narrowed to one open-weight target model, three questions due end of September; Sep 10 read: still trails Luna, recommendation on the table is to pause for Q4.
- **Skills:** usage 30.5% (wk Aug 24–30, +2.5 pts; 28.0% the week before), merchant adoption 50.8% (+4.2 pts), skill-ticket success rate 36.5% (plateau since early July, ~55% at launch), skill merchant quality 86.4% flat. Order-status/tracking Skills the systemic weak spot across merchants; subscription-cancellation and returns Skills strong. Median skill-merchant combo 32.4%, IQR 18–51%.
- **Cost:** digest cost skill now reads within $0.01 of the paying-accounts view on overlapping weeks ($0.146 / $0.187 for the Aug 10 / Aug 17 weeks vs $0.15 / $0.18 logged), so its Aug 24–30 read ($0.174) is logged as $0.17; Aug 31 week $0.182 provisional (5-day lag, not logged). Four-week range $0.15–0.19, flat. ⚠️ SA-scope cost per interaction +15% over three weeks ($0.212 → $0.243), steady drift; coincides with shopper confirmation round two (+6.5%/ticket) and Skills added to the SA prompt, against the pre-fetch release (−21.7%); probe open.
- **Latency (partial Sep 6–9):** support+sales P75 12.57s / P50 10.16s (296k turns), ~0.5s above the Aug 16–22 best, −13% / −15% vs the July peak, turn volume ~8× since June; the digest gave no settled value for the Aug 30–Sep 5 week (P50 "~10.2–10.5s" for the last three weeks). SA P75 13.06s / P50 10.36s / P90 15.82s partial; Aug 16–22 restated 12.62s (from 12.53). Helpdesk webhook queue spike Sep 1 (slowest message 8+ min; chat cancels at 55s) flagged as BFCM risk.
- **Quality guardrail:** rolling bad rate 16.7% third week (Aug 30–Sep 5), quality 83.3% vs 85.0% baseline. Raw weekly bad rate 9.2% → 10.6% (peak 11.9% on Sep 2, 9.4% by Sep 5). Reasons back on the multi-select basis (sum >100%): wrong knowledge 26.8, missing 25.1, ignored 22.6, should hand over sooner 19.3; action-not-performed −4.1 pts (real improvement). No reason rising.
- **Support SR:** no weekly section again; August monthly 34.4% stands.
- **SA:** conversion held 13–15% through the week of Aug 24 (no exact value), partial Sep 6 week 12.8% and ERPV $14.95 (understated). No conversation-rate value in the digest. Investigation: ~13,300 tickets/week of genuine missed hand-offs from the Default Agent to SA (Skills precedence over the transfer rule; promotion and product-availability intents; 2.7× more on email); prompt fix validated, unpublished; decisions pending. Shopper confirmation round two (since Aug 28): proposal 18.4% (+5.2), handover −1.6, close +1.6, cost +6.5%/ticket; gain held after removing confounds, moving to release.
- **Linear:** tone of voice In Rollout Sep 7 (beta 134 merchants, target Sep 14) · shopper confirmation target Sep 14 · discovery triggers In Discovery (partner POC mostly built; ML draft PR untested, deprioritized) · product reviews partner ETA Sep 18, ML side Backlog · intent detection, LLM stack review (start Sep 17), image recognition (start Sep 21) Backlog · Skills framework Paused · Gemini 3.8 flash (target Sep 11) and Gemini 2.5 deprecation (target Sep 24) projects created, both Backlog. Intent/spam preprocessing A/B ready for prod (target Sep 10); spam retrain ~Sep 16.
- **Open flags:** SA cost drift · SA success-rate decline · Luna merchant feedback · settled Aug 30 latency week missing from the digest · no weekly SR cut for four weeks · 40% SR target re-anchoring · SA conversion target still TBD · guardrail probe still open.

## Sep 3, 2026 (data: weeks Aug 17–23 and Aug 24–30 · August month-close)

**Completion 30.8%** (+7.9 pts since Aug 20; page's own WoW chip says +6.0 by its prior-entry arithmetic)

- **Latency was August's win, now giving some back:** best week on record Aug 16–22 (P75 12.00s support+sales, median 9.66s, SA P75 12.53s, SA fastest quarter of turns 5.7s). Partial Aug 30 week rebounds to 13.10s / 10.66s / SA 13.63s. Likely cause: Luna at 50% of pre-GA chat from Aug 20 (1.5–2s slower); Luna pulled from chat Sep 1.
- **Cost series RESTATED (Sep 3, same day, Varun's call)** onto the official dashboard's Per Ticket logic (LLM cost ÷ billed automated interactions, paying current-subscriber accounts, AI Journey excluded, last 7 days dropped). Measured on the new view: $0.19 / $0.15 / $0.18 for weeks Aug 3 / 10 / 17; $0.17 over the past 30 days (chat $0.20, email $0.14, contact form/help center $0.16; email group $0.15, already at the Q3 checkpoint). Old cut ran $0.024–0.036 higher. Points before Aug 3 and the ~$0.23 baseline are ESTIMATED (old reading −$0.03) until a Cortex weekly pull on the new view replaces them; Aug 24–30 pending. Original Sep 3 note on the old cut follows.
- **Cost (old cut): the $0.18 dip did not hold.** Aug 17–23 settled at $0.2158 (first read on Aug 27 was $0.274, lagged denominator); Aug 24–30 first read $0.2358, expected to settle down. August ran ~$0.21–0.24, flat vs July. Like-for-like channel check (Cortex, Sep 3): the dip was CHAT ONLY (chat $0.23 → $0.14 → $0.23 for weeks Aug 3/10/17 at flat volume; email $0.14–0.15 and contact form $0.15–0.17 flat), so the flash-lite test (email-only) is ruled out as the cause; cause unknown, probe open. Paying-accounts view reads $0.19 / $0.15 / $0.18 for the same weeks, ~$0.03 below the series with the same shape; series stays on the broader definition. Digest runs restate the same week by $0.01–0.06 in either direction; series is read on settled weeks.
- **Model decision landed:** benchmark completed Aug 21; Aug 28 recommendation approved (Luna on email for winning intents, est. −22% → ~$0.16; Terra optimized for chat; GPT-5.4 retired later). First Luna intent (`Other`) live on email since Sep 1; intent-by-intent expansion decided Sep 7. Cortex estimate $0.21 → $0.15 selective, $0.12 full. Luna latency work paused; Terra (−0.69s P75, −9.3% cost in A/B) + open-weight fine-tuned candidates are the chat path.
- **Shipped:** qualify step on GPT-5.4-nano, Aug 24 (A/B −89% qualify cost, −8.9% per-ticket LLM cost, +4.5pp success rate, quality/latency flat). Not yet credited on the cost row.
- **Quality guardrail:** bad rate 16.7% on both completed weeks (Aug 16–22, Aug 23–29), from 20.0% at the start of August; quality rate 83.3% vs 85.0% baseline; raw weekly bad rate 9.3%, flat. Reason mix now share of mentions (basis changed again, not comparable to Aug 20): wrong knowledge 18.8% (−1.8), ignored 15.8%, missing 14.1% (+1.8, fastest riser); sample review says stale content is the main theme. Tone-of-voice spike did not persist. Aug 27 digest run read the same period at ~7.8% on half the merchants; treated as a bad run.
- **Support SR 34.4% for August** on the official monthly card (Jul 33.1, up every month since Jan 23.3). Digest carried no weekly SR section this period; weekly cuts Aug 16–29 pending. Overall AI Agent SR 39.1%, SA 50.7% (from 53.4% in July).
- **Skills:** usage 26.6% (wk Aug 10–16), merchant adoption 40.0%, skill-ticket success rate 37.0% (plateau), skill merchant quality 85.7%. Order-status/tracking/cancellation skills underperform as a class; subscription-cancellation skills strongest.
- **SA:** conversation rate 0.129% rolling 28d to Sep 2 (up 6% over 3 weeks, first rise since July); conversion 14.29% wk Aug 17–23, partial Aug 31 week 12.97%; SA success rate 49.5% on complete 28-day windows (from 52.0%).
- **Linear hygiene flags:** intent detection, LLM stack review, image recognition still Backlog; Skills framework iteration (started Aug 25) and persisted Skills show Paused; tone of voice In Progress since Aug 28 with its Aug 25 target passed; shopper confirmation target moved to Sep 14; quiz-to-skill target Sep 23.
- **Open flags:** cost source instability (run-to-run restatements) on top of the Jul 27 reconciliation · SA success rate decline (real, 3 complete windows) · late-August latency rebound attribution to Luna is likely, not proven · Skills-row weekly reading not refreshed past Aug 16 (digest gave no newer weekly usage figure).

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
