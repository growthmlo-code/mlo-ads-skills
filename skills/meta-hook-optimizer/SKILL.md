---
name: meta-hook-optimizer
description: Diagnoses a weak hook (the first 3 seconds) on a Meta video or static ad and generates 5–10 stronger, testable opening-hook variants plus a structured test plan. Uses hook rate = thumb-stop rate (3-sec views ÷ impressions) to judge, targeting 25%+ (30%+ = winner). ALWAYS use this skill when the user asks to "mejora el hook", "hook optimizer", "dame hooks para [producto]", "variantes de gancho", "el primer segundo no funciona", "el gancho no engancha", "thumb-stop bajo / hook rate bajo", "improve the hook", "give me hooks for [product]", "my first 3 seconds aren't working", "scroll-stopper", "pattern interrupt", or wants opening-line/first-frame ideas for a Meta ad. Fires on casual asks in ES or EN about fixing or generating ad hooks/openers.
---

# Meta Hook Optimizer

## What it does
Takes an ad script/concept (and its current hook-rate metrics if available), diagnoses why the
first 3 seconds are underperforming, and produces **5–10 testable opening-hook variants** across
different psychological archetypes plus a **structured hook test plan** (what to hold constant,
what to vary, how to read the winner). Optimizes the opener only — the part that earns the rest of
the view. Works for ES or EN DTC brands; hooks are written in the brand's market language.

## When to use
- The user wants stronger openers: "dame hooks para [producto]", "give me hooks for [product]",
  "variantes de gancho", "mejora el hook".
- A hook is underperforming: "el primer segundo no funciona", "my first 3 seconds aren't working",
  "thumb-stop bajo", "hook rate bajo", "el gancho no engancha", "scroll-stopper".
- The user asks for pattern-interrupt / first-frame / opening-line ideas for a Meta video or static.
- Follows naturally after `meta-creative-analyzer` flags a low 3-sec view rate.

## Inputs needed
Ask for whatever is missing:
1. **The ad script or concept** (or at least the product + core promise + who it's for / ICP).
2. **Current hook-rate metrics** if diagnosing an existing ad: 3-sec views, impressions (or the
   hook rate %). If unavailable, proceed in generation mode.
3. **Format**: video or static (static has no 3-sec view — judge by CTR instead).
4. **Market language** (ES / EN) and any brand voice / claims constraints.
5. **Funnel stage** of the placement (cold vs retargeting) — changes which archetypes to favor.

## Data sources
- **The script/concept** — from the user.
- **Current hook-rate metrics** — from the `meta-creative-analyzer` skill, or pull 3-sec video
  views and impressions directly from Meta Ads via the `ads_*` Meta Marketing MCP (or Windsor.ai
  `facebook` connector). Hook rate = 3-sec views ÷ impressions.
- **Winning-hook intel (optional)** — Atria via Chrome: extract opening lines from the brand's or
  competitors' top creatives to ground variants in proven angles (see `meta-creative-analyzer`).
- Be honest: if metrics aren't connected, say so and run in generation-only mode.

## Method
1. **Frame the job.** Confirm you're fixing the **hook (first 3s)**, not the body/offer. Get the
   script, product, ICP, promise, format, funnel stage, and language.
2. **Diagnose (if metrics exist).** Compute hook rate = 3-sec views ÷ impressions × 100.
   - ≤20% → hook is the bottleneck (proceed).
   - ≥25% but weak CTR/conversions → it's a **hold/body/offer** problem, not the hook; say so and
     stop, or redirect.
   Then watch/read the first frame on mute and check: does it look different from organic feed? is
   the payoff in second 1? does it name the pain/ICP? are there sound-off captions? (Full checklist
   in the knowledge base §3.)
3. **Pull proven angles (optional).** If Atria is available, extract winning opening lines for the
   brand/competitors to seed the variants.
4. **Generate 5–10 hook variants.** Spread them across archetypes (question/pain call-out, bold
   claim/myth-bust, negativity/mistake, curiosity gap, social proof/UGC, before/after,
   founder/origin, number/stat, price shock, callout-to-ICP, FOMO/offer). Each variant must:
   pattern-interrupt frame 0, state the promise in second 1, be one idea, work sound-off (≤~7 words
   on screen), and favor cold-traffic archetypes for cold placements / offer archetypes for
   retargeting. For each variant give the **spoken/text line + the first-frame visual + the on-screen
   caption + which archetype**.
5. **Write the test plan.** Hold the body and offer **constant**; vary **only** the first 3s across
   the variants; ship them as separate ads in the concept; define the win read (kill on hook rate,
   scale on conversions); set the sample-size floor and refresh cadence.
6. **Deliver** the variants table + test plan (see Output).

## Rules & thresholds
- **Hook rate = thumb-stop rate = 3-sec video views ÷ impressions × 100.** They are the same metric.
- **Benchmarks:** ≤15% = mandatory rework; ~20–24% = platform median; **25% = pass line**;
  **30–35%+ = winner / best-in-class**; optimized campaigns reach 30–50%. If <25%, fix the first 3s
  before touching anything else.
- **First 1.5 seconds** is where the strongest Reels hooks land; ~65% of viewers drop in the first
  3s without a strong hook.
- **Sound-off is default** (~85% watch muted): every hook needs large high-contrast on-screen text,
  ≤~7 words.
- **Ship 5–10 variants per concept (min 3),** each from a different archetype.
- **Change ONE variable — the opener.** Keep body + offer identical so hook rate attributes the win.
- **Kill on hook rate, scale on conversions.** A 10-point thumb-stop lift ≈ doubles effective reach.
- **Refresh hooks weekly–biweekly** on high-spend accounts (fatigue hits the opener first).
- **Static ads** have no 3-sec view → judge the first frame by CTR / outbound CTR, not hook rate.
- All numbers are sourced in `reference/knowledge-base.md`.

## Output
Two deliverables in the chat (offer to also drop them into the brand's Notion or a Slack draft):

**A) Diagnosis (if metrics given)** — one line: current hook rate, band, and the verdict
(hook problem vs hold problem) with the 1–2 biggest first-frame issues.

**B) Hook variants table** (5–10 rows):

| # | Archetype | Hook line (spoken/text) | First-frame visual | On-screen caption (≤7 words) |
|---|-----------|--------------------------|--------------------|------------------------------|
| 1 | Pain call-out | "Still waking up tired after 8 hours?" | Face, eyes closing, mid-yawn | STILL TIRED AT 8HRS? |
| 2 | Price shock | "$8 replaced my $80 serum." | Two bottles slammed side by side | $8 vs $80 |
| … | … | … | … | … |

**C) Test plan** — constants (body + offer held fixed), the variable (first 3s only), number of
variants shipped, win read ("kill below ~25% hook rate; scale variants with best CTR→CPA/ROAS"),
sample-size floor, and refresh cadence.

## Guardrails
- Never claim a metric you didn't measure — if hook rate isn't available, say so and run in
  generation-only mode.
- Don't rewrite the offer or body; this skill only touches the opener. If the real problem is
  hold/offer, name that and stop rather than generating hooks that can't fix it.
- Respect brand voice, approved claims, and regulated-category limits (supplements, health). Don't
  invent studies, stats, or "3 out of 4" numbers the brand can't substantiate.
- Keep hooks in the brand's market language (ES vs EN); don't translate a Spanish brand's hooks to
  English by default.
- Don't bulk-create ads in Meta from this skill's output without showing the variants and getting
  explicit confirmation; respect account currency/locale.

## References
See `reference/knowledge-base.md` for the sourced benchmarks, formulas, hook archetype library,
first-3-second principles, the full testing protocol, and the expert YouTube source.
