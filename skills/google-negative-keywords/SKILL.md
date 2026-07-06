---
name: google-negative-keywords
description: Analyzes a Google Ads Search Terms Report and produces a clean, ready-to-apply negative keyword list — the correct match type per term, grouped into shared lists (universal/master, industry, campaign/funnel) — to cut wasted spend. ALWAYS use this skill when the user says "negative keywords", "palabras clave negativas", "limpiar search terms", "clean up search terms", "negativos de [marca]", "we're spending on terms that don't convert", "estamos gastando en términos que no convierten", "reduce wasted spend on Google", "cut junk search queries", or asks to build/refresh a negative keyword list or shared negative list for a DTC brand. Also trigger on casual asks like "review the search terms for X" or "which searches are wasting budget".
---

# Google Ads Negative Keyword Builder

## What it does
Takes a Google Ads Search Terms Report, triages every query by cost vs. conversions, flags the ones unrelated to the offer, and returns a de-duplicated negative keyword list with the *right match type per term* (broad / phrase / exact). Terms are organized into shared lists — a universal/master list, an industry list, and campaign/funnel lists — so the output is copy-paste ready and cuts wasted spend without over-blocking valid traffic.

## When to use
- User asks to clean up wasted Google spend: "we're spending on terms that don't convert", "estamos gastando en términos que no convierten".
- Explicit requests: "negative keywords", "palabras clave negativas", "limpiar search terms", "negativos de [marca]", "build a shared negative list".
- Periodic hygiene: "review the search terms report for [brand]", "revisa los search terms de X", "which queries are wasting budget this month".
- After launching broad/intent match keywords or a PMax/Demand Gen campaign, when irrelevant queries start showing up.

## Inputs needed
Ask for anything missing:
- **Account / brand** (which Google Ads account, and the store's offer so we know what's relevant vs. junk).
- **Date range** — default 30–90 days (need enough spend and conversion signal; too short = noise).
- **What the brand does NOT sell / does NOT want** — competitors to block, geos out of shipping range, wholesale/jobs/DIY intent, etc.
- **Conversion definition** — purchases only, or leads/add-to-cart too.
- **Where to write the output** — Notion table, CSV, or paste-ready blocks.

## Data sources
- **Google Ads Search Terms Report** — pull via the **Windsor.ai connector `google_ads`** (`get_data` requesting search-term + cost + conversions + clicks + impressions fields for the date range), or a Google Ads MCP if one is connected. If neither is connected, ask the user to export the Search Terms Report CSV from Google Ads (Insights and reports → Search terms) and hand it over.
- **Output** can be written to a **Notion table** (via the Notion MCP) or delivered as CSV / paste-ready text blocks.
- Be honest: this skill *prepares* the list; it does not push negatives into the account automatically. Applying them is a manual paste (or a Google Ads script) the user runs after approving the preview.

## Method
1. **Pull the report.** Get the Search Terms Report for the chosen window (default 30–90 days) with columns: search term, cost, conversions, clicks, impressions, and (if available) the matched keyword/campaign. Respect the account's currency and locale.
2. **Sort by cost, descending.** Wasted spend concentrates at the top. This is the triage order — always start from the most expensive queries.
3. **Filter to 0-conversion spend.** Isolate terms with **0 conversions and meaningful cost** in the window. "Meaningful" scales with the account: a practical floor is cost ≥ ~1× the target CPA (or ≥ 2–3× average CPC) with 0 conversions. Terms with conversions stay — never negate a converter.
4. **Classify each 0-conversion term** against the relevance dimensions (see Rules): geo mismatch, wrong service/product type, DIY/informational intent, competitor brand, budget/freebie intent ("free", "gratis", "cheap"), jobs/careers, or plainly off-topic. Anything that fits = candidate negative. Anything ambiguous or possibly-valuable = leave it (missing a negative is cheaper than over-blocking).
5. **Choose match type per term by intent** — the core decision:
   - **Broad negative** (no operators) → block a whole *theme/concept* the brand never wants (e.g. `free`, `jobs`, `wholesale`). Blocks any query containing all those words in any order.
   - **Phrase negative** (`"..."`) → block a *context/product line* while allowing longer valid tails (e.g. `"repair kit"`). The safe default when unsure.
   - **Exact negative** (`[...]`) → block *one specific query* that wastes spend while its longer-tail cousins still convert (e.g. `[running shoe review]`).
6. **Bucket into shared lists:**
   - **Universal/Master** — junk that's irrelevant for every brand/campaign: `free`, `gratis`, `jobs`, `empleo`, `careers`, `salary`, `meme`, `pdf`, `tutorial`, `how to`, `diy`, `used`, `segunda mano`, `reviews`, `complaints`. Reusable across accounts.
   - **Industry list** — junk specific to the vertical (e.g. for supplements: `recipe`, `side effects`, `banned`).
   - **Campaign/Funnel list** — intent-tier exclusions: block bottom-funnel/branded terms out of TOF prospecting campaigns, block competitor/research terms out of BOF, etc.
7. **De-duplicate & prune.** Remove terms already covered by a broader negative in the same list (a broad `free` makes exact `[free shipping]` redundant and risky). Keep the list minimal: *fewest negatives that block the most junk*.
8. **Build the preview.** Present a table: term | match type | list | 30–90d cost | conversions | reason. Sum the wasted spend being cut. Get explicit confirmation before anything is applied.

## Rules & thresholds
- **Match-type behavior (exact rules):** negative **broad** blocks a query only if it contains *all* the negative's words (any order); negative **phrase** blocks if the query contains the words *in order* (extra words allowed before/after); negative **exact** blocks *only* the precise term with no extra words. ([storegrowers](https://www.storegrowers.com/negative-keyword-match-types/), [Google](https://support.google.com/google-ads/answer/2453972))
- **Google defaults new negatives to EXACT** when added from the Search Terms Report — almost always change to **phrase** before saving. This is the #1 silent mistake. ([storegrowers](https://www.storegrowers.com/negative-keyword-match-types/))
- **No close variants.** Negatives do NOT auto-match plurals/variants — `running shoe` ≠ `running shoes`. Add both forms when needed. (Exception: since **June 2024**, misspellings are auto-blocked — `analytics` blocks `anlytics`.) ([Google](https://support.google.com/google-ads/answer/2453972), [karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/))
- **List limits:** up to **20 negative keyword lists per account**, **5,000 keywords per list**, and **1,000 account-level negatives**. Queries **longer than 16 words** may bypass negatives after the 16th word. ([Google system limits](https://support.google.com/google-ads/answer/2453983))
- **PMax negatives:** raised to **10,000 per campaign** (March 2025) with match-type + shared-list support — the main lever for cleaning automated campaigns. ([karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/))
- **2025 context:** even exact keywords now trigger synonyms/intent matches, so negatives are the primary control left in AI-heavy campaigns. This is why the skill exists. ([karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/))
- **Wasted-spend benchmark:** unmanaged negatives commonly drive **15–30% of non-brand Search/Shopping spend**; disciplined negation typically recovers **10–20%**. ([optmyzr](https://www.optmyzr.com/blog/negative-keywords/), [karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/))
- **Symbols:** `&`, accents, and `*` are allowed in negatives; `.` and `+` are ignored; commas/`@`/`%`/brackets are invalid. ([Google](https://support.google.com/google-ads/answer/2453972))

## Output
A **preview table** (Notion, CSV, or paste-ready), grouped by shared list:

| Term | Match type | List | Cost (30–90d) | Conv. | Reason |
|------|-----------|------|--------------|-------|--------|
| free | broad | Master | $412 | 0 | freebie intent |
| "repair kit" | phrase | Industry | $188 | 0 | not sold |
| [nike running shoe] | exact | Campaign | $96 | 0 | competitor / BOF |

Plus paste-ready blocks per list (one term per line, operators included) and a **total wasted spend recovered** figure. State clearly that these are staged for the user to review and apply — nothing is pushed to the account.

## Guardrails
- **Never negate a term that has conversions** (or assisted conversions if that data is available).
- **Never bulk-apply.** Always show the preview + wasted-spend total and get explicit confirmation. This skill produces a list; the human applies it.
- **Prefer under-blocking to over-blocking.** A wrong broad negative silently kills valid traffic and costs more than a missed negative. When unsure, use phrase or exact, or leave the term out.
- **Watch match type.** Never leave everything on the Google exact default; never make a specific 3-word query a broad negative (it will block far more than intended).
- **Respect currency/locale.** Use the account's real currency; write ES negatives (`gratis`, `empleo`, `barato`, `segunda mano`) for ES-market brands, not just English.
- **Don't double-cover.** Check the term isn't already blocked by an existing broader negative before adding it.

## References
See [`reference/knowledge-base.md`](reference/knowledge-base.md) for the full cited criteria, per-industry universal-list starter terms, match-type edge cases, list-architecture detail, and all source URLs.
