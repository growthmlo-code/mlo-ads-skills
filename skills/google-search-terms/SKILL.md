---
name: google-search-terms
description: >
  Mines a Google Ads Search Terms Report to surface three things at once: (1) new keyword
  opportunities to ADD, (2) intent/theme clusters, and (3) wasteful terms to flag for
  negation. Runs word-level n-gram analysis, segments every term into convert / brand /
  competitor / high-cost-no-conv / irrelevant, and outputs an action table (ADD as keyword
  / NEGATE / MONITOR / IGNORE) plus an n-gram insight summary. This is the ANALYSIS engine;
  the actual exclusion action lives in the `google-negative-keywords` skill. ALWAYS use this
  skill when the user says any of: "analiza los search terms", "search terms report",
  "qué búsquedas están convirtiendo", "oportunidades de keywords", "n-gram analysis de
  [marca]", "mina los términos de búsqueda", "qué keywords añadir", "analyze search terms",
  "what searches are converting", "keyword opportunities", "mine the search query report",
  or asks which Google Ads searches to turn into keywords or which are wasting spend.
---

# Google Search Terms Miner (n-gram analysis engine)

## What it does
Pulls a brand's Google Ads Search Terms Report over a rolling window, runs 1/2/3-word
n-gram analysis to find which *tokens* win and which waste money, then classifies every
search term into an action: promote to an exact-match keyword, flag for negation, monitor,
or ignore. It also clusters terms by intent/theme so you see the shape of demand, not just a
flat list. Output is an auditable action table plus a short n-gram insight summary you can
paste into a report or hand to the media buyer.

## When to use
- User wants to find new keywords to add: "oportunidades de keywords de [marca]",
  "qué keywords añadir en Google", "keyword opportunities".
- User wants to know what's converting: "qué búsquedas están convirtiendo",
  "what searches are converting", "mina los términos de búsqueda".
- User asks for n-gram / word-level analysis: "n-gram analysis de [marca]",
  "analiza los search terms", "search terms report de [marca]".
- User suspects wasted spend but wants the diagnosis first (the negation *action* then
  hands off to `google-negative-keywords`).

## Inputs needed
Ask if missing:
- **Brand / Google Ads account** (which account or MCC child; confirm account currency + locale).
- **Date window** — default 30 days; use 60–90 days if the account is low-volume so terms
  reach statistical significance. State the window you used.
- **Target CPA and/or target ROAS** (or breakeven ROAS) — needed to judge "converting" vs
  "wasteful". If unknown, pull from the brand brief / KPI panel or ask.
- **Campaign scope** — all campaigns, or one (e.g. only Search, only PMax search themes).
- Optional: **brand terms + known competitors** so brand/competitor buckets are accurate.

## Data sources
- **Google Ads Search Terms Report** — via the Windsor.ai connector `google_ads`
  (`mcp__...__get_data` with the google_ads source) or a Google Ads MCP if connected.
  Fields required per search term: search term, cost, clicks, impressions, conversions,
  conversion value (revenue), and — if available — the matched keyword and campaign/ad group.
  If the connector cannot return the matched-keyword column, say so; you can still analyze
  by term but keyword-level promotion decisions get weaker.
- **Brand brief / KPI panel (Notion)** — for target CPA / target or breakeven ROAS if the
  user doesn't give it.
- Be honest: Search Terms data that Google withholds ("Other search terms") is NOT in the
  report; you can only analyze visible terms. Note the visible-vs-total spend gap if large.

## Method
1. **Confirm scope**: brand/account, date window (default 30d; 60–90d if low volume),
   target CPA/ROAS, currency/locale. Pull brand + competitor term lists if available.
2. **Pull the report**: get every visible search term with cost, clicks, impressions,
   conversions, conv value, and matched keyword. Normalize to the account currency.
3. **Term-level segmentation** — bucket EVERY term into exactly one of:
   - **CONVERT** — has conversions AND CPA ≤ target (or ROAS ≥ target/breakeven).
   - **BRAND** — contains the brand's own name/variants (report separately; usually keep).
   - **COMPETITOR** — contains a competitor brand name.
   - **HIGH-COST-NO-CONV** — cost ≥ threshold AND conversions = 0 (waste candidate).
   - **IRRELEVANT** — intent clearly unrelated to what the brand sells (jobs, free, DIY,
     wrong product, wrong geo), regardless of cost.
   - **MONITOR** — has clicks/spend but below significance thresholds; not yet decidable.
4. **N-gram analysis** — tokenize every search term into 1-word, 2-word, and 3-word grams.
   Aggregate cost, clicks, conversions, conv value per gram (a term feeds every gram it
   contains). Then:
   - **Winning tokens**: grams with conversions and CPA ≤ target / ROAS ≥ target. These are
     your ADD candidates — 3-word (and longer) grams usually make the best new keywords.
   - **Wasteful tokens**: grams with cost above threshold and 0 conversions. 1- and 2-word
     grams here are the best broad/phrase negatives (one gram can replace hundreds of
     exact negatives) — hand these to `google-negative-keywords`.
5. **Cluster by intent/theme** — group terms/grams into 3–7 named clusters (e.g.
   "material X", "problem/solution", "gift", "comparison", "location", "price"). Note which
   clusters convert and which burn budget. This is the strategic read.
6. **Assign the recommended action** to each notable term (see Rules for the exact gates):
   - **ADD as keyword** — CONVERT term, statistically meaningful → promote to exact match.
   - **NEGATE** — HIGH-COST-NO-CONV or IRRELEVANT → flag for `google-negative-keywords`
     (this skill does NOT create the negatives; it hands off).
   - **MONITOR** — below significance; revisit next window.
   - **IGNORE** — trivial spend, one-off, or already covered as a keyword.
7. **Write the output**: the action table (top terms + all ADD/NEGATE picks), the n-gram
   winners/wasters lists, the intent clusters, and a 3–5 line insight summary.
8. **Hand off**: for every NEGATE row, tell the user to run `google-negative-keywords` to
   choose match type, level (ad group vs campaign vs list), and apply with a preview.

## Rules & thresholds
- **Default window 30 days; extend to 60–90 days** for low-volume accounts so terms reach
  significance. Never negate on assumption alone — require data ([Optmyzr](https://www.optmyzr.com/blog/negative-keywords/)).
- **Promote-to-keyword gate**: promote a converting search term to its own **exact-match**
  keyword when it has a repeatable conversion signal (≈ **2+ conversions** in-window) AND
  CPA ≤ target (or ROAS ≥ target/breakeven). Exact match raises Quality Score and relevance,
  and gives the winner dedicated bidding ([WordStream](https://www.wordstream.com/blog/ws/2010/11/10/advanced-search-query-mining), [Embarque](https://www.embarque.io/post/exact-match-keywords)).
- **N-gram significance filters** (avoid fractional-conversion noise): treat a gram as a
  real WINNER only when **conversions ≥ 1–2**; treat as a real WASTER on the
  **clicks > 150 (or cost above target-CPA) AND conversions = 0** filter
  ([Adalysis](https://adalysis.com/blog/n-gram-analysis-the-secret-to-scalable-search-term-management-in-google-ads/)).
- **N-gram sizing**: 1- and 2-word grams → best NEGATIVES; 3-word (and 4-word) grams →
  best new KEYWORDS. One broad-match negative gram can replace hundreds of exact negatives
  ([blimpp/n-gram](https://blimpp.com/run-n-gram-analysis-on-google-search-terms/), [PEMAVOR](https://www.pemavor.com/the-power-of-n-gram-analysis-unlocking-hidden-keyword-opportunities-in-google-ads/)).
- **Negation is data-driven, not proactive**: if you'd need to negate **≥10% of your search
  terms**, that's a red flag — the keyword/match type is too broad; fix targeting instead of
  playing negative-keyword whack-a-mole ([Search Engine Land](https://searchengineland.com/google-ads-search-terms-report-tips-465174)).
- **Waste cost threshold** for HIGH-COST-NO-CONV: a term/gram with **0 conversions** whose
  cost ≥ ~**1× the target CPA** is a negate candidate; scale the bar to account volume.
- **Currency/locale**: report in the account's native currency (many MLO brands run MXN,
  COP, GBP, EUR, USD). Never mix currencies or assume USD.
- This skill **analyzes and recommends only** — it never creates keywords or negatives.
  Application is done by `google-negative-keywords` (negatives) or by the user (new keywords).

## Output
A single deliverable with four parts (return inline; offer to write to Notion/CSV if asked):

**1. Action table** (one row per notable term):

| Search term | Clicks | Cost | Conv | Conv value | CPA | ROAS | Bucket | Action |
|---|---|---|---|---|---|---|---|---|
| crema hidratante piel seca | 41 | $58 | 4 | $312 | $14.5 | 5.4 | CONVERT | ADD as keyword (exact) |
| crema gratis muestra | 22 | $31 | 0 | $0 | – | – | IRRELEVANT | NEGATE (→ google-negative-keywords) |
| crema hidratante | 90 | $120 | 1 | $70 | $120 | 0.6 | HIGH-COST-NO-CONV* | MONITOR |
| [competitor] crema | 15 | $28 | 0 | $0 | – | – | COMPETITOR | MONITOR / decide |

**2. N-gram winners** (add candidates) and **n-gram wasters** (negate candidates), each with
aggregated cost / conv / CPA and gram size (1/2/3-word).

**3. Intent clusters** — 3–7 named themes with a one-line read on each (converts / wastes).

**4. Insight summary (3–5 lines)** — the headline: top ADD picks, biggest wasted tokens,
the dominant converting intent, and the single most valuable next action.

## Guardrails
- **Never auto-apply.** This skill only recommends; adding negatives goes through
  `google-negative-keywords` with a preview + confirmation, and new keywords are the user's call.
- **Respect significance.** Don't promote a keyword or flag a negative off a single stray
  click/conversion — honor the conversion and clicks>150 / cost≥target-CPA gates. Widen the
  window before judging low-volume terms.
- **Don't double-count intent.** Each term gets exactly one bucket; grams aggregate across
  terms but a term is only "converting" once.
- **Brand & competitor terms are decisions, not defaults.** Don't auto-negate brand terms;
  flag competitor terms for a human call (bidding on competitors can be intentional).
- **Currency/locale honesty.** Report native currency; note if visible spend is far below
  total campaign spend (Google is hiding "Other search terms").
- **Cross-reference, don't duplicate.** Segmentation and the negate hand-off are shared with
  `google-negative-keywords`; this skill owns the *analysis*, that skill owns the *exclusion*.

## References
See `reference/knowledge-base.md` for the full sourced criteria: n-gram method, promotion
gates, negative match-type behavior, thresholds, and all source URLs.
