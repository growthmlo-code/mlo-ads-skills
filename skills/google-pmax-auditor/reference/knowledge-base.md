# Knowledge base — Google Performance Max Auditor

Distilled, sourced expert criteria for auditing a Google Ads Performance Max (PMax) campaign.
Every threshold below carries a source link. Full URL list at the bottom.

---

## 1. Why PMax needs a structured audit (the "black box" problem)

PMax hides most levers: no ad-group-level negatives, incomplete search-term visibility, and
blended channel spend. The auditor's job shifts from "daily optimizations" to **guarding the
inputs that feed the algorithm** — "garbage in, garbage out." Prioritize the areas most
relevant to the specific business rather than treating every item equally.
([Search Engine Land — Auditing the PMax black box](https://searchengineland.com/auditing-the-performance-max-black-box-a-strategic-approach-457732))

**Prerequisite check (expert opinion):** PMax was designed to find *more* conversions from
your *existing* conversion data. With thin conversion history it is not the fix — use Search
and/or Shopping first to find winning products and build solid conversion data, then layer in
PMax. ([Aaron Young / Define Digital Academy — PMax Issues](https://www.definedigitalacademy.com/blog/google-ads-performance-max-issues))

---

## 2. Asset coverage & Ad Strength (per asset group)

**Maximums per asset group:** 15 headlines (30 char), 5 long headlines (90 char), 5
descriptions (90 char), 20 images, up to 5 videos. Google's AI assembles combinations per
placement. **Required image ratios:** landscape 1.91:1, square 1:1, portrait 4:5 — 5+ of each
recommended.
([Dataslayer — PMax Complete Guide 2025](https://www.dataslayer.ai/blog/google-ads-performance-max-complete-guide-2025))

- **Thin asset groups** (one or two headlines, a single image, no video) underperform vs
  fully populated, theme-relevant groups with custom creative. Flag any group not at
  **Excellent** Ad Strength.
- Improving asset ratings from **Good → Excellent lifts conversions ~6% on average.**
  ([Go Fish Digital — 2025 PMax Priorities](https://gofishdigital.com/blog/performance-max-priorities-2025/))
- 2025: asset reporting now shows impressions, clicks, and cost per asset (not just
  conversions), segmentable by device/time/conversions/network.
  ([Google Ads Help — Highlights 2025](https://support.google.com/google-ads/answer/16756291))

**Audit action:** count filled vs max slots per group; missing video or a missing image ratio
= High severity; below-Excellent Ad Strength = High/Med.

---

## 3. Search themes

- **Limit raised from 25 → 50 search themes per asset group** in 2025.
  ([Google Ads Help — Highlights 2025](https://support.google.com/google-ads/answer/16756291))
- Search themes are keyword-style guidance (not just audiences). Google shows a **"usefulness"
  indicator** — whether a theme generates extra traffic. Monitor it and replace low-usefulness
  themes. ([Go Fish Digital](https://gofishdigital.com/blog/performance-max-priorities-2025/))
- Reality check: the **messages in your assets drive targeting more than optional signals or
  themes** — thin/irrelevant creative undermines even good themes.
  ([Search Engine Land — audience signals & search themes](https://searchengineland.com/google-ads-pmax-audience-signals-search-themes-463329))

**Audit action:** every asset group should have relevant themes; flag zero-theme groups and
low-usefulness themes.

---

## 4. Audience signals

- Audience signals **teach the algorithm who your customers are — they do not restrict who
  sees ads.** Add past purchasers and PMax finds *similar* people, not just remarketing.
  Treating them as hard targeting is a common mistake.
  ([Go Fish Digital](https://gofishdigital.com/blog/performance-max-priorities-2025/))
- Highest-quality signals: Customer Match lists, converters, and **custom segments built from
  actual converting search terms**. A missing or generic-interest signal slows learning.
  ([Search Engine Land — audit framework](https://searchengineland.com/auditing-the-performance-max-black-box-a-strategic-approach-457732))

---

## 5. Brand exclusions & Search cannibalization

- PMax tends to **cannibalize Search campaigns**, especially brand queries (cheap, high-intent
  clicks a brand Search campaign should win). Align **brand exclusions** with a decision about
  where brand traffic should live.
  ([Search Engine Land — audit framework](https://searchengineland.com/auditing-the-performance-max-black-box-a-strategic-approach-457732))
- The **PMax Search Terms Report** now lets you attack this with real query data rather than
  campaign-level guesses: harvest high-performing terms back into Search, and confirm whether
  PMax is stealing brand terms.
  ([Ten Thousand Foot View — PMax Search Terms](https://www.tenthousandfootview.com/p-max-search-terms-keywords/))

**Audit action:** compare PMax brand-term conversions vs the brand Search campaign; if PMax
dominates brand terms, enable brand exclusions and route brand to Search (High severity).

---

## 6. Budget pacing & bidding (tROAS / tCPA)

- **Daily budget ≈ 3× your target CPA**; start at roughly **$50–100/day for 4–6 weeks** to let
  the algorithm learn before judging.
  ([Dataslayer — PMax Complete Guide 2025](https://www.dataslayer.ai/blog/google-ads-performance-max-complete-guide-2025))
- **Don't set tROAS/tCPA too aggressively before enough data** — it over-restricts delivery
  during learning. Ensure tROAS reflects **rule-adjusted conversion values, not raw**, or bids
  misalign. ([HyperFX — PMax Best Practices](https://www.hyperfx.ai/blog/performance-max-best-practices-2026))
- Monthly audits should compare tCPA/tROAS targets against actual performance and review
  placement data + audience signal freshness.
  ([HyperFX](https://www.hyperfx.ai/blog/performance-max-best-practices-2026))

**Audit action:** if budget is constrained or lost-IS-budget high, note it; if tROAS is far
above account average, it is likely throttling delivery.

---

## 7. Negatives, layered (the biggest 2025 change)

- **Per-campaign limit raised from 100 → 10,000** on **2025-03-11** (Ginny Marvin / Google Ads
  Liaison), aligning PMax with Search; rollout completed within weeks.
  ([PPC.land — 10,000 limit](https://ppc.land/google-raises-negative-keywords-limit-to-10-000-for-performance-max-campaigns/))
- **Shared negative keyword lists** for PMax: reported in July, **official rollout completed
  Aug 7 2025** — build one Master brand-safety list and apply across all PMax campaigns.
  ([GROAS — negative keyword list limit 2025](https://groas.ai/post/google-ads-negative-keyword-list-limit-what-changed-in-2025-how-to-use-it))
- **Account-level negatives max 1,000**; documented per-shared-list limit ~5,000 (some
  advertisers report adding more without error).
  ([GROAS — 10,000 keyword guide](https://groas.ai/post/performance-max-negative-keywords-2025-complete-guide-to-the-10-000-keyword-limit))
- **Three implementation methods (official):** campaign-level (Keywords → Negative keywords,
  one per line, with match-type symbols), shared lists, and account-level (auto-applies).
  Negatives apply to **Search & Shopping inventory only** — **not** YouTube/Display/Gmail/
  Discover. ([Google Ads Help — PMax negative keywords](https://support.google.com/google-ads/answer/15726455))
- **Cadence:** update negatives at least **weekly** from search-term insights. Caveat: PMax
  search-term visibility is still incomplete, so some waste stays hidden — strategy is
  reactive. ([Karooya — why negatives matter more than ever](https://www.karooya.com/blog/why-negative-keywords-matter-more-than-ever-in-performance-max-campaigns/))

**Layering model to audit for:** Master shared list (always-off / brand safety) → campaign
negatives (surgical, up to 10,000) → account negatives (max 1,000, global). No negatives on a
spending campaign = High severity.

---

## 8. PMax Search Terms Report (waste + harvesting)

- **Launched ~end of March 2025** (unannounced), alongside the negatives tool. Provides a full
  KPI set per query: impressions, clicks, CTR, conversions, conv. rate, CPA, ROAS. **No
  breakdown by asset group.**
  ([Ten Thousand Foot View](https://www.tenthousandfootview.com/p-max-search-terms-keywords/))
- Google frames it as "the same granularity of Search reporting … right in Performance Max."
  ([Google Ads Help — Highlights 2025](https://support.google.com/google-ads/answer/16756291))
- **Two uses:** (1) harvest high-performing terms into relevant Search campaigns as target
  keywords; (2) add low-CTR / irrelevant queries as negatives. Filter by conversions (high→low)
  for winners and by impressions × low CTR for waste.
  ([Ten Thousand Foot View](https://www.tenthousandfootview.com/p-max-search-terms-keywords/))

---

## 9. Final URL expansion

- Confirm it's **ON with URL exclusions** for pages you never want to send traffic to (cart,
  account, login, blog, out-of-stock), or intentionally OFF. Unbounded expansion routes spend
  to junk/low-intent URLs.
  ([Search Engine Land — audit framework](https://searchengineland.com/auditing-the-performance-max-black-box-a-strategic-approach-457732))

---

## 10. Listing groups / feed health (retail only)

- Verify **Merchant Center is linked**; audit product feed titles, descriptions, and **custom
  labels**; check feed update frequency; **audit disapprovals and stock** for top sellers.
- Confirm listing groups aren't concentrating budget on one SKU while starving the catalog.
  ([Search Engine Land — audit framework](https://searchengineland.com/auditing-the-performance-max-black-box-a-strategic-approach-457732),
  [Dataslayer](https://www.dataslayer.ai/blog/google-ads-performance-max-complete-guide-2025))

**Audit action:** disapproved or out-of-stock top sellers = High severity (they silently kill
Shopping delivery).

---

## 11. Severity / prioritization model

Impact-based, not a fixed score
([Search Engine Land — audit framework](https://searchengineland.com/auditing-the-performance-max-black-box-a-strategic-approach-457732)):

- **High (fix now):** broken conversion tracking; broken forms/checkout; disapproved or
  out-of-stock top products; missing customer-match audience; no negatives on spending
  campaign; brand cannibalization; Poor/Average Ad Strength.
- **Medium (next):** incomplete asset groups; underperforming standard Search campaign;
  Final URL expansion without exclusions; over-aggressive tROAS.
- **Low (ongoing):** ad-extension gaps; feed-title optimization; search-theme refinement.

---

## Expert video / educator source

- **YouTube expert:** **Aaron Young — Define Digital Academy** (self-described #1 Google Ads
  educator on YouTube, 120k+ subscribers; covers Search, Shopping, PMax, Demand Gen). Channel:
  <https://www.youtube.com/@AaronYoungGoogleAds>. Companion write-up used here —
  ["Google Ads Performance Max Issues"](https://www.definedigitalacademy.com/blog/google-ads-performance-max-issues)
  — his core PMax thesis: PMax only works on top of solid conversion data built first via
  Search/Shopping. (A second respected PMax video educator is **Surfside PPC**,
  <https://www.youtube.com/surfsideppc> — clear step-by-step PMax walkthroughs.)
  *Note: full video transcripts were not retrievable in this environment, so the educator's
  published articles/channel are cited in their place, per build-template guidance.*

---

## Sources

- Google Ads Help — Performance Max negative keywords: https://support.google.com/google-ads/answer/15726455
- Google Ads Help — Highlights 2025: https://support.google.com/google-ads/answer/16756291
- Karooya — Why negative keywords matter more than ever in PMax: https://www.karooya.com/blog/why-negative-keywords-matter-more-than-ever-in-performance-max-campaigns/
- Ten Thousand Foot View — PMax Search Terms / Keywords: https://www.tenthousandfootview.com/p-max-search-terms-keywords/
- Search Engine Land — Auditing the PMax black box: https://searchengineland.com/auditing-the-performance-max-black-box-a-strategic-approach-457732
- Search Engine Land — PMax audience signals & search themes: https://searchengineland.com/google-ads-pmax-audience-signals-search-themes-463329
- Go Fish Digital — 2025 PMax Priorities checklist: https://gofishdigital.com/blog/performance-max-priorities-2025/
- Dataslayer — Google Ads Performance Max Complete Guide 2025: https://www.dataslayer.ai/blog/google-ads-performance-max-complete-guide-2025
- HyperFX — Performance Max Best Practices 2026: https://www.hyperfx.ai/blog/performance-max-best-practices-2026
- PPC.land — Google raises negative keywords limit to 10,000 for PMax: https://ppc.land/google-raises-negative-keywords-limit-to-10-000-for-performance-max-campaigns/
- GROAS — PMax Negative Keywords 2025 (10,000 guide): https://groas.ai/post/performance-max-negative-keywords-2025-complete-guide-to-the-10-000-keyword-limit
- GROAS — Google Ads Negative Keyword List Limit: What Changed in 2025: https://groas.ai/post/google-ads-negative-keyword-list-limit-what-changed-in-2025-how-to-use-it
- Aaron Young / Define Digital Academy — Google Ads Performance Max Issues: https://www.definedigitalacademy.com/blog/google-ads-performance-max-issues
- Aaron Young — YouTube channel: https://www.youtube.com/@AaronYoungGoogleAds
- Surfside PPC — YouTube channel: https://www.youtube.com/surfsideppc
