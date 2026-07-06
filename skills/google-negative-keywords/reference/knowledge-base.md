# Knowledge base — Google Ads negative keywords

Distilled, cited expert know-how behind the `google-negative-keywords` skill. Every threshold below carries a source link; full list at the bottom.

---

## 1. Why negatives are the primary lever in 2025–2026

Google's match types have collapsed toward AI-driven intent matching. Exact match is "no longer truly exact — it includes synonyms, close variants, and intent-based matches," and broad/phrase are looser still. In AI-heavy campaign types (Performance Max, Demand Gen) advertisers have almost no granular targeting control left, so **negative keywords are "one of the few proactive controls left."** ([karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/))

Impact of neglect: unmanaged negative lists commonly drive **15–30% of non-brand Search and Shopping budget** as waste ([optmyzr](https://www.optmyzr.com/blog/negative-keywords/)). Disciplined negation typically recovers **10–20% of ad budget**; one vendor reports customers saving **$16M+/year** across Google + Amazon through negation ([karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/)). A published case study reported **47% lower cost-per-conversion and 52% less wasted spend** after adding 200+ negatives and shifting budget toward tighter match types ([optmyzr](https://www.optmyzr.com/blog/negative-keywords/)).

---

## 2. Match type behavior — the exact rules

The three negative match types and their blocking logic ([Google — about negative keywords](https://support.google.com/google-ads/answer/2453972), [storegrowers](https://www.storegrowers.com/negative-keyword-match-types/)):

| Type | Syntax | Blocks when the query… | Example `running shoes` |
|------|--------|------------------------|--------------------------|
| **Broad** (default) | `running shoes` | contains **all** the words, in **any order** | blocks "running shoes", "shoes running", "red running shoes"; allows "running" or "shoes" alone |
| **Phrase** | `"running shoes"` | contains the words **in order** (extra words allowed before/after) | blocks "buy running shoes online", "leather running shoes"; allows "shoes for running" |
| **Exact** | `[running shoes]` | is **exactly** those words, no extras | blocks only "running shoes"; allows "red running shoes", "buy running shoes" |

Note: negative **broad** is confusingly named — it is actually the most *restrictive* in the sense that it fires on any word-order permutation, but only when *all* words are present. Phrase is the "good balance between blocking enough and not accidentally over-blocking" and is the recommended default when unsure ([storegrowers](https://www.storegrowers.com/negative-keyword-match-types/)).

### Match-type decision framework

| Situation | Match type |
|-----------|-----------|
| Block an entire concept/theme/brand you never want (free, jobs, wholesale, a competitor) | **Broad** |
| Block a product line or multi-word context while keeping longer valid tails | **Phrase** |
| Block one specific high-cost, 0-conversion query while its longer cousins still convert | **Exact** |
| Default when unsure | **Phrase** |

Source: [storegrowers](https://www.storegrowers.com/negative-keyword-match-types/).

### Critical edge cases
- **Google defaults new negatives added from the Search Terms Report to EXACT match.** You almost always want to change to phrase before saving — this is the single most common silent mistake. ([storegrowers](https://www.storegrowers.com/negative-keyword-match-types/), [karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/))
- **No close variants.** Unlike positive keywords, negatives do NOT auto-expand to plurals/variants — `running shoe` and `running shoes` are treated as completely different terms. Add both forms when you need both. ([Google](https://support.google.com/google-ads/answer/2453972), [storegrowers](https://www.storegrowers.com/negative-keyword-match-types/))
- **Exception — misspellings:** since **June 2024**, negatives automatically block misspellings (adding `analytics` blocks `anlytics`, `analitics`). You no longer need to enumerate typos. ([karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/))
- **16-word cap:** search phrases longer than 16 words may bypass a negative if the negative's terms appear after the 16th word. ([Google](https://support.google.com/google-ads/answer/2453972))
- **Symbols:** allowed → `&`, accent marks (`á`), `*`. Ignored → `.`, `+`. Invalid → commas, `!`, `@`, `%`, `^`, parentheses, brackets, `;`, `~`, backticks, `<>`, `?`, `\`, `|`. ([Google](https://support.google.com/google-ads/answer/2453972))

---

## 3. The triage workflow (search terms → negatives)

The Search Terms Report is "the only trustworthy source for new exclusions." Report lives under **Insights and reports → Search terms**. ([optmyzr](https://www.optmyzr.com/blog/negative-keywords/), [searchengineland](https://searchengineland.com/google-ads-search-terms-report-tips-465174))

Step order:
1. **Sort by cost (or impressions), descending.** "Look for queries that spent money but generated no conversions." Wasted spend concentrates at the top. ([optmyzr](https://www.optmyzr.com/blog/negative-keywords/))
2. **Filter to 0 conversions + meaningful cost** over a 30–90 day window (enough spend and conversion signal; too short a window = noise). No universal $ threshold exists in the literature — it's a qualitative "clearly irrelevant" judgment scaled to the account; a practical floor is cost ≥ ~1× target CPA (or ≥ 2–3× avg CPC) with 0 conversions.
3. **Classify** each candidate against the relevance dimensions (section 4).
4. **Assign match type** per the framework (section 2).
5. **Bucket into shared lists** (section 5) and de-duplicate.

**Cadence:** block a recurring **20–30 min/week** slot for search-terms review; that's enough for most accounts. "Most advertisers spend more time reporting than actually optimizing." ([searchengineland — filters](https://searchengineland.com/google-ads-search-term-filters-cut-wasted-spend-458977), [optmyzr](https://www.optmyzr.com/blog/negative-keywords/))

**Also promote, don't only block:** while triaging, flag any high-intent converting query worth pulling into its own ad group/campaign. Negation and promotion are the two outputs of every review. ([searchengineland](https://searchengineland.com/google-ads-search-terms-report-tips-465174))

---

## 4. Classification dimensions

Adapted from the dmitry-ai negative-keywords pipeline, which classifies every search query against these criteria ([github: dmitry-ai/google-ads-negative-keywords-pipeline](https://github.com/dmitry-ai/google-ads-negative-keywords-pipeline)):

1. **Geographical relevance** — query targets a location outside the brand's shipping/service area.
2. **Service/product-type match** — query is for something the business doesn't sell (a supplement brand getting "recipe" searches).
3. **DIY / informational intent** — user wants to do it themselves or is just researching, not buying ("how to", "tutorial", "diy").
4. **Competitor brand mentions** — query names a competitor; block from prospecting, sometimes keep for conquesting campaigns.
5. **Budget / freebie indicators** — price-sensitive or free-seeker intent ("free", "gratis", "cheap", "barato", "used", "segunda mano").

Anything matching a dimension = candidate negative. Anything ambiguous or possibly valuable = leave it out (under-blocking is cheaper than over-blocking — section 6). The pipeline batches queries through an LLM to classify at scale; the same dimensions drive manual triage.

---

## 5. List architecture (shared/negative lists)

Google's own limits ([Google system limits / about negative keyword lists](https://support.google.com/google-ads/answer/2453983), [searchengineland — limit change](https://searchengineland.com/google-ads-doubles-negative-keyword-list-limit-glitch-or-quiet-policy-change-462361)):
- **20 negative keyword lists per account**
- **5,000 keywords per list** (Google has occasionally accepted lists slightly over, per Ginny Marvin, but treat 5,000 as the ceiling)
- **1,000 account-level negatives** (apply across all eligible campaigns; best for truly universal junk)
- **PMax: 10,000 negatives per campaign** since March 2025, with match-type + shared-list support ([karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/))

Recommended three-tier architecture ([gofishdigital](https://gofishdigital.com/blog/negative-keywords-in-google-ads-the-key-to-scalable-campaigns/), [karooya — shared lists](https://www.karooya.com/blog/create-shared-negative-keyword-list-in-google-ads/)):

**Tier 1 — Universal / Master list** (reusable across every account). Junk irrelevant to any DTC brand. Starter set (add ES for Spanish-market brands):
- EN: `free`, `jobs`, `careers`, `salary`, `hiring`, `resume`, `meme`, `pdf`, `tutorial`, `how to`, `diy`, `used`, `second hand`, `reviews`, `complaints`, `wikipedia`, `youtube`, `login`, `download`, `template`.
- ES: `gratis`, `empleo`, `trabajo`, `sueldo`, `curriculum`, `barato`, `segunda mano`, `usado`, `opiniones`, `foro`, `casero`, `hazlo tu mismo`.
Sources: [saashero](https://www.saashero.net/google-ppc/google-ads-management-negative-keywords/), [ppc.io industry examples](https://ppc.io/blog/negative-keywords-examples).

**Tier 2 — Industry list** — vertical-specific junk (supplements: `side effects`, `banned`, `recipe`; apparel: `sewing pattern`, `wholesale`; etc.). ([ppc.io](https://ppc.io/blog/negative-keywords-examples))

**Tier 3 — Campaign / funnel list** — intent-tier exclusions:
- Block **branded / BOF** terms out of **TOF prospecting** campaigns (don't pay prospecting rates for people who already know the brand).
- Block **competitor / research** terms out of **BOF** campaigns.
- Separate brand vs. non-brand, and exclude regional variants where relevant.
Sources: [gofishdigital](https://gofishdigital.com/blog/negative-keywords-in-google-ads-the-key-to-scalable-campaigns/), [negator.io hybrid architecture](https://www.negator.io/post/google-ads-2025-algorithm-update-survival-guide-negative-keyword-strategies).

Ad-group-level negatives remain useful for **surgical** exclusions where ad groups are tightly themed (e.g. keeping "cheap" out of a premium ad group). ([saashero](https://www.saashero.net/google-ppc/google-ads-management-negative-keywords/))

**Official / MCC-level automation:** for managing universal lists across many accounts, the Google-maintained exclusion scripts apply MCC-level shared negative lists programmatically ([github: google-marketing-solutions/google-ads-exclusion-scripts](https://github.com/google-marketing-solutions/google-ads-exclusion-scripts), [Google — common negative list script](https://developers.google.com/google-ads/scripts/docs/solutions/common-negative-list)).

---

## 6. The over-blocking rule (the expert's core caution)

"We just see people are just overusing negative keywords... you're much more likely to make a mistake and exclude things too broadly." A wrong broad negative silently suppresses legitimate, converting traffic — and that costs more than a negative you never added. ([optmyzr](https://www.optmyzr.com/blog/negative-keywords/))

Practical rules:
- **Fewest negatives that block the most junk.** Add the minimum number needed. ([Google](https://support.google.com/google-ads/answer/2453972))
- **De-duplicate against broader negatives.** A broad `free` makes exact `[free shipping]` redundant *and* risky (it may be doing nothing while looking like coverage).
- **Never negate a converter**, including assisted conversions where visible.
- **When unsure, go narrower** (phrase or exact) or skip the term.
- **Watch geo/competitor nuance:** a competitor term you block in prospecting might be a valid conquesting target elsewhere — scope it to the right list, don't account-level it blindly.

---

## 7. Expert video source

**"Google Ads Keywords Tutorial 2024 — Research, Targeting, Negatives, Match Types, and Best Practices"** — Surfside PPC (YouTube): <https://www.youtube.com/watch?v=W2nDyCY0-ZM>. Recognized PPC-education channel; the tutorial walks the Search Terms Report workflow end to end — selecting one or multiple search terms via checkboxes, "add as negative keyword," saving to campaign or ad-group level, and the reminder that Google stages new negatives as **exact match** by default so you must set the intended match type before saving. (Full transcript not machine-retrievable through the fetch tool; guidance corroborated by the [storegrowers](https://www.storegrowers.com/negative-keyword-match-types/) and [karooya](https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/) written sources cited above.)

---

## Sources
- Google Ads Help — About negative keywords: https://support.google.com/google-ads/answer/2453972
- Google Ads Help — About negative keyword lists / system limits: https://support.google.com/google-ads/answer/2453983
- Google Ads Help — Set up and apply negative keyword lists: https://support.google.com/google-ads/answer/7449003
- Google Ads Help — Get negative keyword ideas using the search terms report: https://support.google.com/google-ads/answer/7102466
- Google for Developers — Common Negative List script (single account): https://developers.google.com/google-ads/scripts/docs/solutions/common-negative-list
- GitHub — dmitry-ai/google-ads-negative-keywords-pipeline: https://github.com/dmitry-ai/google-ads-negative-keywords-pipeline
- GitHub — google-marketing-solutions/google-ads-exclusion-scripts: https://github.com/google-marketing-solutions/google-ads-exclusion-scripts
- Store Growers — Negative keyword match types: https://www.storegrowers.com/negative-keyword-match-types/
- Optmyzr — Negative keywords / reduce wasted spend (2026): https://www.optmyzr.com/blog/negative-keywords/
- Karooya — Keywords & negative keywords in Google Ads 2025: https://www.karooya.com/blog/keywords-negative-keywords-in-google-ads-2025/
- Karooya — Create a shared negative keyword list: https://www.karooya.com/blog/create-shared-negative-keyword-list-in-google-ads/
- Go Fish Digital — Negative keywords, scalable campaigns: https://gofishdigital.com/blog/negative-keywords-in-google-ads-the-key-to-scalable-campaigns/
- SaaS Hero — Negative keyword management guide: https://www.saashero.net/google-ppc/google-ads-management-negative-keywords/
- PPC.io — Negative keywords by industry (150+ examples): https://ppc.io/blog/negative-keywords-examples
- Search Engine Land — Search terms report tips: https://searchengineland.com/google-ads-search-terms-report-tips-465174
- Search Engine Land — Search term filters to cut wasted spend: https://searchengineland.com/google-ads-search-term-filters-cut-wasted-spend-458977
- Search Engine Land — Negative keyword list limit change: https://searchengineland.com/google-ads-doubles-negative-keyword-list-limit-glitch-or-quiet-policy-change-462361
- Negator.io — 2025 algorithm update / negative keyword strategies: https://www.negator.io/post/google-ads-2025-algorithm-update-survival-guide-negative-keyword-strategies
- YouTube (Surfside PPC) — Google Ads Keywords Tutorial 2024: https://www.youtube.com/watch?v=W2nDyCY0-ZM
