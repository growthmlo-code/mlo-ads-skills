---
name: meta-creative-analyzer
description: >
  Analyzes Meta ad creative PERFORMANCE using the numbers — hook rate, hold rate,
  thumb-stop, CTR, spend efficiency, CPA/ROAS, frequency, CPM and fatigue signals — pulled
  at the ad/creative level, then ranks every creative into SCALE / ITERATE / KILL with a
  one-line why and a benchmarks table. This is the QUANTITATIVE sibling of
  creative-strategy-analyzer (which reads Atria for strategic angles/hooks): this skill is
  metric- and threshold-driven. ALWAYS use this skill when the user asks (ES or EN):
  "analiza mis creativos por métricas", "hook rate de [marca]", "qué creativo escalo",
  "cuáles mato", "thumb stop", "hold rate", "creative performance", "cuál está fatigado",
  "por qué cae el CTR de este creativo", "ranking de creativos de X", "analyze my creatives
  by metrics", "which creative do I scale", "which ones do I kill", "creative fatigue on
  [brand]". Trigger on partial/casual asks too (e.g. "sácame el hook rate de los ads de X",
  "cuál anuncio está muerto").
---

# Meta Creative Analyzer (metrics)

## What it does
Pulls ad/creative-level insights from Meta, computes the creative diagnostic metrics
(hook rate, hold rate, thumb-stop, CTR, CPM, frequency, spend, CPA/ROAS), compares each
creative against benchmarks, and returns a ranked table where every creative gets a verdict
— **SCALE**, **ITERATE**, or **KILL** — plus a one-line reason. It kills obvious losers fast
on hook rate + spend, and reserves SCALE for creatives that also win on conversions/ROAS.

## This vs. creative-strategy-analyzer
MLO already has `creative-strategy-analyzer` — that one navigates **Atria** to extract
winning **angles, hooks, USPs, ICPs** (the qualitative/strategic view). **This** skill is the
**quantitative sibling**: it works from raw Meta numbers to grade and rank creatives by
performance. Use them together — this one tells you *what* to scale/kill; the strategy
analyzer tells you *why* it worked and what to build next.

## When to use
- The user wants creatives graded/ranked by performance and a scale/iterate/kill call.
  - ES: "analiza mis creativos por métricas", "qué creativo escalo", "cuáles mato", "hook rate de [marca]", "cuál está fatigado".
  - EN: "analyze my creatives by metrics", "which creative do I scale / kill", "hook rate for [brand]", "creative fatigue".
- Deciding where to push budget (SCALE) vs. what to refresh (ITERATE) vs. what to pause (KILL).
- Spend is up but results are flat and you suspect specific creatives are dragging or fatiguing.
- Weekly creative review / before a new creative batch, to see what's working.

## Inputs needed
Ask for whatever is missing:
- Brand name and which Meta ad account (or let `ads_get_ad_accounts` list them).
- Scope: whole account, one campaign, or one ad set. Default: all active ads in the account.
- Reporting window. Default **last 7 days**; use **14–30 days** for low-volume accounts so
  each creative clears the minimum-volume gate (see Rules).
- The success metric + target: **ROAS** (ecom, needs purchase conversion tracking) or **CPA**,
  and the target number. Ask for account currency/locale.
- Whether these are prospecting (cold) or retargeting ads — fatigue thresholds differ.

## Data sources
- **Meta Ads** via the `ads_*` Meta Marketing MCP (primary): pull ad/creative-level insights —
  `impressions`, `video_3_sec_watched` / 3-second video plays, `thruplays` (and 15-sec /
  video-complete views if available), `inline_link_clicks` + `ctr`, `spend`, `frequency`,
  `cpm`, and purchase conversions / `purchase_roas` / cost-per-result. Break down **by ad**
  (`level=ad`) with the creative name/thumbnail so each row maps to one creative.
- **Windsor.ai `facebook`** connector as an alternative source for the same ad-level fields if
  the Meta MCP isn't connected for that account.
- **Atria (Chrome)** — optional supplement: if connected, pull the qualitative read (angle,
  hook type, format) to annotate each ranked creative, or hand off to
  `creative-strategy-analyzer`. Not required for the numeric ranking.
- Be honest about gaps: hook/hold rely on video metrics — **image/static ads have no hook or
  hold rate**, judge those on CTR + CPA/ROAS only. If purchase conversions aren't tracked in
  the account, ROAS is unavailable; fall back to CTR + cost-per-result and say so.

## Method
Do these in order.

1. **Scope & pull.** Confirm account, scope, window, success metric + target, currency, and
   cold-vs-retargeting. Pull ad-level insights for every ad in scope with: impressions,
   3-sec video plays, thruplays (and 15-sec/complete if present), link clicks, CTR, spend,
   frequency, CPM, purchases, ROAS/CPA. One row per creative.
2. **Volume gate.** Drop (or mark "not enough data") any creative below the minimum-volume
   threshold — you cannot grade a creative on noise. See Rules for the exact gate.
3. **Compute the diagnostic metrics** per creative:
   - Hook rate = 3-sec video plays ÷ impressions.
   - Hold rate = thruplays (or 15-sec/complete) ÷ impressions. **State which denominator you
     used** — some tools define hold as thruplays ÷ 3-sec plays; pick one and be consistent.
   - Thumb-stop = same as hook rate (3-sec ÷ impressions); report once, label clearly.
   - CTR (link), CPM, frequency, spend, CPA/ROAS — as pulled.
4. **Diagnose the funnel per creative** (attention → engagement → action):
   - Low hook → the opening 3 seconds fail; the scroll never stops.
   - Good hook + low hold → strong opening, weak body/pacing; the story loses them.
   - Good hook + good hold + weak CTR/ROAS → engaging but not persuasive/relevant; offer or CTA problem.
   - Good on all → winner.
5. **Check fatigue** for creatives with meaningful spend over the window: rising **frequency**,
   rising **CPM**, and falling **CTR** together = fatigue. Compare current vs. the trailing
   baseline (see Rules). Flag which fatigue signal(s) fired.
6. **Assign the verdict** per creative using the decision logic in Rules:
   **SCALE** (winner, push budget), **ITERATE** (fixable — refresh the weak stage), or
   **KILL** (loser or terminally fatigued; pause).
7. **Rank & report.** Sort by the success metric (ROAS/CPA) within verdict, SCALE first.
   Build the ranked table + benchmarks table (Output). Add 1–2 lines of account-level read
   (e.g. "3 of 9 creatives carry 80% of profitable spend; hook rates are healthy but hold is
   the bottleneck").

## Rules & thresholds
Benchmarks are DTC/ecom-oriented; treat as flags, not laws — always read against the
account's own baseline. Numbers sourced in `reference/knowledge-base.md`.

- **Minimum volume before judging a creative:** ~**2,000+ impressions** AND (**50–100 clicks**
  OR **3–5 purchases**), over **3+ days**. Below this = "not enough data", do not rank.
- **Hook rate (3-sec ÷ impressions):** <25% weak · 25–35% solid · **>35% strong** · >30% = a
  scalable-quality opening. Use a low hook + real spend to KILL losers fast.
- **Hold rate (thruplays or 15-sec ÷ impressions):** ~40–50% average · **>50–60% strong** ·
  <30% weak. (If you instead use thruplays ÷ 3-sec plays, the "good" band is higher — label it.)
- **Link CTR:** Meta average ~0.9–1.5%; **>1.5% strong**; ecom target **1.5–2.5%**.
- **ROAS:** Meta blended average ~2.5–4.0 (varies by LTV/margin); scale only vs. the brand's
  breakeven ROAS. **CPA:** judge vs. the brand's target CPA.
- **Frequency (fatigue):** prospecting/cold flag at **>2.5–3.0**; **5+** = strong decline + more
  negative feedback.
- **CTR decline (fatigue):** week-over-week drop of **10–15%** = watch; **20–30%** below
  baseline = fatigue zone; **40%+** drop = replace/pause.
- **CPM inflation (fatigue):** **>18%** rise over two weeks is meaningful drift; a **50–100%**
  CPM jump while CTR is flat = the ad is being penalized → refresh/kill.
- **Kill triggers (fast):** CTR < 50% of the control/account average, OR CPA > 25% above target,
  after **48–72 hours** of delivery past the volume gate.
- **Decision logic:**
  - **SCALE** = clears volume gate + ROAS ≥ target (or CPA ≤ target) + healthy hook/hold + no
    fatigue. Raise budget gradually.
  - **ITERATE** = one fixable stage (e.g. good hook, weak hold → new body; good engagement, weak
    CTR → new CTA/offer), OR a former top performer now fatiguing (refresh 30–40% of elements,
    cut spend ~50%).
  - **KILL** = low hook + real spend, OR CPA/ROAS well off target past the gate, OR 40%+ CTR
    drop / doubled costs (terminal fatigue). Pause; extract the learning.

## Output
A single response with two tables + a short read. Default to the user's language (ES/EN).

**1) Ranked creative table** (SCALE first, then ITERATE, then KILL; sorted by ROAS/CPA within each):

| Creative | Hook % | Hold % | CTR % | Spend | ROAS (or CPA) | Freq | Verdict | Why (one line) |
|---|---|---|---|---|---|---|---|---|
| Testimonial_v3 | 38% | 55% | 2.1% | $1,240 | 4.8 | 1.9 | **SCALE** | Wins on all stages, no fatigue — push budget |
| UGC_hook_A | 34% | 28% | 1.6% | $610 | 2.1 | 2.2 | **ITERATE** | Great hook, hold collapses — new body/mid-section |
| Static_promo | — | — | 0.7% | $430 | 0.9 | 3.4 | **KILL** | Below-target ROAS + weak CTR + fatiguing — pause |

**2) Benchmarks table** — the thresholds used (hook, hold, CTR, ROAS/CPA, frequency, fatigue),
so the verdicts are auditable.

**3) Read (2–4 lines):** where the profitable spend concentrates, the account-level bottleneck
(hook vs. hold vs. CTR vs. offer), and the top next action. Optionally hand off to
`creative-strategy-analyzer` for the strategic "why" and next-batch angles.

## Guardrails
- **Static/image ads have no hook or hold rate** — never invent one; grade them on CTR + CPA/ROAS
  and mark hook/hold as "—".
- **Respect the volume gate.** A 45% hook rate on 300 impressions is noise, not a winner. Never
  rank a creative that hasn't cleared the gate.
- **Define hold rate's denominator explicitly** and keep it consistent across the whole report —
  the two common definitions give very different numbers.
- **Hook rate alone never justifies SCALE.** Scale on conversions/ROAS; use hook rate to *kill*
  fast, not to promote. A high hook with bad ROAS is a hook doing the wrong job.
- **Don't confuse a fatiguing winner with a loser.** A former top creative with rising freq/CPM
  and falling CTR is ITERATE (refresh), not necessarily KILL.
- **Respect account currency/locale** in every money figure; write numbers in the user's locale
  (ES uses comma decimals).
- This skill **reads and recommends** — it does not pause, scale, or edit ads. Present the ranked
  verdicts and let the user apply changes (or confirm before any write action).

## References
See `reference/knowledge-base.md` for every benchmark, formula, and fatigue threshold with
its source URL (Vaizle, Sovran, Triple Whale, Motion, plus an expert video).
