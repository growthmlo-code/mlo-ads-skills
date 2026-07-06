# Knowledge Base — Google Search Terms Mining & N-gram Analysis

Distilled, sourced expertise behind the `google-search-terms` skill. This is the ANALYSIS
layer (find keywords to add + cluster intent + flag waste). The exclusion *action* (choosing
match type, level, and applying negatives) belongs to the sibling `google-negative-keywords`
skill — cross-referenced below, not duplicated.

---

## 1. What the Search Terms Report is (and its blind spot)

The Search Terms Report lists the actual queries users typed that triggered your ads, with
per-term cost, clicks, impressions, conversions and conversion value. Critically, a search
term has its **own** match type — Google's *judgment* of how the query mapped to your keyword
— which is distinct from the keyword's match type (the *rule* you set). Segmenting the report
by search-term match type surfaces where broad match is drifting.

Blind spot: Google withholds low-volume/privacy-sensitive queries under "**Other search
terms**". You can only mine what's visible. If visible spend is far below total campaign
spend, note the gap — you are optimizing a partial view. If hidden terms consume budget with
worse performance than visible ones, that argues for narrowing targeting (tighter match types
/ exact keywords) rather than adding more negatives.

Sources: [Search Engine Land — Search terms report: 5 tips](https://searchengineland.com/google-ads-search-terms-report-tips-465174),
[Google Ads Help — negative keyword ideas from the search terms report](https://support.google.com/google-ads/answer/7102466?hl=en).

---

## 2. Term-level segmentation (the six buckets)

Every visible term is classified into exactly one bucket. Optmyzr's guide recommends
categorizing terms rather than eyeballing a flat list:

- **CONVERT** — has conversions and hits target (CPA ≤ target or ROAS ≥ target/breakeven).
- **BRAND** — contains the advertiser's own name/variants. Report separately; usually keep.
- **COMPETITOR** — contains a competitor's brand. A human decision (bidding on competitors
  can be intentional); don't auto-negate.
- **HIGH-COST-NO-CONV** — spent money, produced zero conversions → primary waste candidate.
  Optmyzr's identification method: sort by cost/impressions and find "queries that spent
  money but generated no conversions."
- **IRRELEVANT** — intent unrelated to the offer (jobs, "free", DIY, wrong product, wrong
  geo). Example given: human haircare showing for "pet shampoo."
- **MONITOR** — has spend/clicks but below significance; not yet decidable.

Level of exclusion (when it later goes to the negatives skill): reserve **account-level**
negatives for universally irrelevant intent; use **ad-group-level** for narrow relevance
conflicts.

Source: [Optmyzr — Negative keywords guide](https://www.optmyzr.com/blog/negative-keywords/),
[Google Ads Help](https://support.google.com/google-ads/answer/7102466?hl=en).

---

## 3. N-gram analysis — the word-level engine

**Definition**: N-grams are one-, two-, or three-word patterns found inside search terms.
You aggregate performance (cost, clicks, conversions, conv value) for each n-gram across
every term that contains it. This collapses complexity dramatically — an account with a
million search terms often has only **30,000–50,000 n-grams** — making patterns visible that
manual term-by-term review misses.

**How aggregation surfaces waste**: e.g. "search terms including 'and leisure' or 'lawn and
leisure' have spent over $1,000, with zero conversions" — individual terms roll up into a
pattern-level verdict you can act on with one negative.

**Filters (from Adalysis)**:
- Wasteful pattern: `Conversions = 0`, sort by cost — or the stricter
  **`Clicks > 150 AND Conversions = 0`**.
- Avoid fractional-conversion noise: require **`Conversions ≥ 1`** (some use ≥ 2) and
  **`Clicks > 150`** before trusting a WINNER gram.
- Sort winning grams by CPA / ROAS to rank promote candidates.

**Gram sizing rule (the key heuristic)**: **1- and 2-word grams** are the best source of new
**negative** keywords; **3- and 4-word grams** are the best source of new **positive**
keywords to target. A single well-chosen broad-match negative gram can replace hundreds of
exact-match negatives — accounts using n-gram optimization reach the same control with
~**73% fewer negative keywords**.

Tooling: n-gram analysis lives outside the Google Ads UI, so it's done via a script or tool —
WordStream's free copy-paste Google Ads script, the Brainlabs/Nils Rooijmans "Search Query
Mining" script, Adalysis (N-grams tab, click the + to see the underlying terms), or Optmyzr's
Search Term N-Grams word-cloud tool. In this skill we compute the grams from the report data
directly rather than requiring a script install.

Sources: [Adalysis — N-gram analysis: the secret to scalable search-term management](https://adalysis.com/blog/n-gram-analysis-the-secret-to-scalable-search-term-management-in-google-ads/),
[PEMAVOR — The power of n-gram analysis](https://www.pemavor.com/the-power-of-n-gram-analysis-unlocking-hidden-keyword-opportunities-in-google-ads/),
[WordStream — The only Google Ads script you need](https://www.wordstream.com/blog/n-gram-google-ads-script),
[blimpp — Run n-gram analysis on Google search terms](https://blimpp.com/run-n-gram-analysis-on-google-search-terms/),
[Nils Rooijmans — Brainlabs Search Query Mining script (updated)](https://nilsrooijmans.com/updated-google-ads-script-brainlabs-search-query-mining-for-n-gram-analysis/).

---

## 4. Promoting converting search terms → exact-match keywords

The core "search query mining" play (WordStream): broad match is the discovery engine; the
goal is to find *profitable* queries and pull them out as **exact-match** keywords.

Method: "When you find a search term with multiple conversions and a cost-per-conversion
below your target, pull it out, add it as an exact-match keyword in its own ad group, and
give it dedicated attention." Promote top-performing broad terms into phrase/exact campaigns.

**Why exact match**: it reaches the most relevant audience, drives higher Quality Scores
(ad relevance to searcher intent), and yields lower CPCs and better ad positions.

**Promotion gate used by the skill**: repeatable conversion signal (≈ **2+ conversions**
in-window) AND CPA ≤ target (or ROAS ≥ target/breakeven). The "multiple conversions +
below-target CPA" bar mirrors the WordStream criterion; the ≥2 conversion floor also matches
the n-gram significance filters above (avoid promoting off a single stray conversion).

Cadence: don't let broad match run unchecked. "A single week of unchecked broad match
activity can generate dozens of low-intent queries" — review at least every 1–2 weeks; a full
month is too long between checks for broad-match-heavy accounts.

Sources: [WordStream — Advanced search query mining](https://www.wordstream.com/blog/ws/2010/11/10/advanced-search-query-mining),
[Embarque — Exact match keywords guide](https://www.embarque.io/post/exact-match-keywords),
[Search Engine Land — 5 tips (Tip 5: add the keyword column; promote high performers)](https://searchengineland.com/google-ads-search-terms-report-tips-465174).

---

## 5. Intent / theme clustering

Beyond word-level grams, group terms into 3–7 named intent clusters (e.g. material,
problem→solution, gift, comparison/"vs", location, price/"cheap"/"free"). Clustering shows
the *shape of demand*: which intents convert (feed them keywords/budget) and which burn budget
(negate at the cluster level). This is the strategic read that a flat action table alone
misses, and it's how you decide between "add more keywords in this theme" vs "this whole theme
is off-intent, negate it."

Source (n-gram/theme grouping rationale): [Adalysis](https://adalysis.com/blog/n-gram-analysis-the-secret-to-scalable-search-term-management-in-google-ads/),
[PEMAVOR — N-gram analysis in PPC](https://www.pemavor.com/n-gram-analysis-in-ppc/).

---

## 6. Negative match-type behavior (hand-off knowledge)

This skill *flags* negation candidates; the actual creation is done by
`google-negative-keywords`. But the analyst needs to know how negatives behave so the flags
are correctly sized (1-2-word gram → broad/phrase negative; specific term → exact):

- **Negative broad** (no operators): blocks searches containing ALL the words in any order;
  does **not** block close variants. `running shoes` blocks "running shoes" and "shoes
  running" but allows "running shoe" (singular).
- **Negative phrase** (quotes): blocks the words in that order. `"running shoes"` blocks
  "leather running shoes" but allows "shoes running".
- **Negative exact** (brackets): blocks only that precise phrase. `[running shoes]` blocks
  only that term, allowing "red running shoes".
- **Negatives don't match close variants** (plurals, misspellings, synonyms) the way positive
  keywords do — you must list variants explicitly. Google confirms: "negative keyword match
  types work differently than their positive counterparts and don't match to variants."
- **UI default when adding a negative = exact match** (lowest coverage) — Store Growers
  recommends phrase as the safer default for most single-word/short negatives.
- **List limits**: Performance Max supports up to **10,000 negative keywords per campaign**.

Application workflow (Google): Campaigns → Insights and reports → Search terms → check
boxes → "Add as negative keyword" → choose ad group / campaign / new or existing list.

Sources: [Store Growers — Negative keyword match types](https://www.storegrowers.com/negative-keyword-match-types/),
[Google Ads Help](https://support.google.com/google-ads/answer/7102466?hl=en),
[Google Ads Scripts — negative keywords example (operational add/get functions, not selection logic)](https://developers.google.com/google-ads/scripts/docs/examples/negative-keywords).

---

## 7. Thresholds & guardrails cheat-sheet

| Rule | Value | Source |
|---|---|---|
| Default analysis window | 30 days (extend to 60–90d for low volume) | Optmyzr / general practice |
| Promote-to-exact gate | ≥ ~2 conversions in-window AND CPA ≤ target (or ROAS ≥ target/breakeven) | WordStream, Adalysis |
| N-gram WINNER filter | Conversions ≥ 1 (prefer ≥ 2), Clicks > 150 | Adalysis |
| N-gram WASTER filter | Conversions = 0 AND (Clicks > 150 OR cost ≥ ~1× target CPA) | Adalysis |
| Gram sizing | 1-2 words → negatives; 3-4 words → new keywords | blimpp, PEMAVOR |
| "Too many negatives" red flag | Needing to negate ≥ 10% of search terms → fix targeting, not negatives | Search Engine Land |
| Negative-keyword reduction from n-grams | ~73% fewer negatives for same control | groas / n-gram community data |
| PMax negative keyword limit | 10,000 per campaign | Store Growers |
| Review cadence (broad match) | Every 1–2 weeks; a month is too long | WordStream / mirachapps |
| Currency/locale | Always report in the account's native currency; never assume USD | MLO operating rule |

---

## 8. Relationship to `google-negative-keywords`

- **This skill** = the analysis engine. It mines the report, runs n-grams, segments,
  clusters intent, and outputs an action table with ADD / NEGATE / MONITOR / IGNORE plus an
  insight summary. It never creates keywords or negatives.
- **`google-negative-keywords`** = the exclusion action. It takes the NEGATE candidates,
  picks the correct match type (broad/phrase/exact), the correct level (ad group / campaign /
  shared list), previews the impact, and applies with confirmation.
- Shared concepts (segmentation buckets, negative match-type behavior) are documented in both
  for self-containment, but each skill owns one half of the workflow. Always hand NEGATE rows
  to `google-negative-keywords`; keep ADD rows here (the media buyer/user creates the keyword).

---

## Sources

- Search Engine Land — Google Ads search terms report: 5 tips — https://searchengineland.com/google-ads-search-terms-report-tips-465174
- Google Ads Help — Get negative keyword ideas using the search terms report — https://support.google.com/google-ads/answer/7102466?hl=en
- Optmyzr — Negative keywords: reduce wasted spend — https://www.optmyzr.com/blog/negative-keywords/
- Store Growers — Negative keyword match types — https://www.storegrowers.com/negative-keyword-match-types/
- Google Ads Scripts — Negative keywords example — https://developers.google.com/google-ads/scripts/docs/examples/negative-keywords
- Adalysis — N-gram analysis: the secret to scalable search-term management — https://adalysis.com/blog/n-gram-analysis-the-secret-to-scalable-search-term-management-in-google-ads/
- PEMAVOR — The power of n-gram analysis — https://www.pemavor.com/the-power-of-n-gram-analysis-unlocking-hidden-keyword-opportunities-in-google-ads/
- PEMAVOR — N-gram analysis in PPC — https://www.pemavor.com/n-gram-analysis-in-ppc/
- WordStream — The only Google Ads script you need for keyword optimization (n-gram) — https://www.wordstream.com/blog/n-gram-google-ads-script
- WordStream — Advanced search query mining — https://www.wordstream.com/blog/ws/2010/11/10/advanced-search-query-mining
- Embarque — Exact match keywords: tools & best practices — https://www.embarque.io/post/exact-match-keywords
- blimpp — Run n-gram analysis on Google search terms — https://blimpp.com/run-n-gram-analysis-on-google-search-terms/
- Nils Rooijmans — Brainlabs Search Query Mining n-gram script (updated) — https://nilsrooijmans.com/updated-google-ads-script-brainlabs-search-query-mining-for-n-gram-analysis/
- **YouTube (expert video)** — "Google Ads Search Terms Report Analysis Like a Boss (N-gram)" — https://www.youtube.com/watch?v=bFrFivJswUs
