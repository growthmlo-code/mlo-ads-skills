# Meta Creative Analyzer — Knowledge Base

Distilled, sourced expertise for grading Meta ad creatives by the numbers. Every threshold
cites its source inline. Full URL list at the bottom. Benchmarks are DTC/ecom-oriented and are
**flags, not laws** — always read a creative against the account's own baseline.

---

## 1. The three-stage creative funnel

Creative performance decomposes into three stages, each with its own metric family
([Motion](https://motionapp.com/blog/key-creative-performance-metrics)):

1. **Attention** — does the creative stop the scroll? → hook rate / thumb-stop.
2. **Engagement** — does it hold interest? → hold rate, avg watch time, completion rate.
3. **Action** — does it drive business results? → CTR, conversion rate, CPA, ROAS.

Diagnose by reading the stages in order: the first stage that falls below benchmark is the
bottleneck to fix ([Motion](https://motionapp.com/blog/key-creative-performance-metrics)).

---

## 2. Hook rate (a.k.a. thumb-stop rate)

**Definition:** the % of impressions that become 3-second video views — how well the first
frames stop the scroll
([Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide),
[Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/)).

**Formula:** `Hook Rate = (3-second video plays ÷ impressions) × 100`
([Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/),
[Triple Whale](https://www.triplewhale.com/blog/facebook-ad-analytics),
[Motion](https://motionapp.com/blog/key-creative-performance-metrics)).

"Thumb-stop rate" is the same metric (3-sec plays ÷ impressions) under a different name
([Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide),
[Motion](https://motionapp.com/blog/key-creative-performance-metrics)).

**Benchmarks (composite across sources):**

| Band | Hook rate | Source |
|---|---|---|
| Poor / rework the opening | **< 25%** | [Motion](https://motionapp.com/blog/key-creative-performance-metrics), [Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/) |
| Industry average | ~**24–25%** | [Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide), [Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/) |
| Solid / decent | **25–35%** | [Motion](https://motionapp.com/blog/key-creative-performance-metrics) |
| Good / scalable-quality opening | **> 30%** | [Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide), [Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/) |
| Strong / captures interest fast | **> 35%** | [Motion](https://motionapp.com/blog/key-creative-performance-metrics) |
| High-performing range | **40–50%** | [Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide) |
| Peak observed (specific placements) | up to **58%** | [Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide) |

Note: Triple Whale cites a wider "30–45%" typical range — placement, sound-on and platform
shift the numbers ([Triple Whale](https://www.triplewhale.com/blog/facebook-ad-analytics)). A
practical working target is **30–40%**, flag below 25%
([Motion](https://motionapp.com/blog/key-creative-performance-metrics)).

**Hook ↔ conversions:** there is a strong connection between high hook rates and conversion
rates — but hook does **not** always track CTR. Ads with strong hooks sometimes show lower CTR
yet superior conversions ([Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide)).
Practical rule: **use hook rate to kill obvious losers fast; use conversions/ROAS to decide
what to scale** — hook rate alone never justifies a scale.

---

## 3. Hold rate

**Definition:** the share of viewers who stay engaged past the hook — i.e. reach ~15 seconds or
complete the video ([Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/)).

**Two competing formulas exist — pick one and state it:**

- **A) thruplays (or 15-sec/complete) ÷ 3-second plays × 100** — "of the people you hooked, how
  many held?" ([Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/),
  [Motion](https://motionapp.com/blog/key-creative-performance-metrics),
  [Triple Whale](https://www.triplewhale.com/blog/facebook-ad-analytics) — Motion/TW use
  15-sec ÷ 3-sec).
- **B) thruplays ÷ impressions × 100** — hold as a share of all impressions (a stricter, smaller
  number). Some tools/dashboards use this.

The two give very different values, so the report must **label which denominator it used and
stay consistent**.

**Benchmarks (definition A / of-those-hooked):**

| Band | Hold rate | Source |
|---|---|---|
| Needs work | **< 30%** | [Motion](https://motionapp.com/blog/key-creative-performance-metrics) |
| Average | **40–50%** | [Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/), [Motion](https://motionapp.com/blog/key-creative-performance-metrics) |
| Strong | **> 50%** | [Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/) |
| Very strong | **> 60%** | [Motion](https://motionapp.com/blog/key-creative-performance-metrics) |

**Hook × hold diagnostic grid** ([Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/)):

- Low hook + low hold → weak opening **and** weak narrative → rebuild.
- High hook + low hold → strong opening, poor pacing/content after the first seconds → fix the body.
- High hook + high hold → strongest tier, scalable creative.

Why hold matters for money: two ads can share an identical 30% hook and still produce a **6x
ROAS gap** because one held 22% of viewers to the CTA and the other held 4%
([search synthesis, Glued/Billo 2025](https://www.glued.me/blog/hook-rate-vs-hold-rate-guide)).

---

## 4. Action-stage metrics (CTR, CPM, CPA, ROAS)

([Triple Whale](https://www.triplewhale.com/blog/facebook-ad-analytics),
[Motion](https://motionapp.com/blog/key-creative-performance-metrics))

- **CTR (link):** `clicks ÷ impressions × 100`. Meta average **0.9–1.5%**; **>1.5% strong**;
  ecom target **1.5–2.5%** ([Motion](https://motionapp.com/blog/key-creative-performance-metrics)).
  For traffic campaigns, CTR **below 1%** is a warning
  ([Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue)).
- **CPC:** `spend ÷ clicks` — traffic efficiency
  ([Triple Whale](https://www.triplewhale.com/blog/facebook-ad-analytics)).
- **CPM:** cost per 1,000 impressions — reach efficiency; also a fatigue signal (see §5)
  ([Triple Whale](https://www.triplewhale.com/blog/facebook-ad-analytics)).
- **CPA / cost-per-result:** `spend ÷ conversions` — judge vs. the brand's **target CPA**
  ([Triple Whale](https://www.triplewhale.com/blog/facebook-ad-analytics)).
- **ROAS:** `revenue ÷ spend`. Meta blended average **2.5–4.0** (varies with LTV/margin); scale
  only against the brand's **breakeven ROAS**
  ([Motion](https://motionapp.com/blog/key-creative-performance-metrics)). ROAS is "the most
  important metric" tying spend to results
  ([Triple Whale](https://www.triplewhale.com/blog/facebook-ad-analytics)).

---

## 5. Creative fatigue signals

Core pattern: **rising frequency + rising CPM + falling CTR over time = fatigue**
([Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue), search synthesis).
Any single signal can fire alone; the trio together is the strongest confirmation.

| Signal | Watch / flag | Act | Source |
|---|---|---|---|
| **Frequency (cold audiences)** | **> 2.5–3.0** raise a flag | **5+** = strong decline + more negative feedback | [Triple Whale](https://www.triplewhale.com/blog/creative-fatigue), [Triple Whale — analytics](https://www.triplewhale.com/blog/facebook-ad-analytics) |
| **CTR decline (WoW)** | drop of **10–15%** = watch | **20–30%** below baseline = fatigue zone; **40%+** = replace | [Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue) |
| **CPM inflation** | **> 18%** rise over 2 weeks = drift | **50–100%** jump while CTR flat = algorithmic penalty → refresh/kill | [Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue) |
| **Auto budget reallocation** | ad loses **> 20%** of budget share with no manual change | red flag — Meta is pulling delivery | [Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue) |
| **First-time impression ratio** | **< 50%** of daily impressions reaching new users (TOF) | audience saturation approaching | [Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue) |

**Evaluation window:** use a **7–10 day minimum** before fatigue calls; compare against a
**30-day baseline** ([Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue)).

**Fatigue decision tiers** ([Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue)):

| Tier | Trigger | Response |
|---|---|---|
| **Watch** | 10–15% decline on 1–2 metrics over 7 days | brief replacements; don't change spend yet |
| **Refresh (ITERATE)** | 20–30% decline on 2+ metrics over 7 days | modify **30–40%** of elements; cut spend **~50%** |
| **Replace (KILL)** | 40%+ CTR drop or doubled costs | pause immediately; extract the learning |

Pausing usually beats slow-bleeding a fatigued creative on reduced budget: it will just fatigue
slower while still delivering poor results (search synthesis,
[TheOptimizer](https://theoptimizer.io/blog/meta-ads-creative-fatigue-how-to-detect-it-early-and-what-to-do-about-it)).

---

## 6. Minimum volume before judging a creative

Do not grade a creative on noise. Reach minimum volume first
([Motion](https://motionapp.com/blog/key-creative-performance-metrics)):

- **≥ 2,000 impressions**, AND **50–100 clicks** OR **3–5 purchases**, over **3+ days**.

Fast kill triggers once past the gate
([Motion](https://motionapp.com/blog/key-creative-performance-metrics), search synthesis):

- **CTR < 50% of control/account average**, OR **CPA > 25% above target**, after **48–72 hours**.
- One bad day is nothing; **three consecutive bad days is a pattern** — evaluate on a rolling
  **3–5 day** window, not a single-day snapshot
  ([search synthesis / Coinis](https://coinis.com/blog/when-to-kill-meta-ads-decision-framework)).

---

## 7. SCALE / ITERATE / KILL logic

Combines the above into one verdict per creative.

- **SCALE** — clears the volume gate, ROAS ≥ target (or CPA ≤ target), healthy hook (>30%) and
  hold (>50% of-those-hooked), no fatigue signals. Raise budget **gradually**. Rationale: scale
  on conversions/ROAS, not on hook alone
  ([Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide),
  [Motion](https://motionapp.com/blog/key-creative-performance-metrics)).
- **ITERATE** — one fixable stage:
  - good hook, weak hold → new body / mid-section
    ([Vaizle](https://insights.vaizle.com/hook-rate-hold-rate/));
  - good engagement, weak CTR/offer → new CTA/offer/end-card
    ([Motion](https://motionapp.com/blog/key-creative-performance-metrics));
  - former top performer now fatiguing → refresh 30–40% of elements, cut spend ~50%
    ([Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue)).
- **KILL** — low hook + real spend, OR CPA/ROAS well off target past the gate, OR 40%+ CTR drop /
  doubled costs (terminal fatigue). Pause; extract the learning
  ([Motion](https://motionapp.com/blog/key-creative-performance-metrics),
  [Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue)).

**Volume is the system:** expect a ~**10% hit rate** on new concepts (e.g. ~14 losers, 4 average,
2 home runs per ~20-concept sprint). Killing losers fast is the point; one winner then expands
into many variations (format, hook, ICP) — hand the winners to `creative-strategy-analyzer`
(search synthesis, [Triple Whale — fatigue](https://www.triplewhale.com/blog/creative-fatigue)).

---

## 8. Data notes / gotchas

- **Static & image ads have no hook or hold rate** (no video plays) — grade on CTR + CPA/ROAS
  and mark hook/hold "—".
- **Hold rate denominator ambiguity** (§3) — the single biggest source of "our numbers don't
  match theirs." Always state the denominator.
- **Hook ≠ CTR ≠ ROAS.** They can diverge; a great hook with bad ROAS is a hook doing the wrong
  job ([Sovran](https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide)).
- **Platform/placement shift benchmarks.** TikTok hook rates run ~5–10 points above Meta on the
  same creative; sound-on lifts hook and Meta's auction favors sound-designed Reels (search
  synthesis, [Glued](https://www.glued.me/blog/hook-rate-vs-hold-rate-guide)). Keep Meta and
  TikTok benchmarks separate.

---

## Expert video used

- **Motion — Creative Analytics (YouTube channel):**
  <https://www.youtube.com/@MotionCreativeAnalytics> — Motion is the recognized creative-analytics
  authority in DTC paid social; its channel + blog define the hook/hold/thumb-stop framework and
  the attention→engagement→action funnel used throughout this skill. (A machine-readable
  transcript for a single video was not retrievable via fetch, so the companion Motion blog —
  [key-creative-performance-metrics](https://motionapp.com/blog/key-creative-performance-metrics)
  — is cited for the exact numbers, per the build template's substitution rule.) Complementary
  expert reference: **Charley Tichenor — Meta Ads Live Q&A**
  (<https://www.youtube.com/watch?v=HcP1ygR2DZM>), a recognized Meta buyer.

---

## Sources

- Vaizle — Hook Rate & Hold Rate: <https://insights.vaizle.com/hook-rate-hold-rate/>
- Sovran — Hook Rate for Meta Ads (Ultimate Guide): <https://sovran.ai/blog/hook-rate-for-meta-ads-ultimate-guide>
- Triple Whale — Facebook Ad Analytics: <https://www.triplewhale.com/blog/facebook-ad-analytics>
- Triple Whale — Creative Fatigue Framework: <https://www.triplewhale.com/blog/creative-fatigue>
- Motion — Key Creative Performance Metrics: <https://motionapp.com/blog/key-creative-performance-metrics>
- Motion — Creative Analytics (YouTube): <https://www.youtube.com/@MotionCreativeAnalytics>
- Glued.me — Hook Rate vs. Hold Rate guide: <https://www.glued.me/blog/hook-rate-vs-hold-rate-guide>
- TheOptimizer — Meta Ads Creative Fatigue: <https://theoptimizer.io/blog/meta-ads-creative-fatigue-how-to-detect-it-early-and-what-to-do-about-it>
- Coinis — When to Kill a Meta Ad (decision framework): <https://coinis.com/blog/when-to-kill-meta-ads-decision-framework>
- Charley Tichenor — Meta Ads Live Q&A (YouTube): <https://www.youtube.com/watch?v=HcP1ygR2DZM>
