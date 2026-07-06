# Knowledge Base — Meta ASC Auditor (Advantage+ Shopping / Advantage+ Sales)

Distilled, cited criteria for auditing a Meta Advantage+ Shopping Campaign (ASC, now surfaced in Ads Manager as **Advantage+ Sales**). Every threshold below carries a source URL. This is the auditable know-how behind `SKILL.md`.

Context: MLO Growth runs DTC brands across multiple currencies (MXN, COP, EUR, GBP, USD). Read benchmarks as best-practice defaults, not absolutes — always sanity-check against the brand's own history and native currency.

---

## 1. What an ASC actually is (so you audit the right thing)

Advantage+ Shopping is a **simplified, AI-driven ecommerce campaign type**: one campaign, a **single ad set**, automated audience targeting across Meta's addressable market, and dynamic creative optimization that serves the best creative per user across Facebook, Instagram, Messenger and Audience Network. It supports **up to 150 creative combinations** per campaign (vs. up to 50 for manual). The API enforces a **one-to-one campaign↔ad-set relationship**, `IMPRESSIONS` is the only billing event, and a `pixel_id` is required. ([Meta Marketing API docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns), [Marpipe](https://www.marpipe.com/blog/what-is-meta-asc-advantage-shopping-campaign))

Meta's own results: ASC delivered **~17% lower cost per conversion** on average vs. manual campaigns, and in one Meta test **32% lower CPA** when accounts had enough conversion data. ASC surpassed a **$20B annualized revenue run rate in Q4 2024** (~70% YoY growth). ([search synthesis of Meta case data](https://bir.ch/blog/advantage-plus-sales-campaigns-guide))

**Audit implication:** if the campaign is a *manual* Sales campaign (multiple ad sets, manual audiences) that the user calls "Advantage+", flag it first — the checklist thresholds below assume a true single-ad-set ASC. Meta's Andromeda retrieval engine treats **creative** (visuals, hooks, themes, language) as the primary targeting signal, not audience settings — which is why creative volume/mix carries so much weight in this audit.

---

## 2. Catalog health

- A catalog should be **connected and verified**; aim for **≥50 active SKUs** so the algorithm has product breadth to work with. A `pixel_id` is required to run an ASC at all. ([Meta docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns))
- A well-maintained catalog is a prerequisite: keep product data "in tip-top shape" — resolve **rejected items and missing required fields** in catalog diagnostics before scaling. ([Marpipe](https://www.marpipe.com/blog/what-is-meta-asc-advantage-shopping-campaign))
- Catalog / dynamic (Advantage+ Catalog) ads are a supported ASC creative format via `product_set_id`. ([Meta docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns))

**Audit checks:** catalog connected? verified? active SKU count ≥50? diagnostics clean (no meaningful rejections)?

---

## 3. Tracking — Pixel + Conversions API

- **Both** the Pixel and the **Conversions API (CAPI)** should be firing — not one or the other. The Pixel is mandatory to launch; CAPI restores signal lost to iOS/ad-blockers and improves match quality. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/), [Meta docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns))
- **Attribution window:** standard ecom = **7-day click / 1-day view**; for high-consideration items over **~$200**, consider **7-day click only**. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))

**Audit checks:** Pixel firing? CAPI configured and sending events? event match quality acceptable? attribution window appropriate for the price point?

---

## 4. Conversion-data prerequisite

ASC needs a signal base before it optimizes well:
- **~50+ purchase conversions per week**, or **≥50 conversions in the last 30 days**, before results are reliable. Below that, ASC struggles and manual campaigns may do better. ([bir.ch](https://bir.ch/blog/advantage-plus-sales-campaigns-guide), [alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))
- Start with at least **~$50/day** to feed enough learning data. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))

**Audit check:** is weekly conversion volume ≥50? If not, treat low volume as the root cause and don't over-blame setup.

---

## 5. Creative volume + mix (the biggest lever)

- **Day-one volume:** load **6–10 creative variants**; ideal **15+**. A common initial load is **5–10 images/videos, 3–5 primary text variations, 2–3 headlines**. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))
- **Ongoing:** keep **10–15 active creatives** and add **~3–5 new assets per week**. Only about **6% of ads drive the majority of spend**, so volume is how you find winners. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))
- **Fatigue threshold:** **fewer than 4 creatives → faster fatigue and roughly 20–30% higher CPMs within ~2 weeks.** Stale creative is a top cause of decay. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/), [bir.ch](https://bir.ch/blog/advantage-plus-sales-campaigns-guide))
- **Format mix:** run **static images + video + catalog/dynamic** together and feed diverse copy so the AI has range to test. A missing format is a finding. ([Marpipe](https://www.marpipe.com/blog/what-is-meta-asc-advantage-shopping-campaign), [bir.ch](https://bir.ch/blog/advantage-plus-sales-campaigns-guide))
- **Ceiling:** ASC supports up to **150 creative combinations** — but expert field practice shows strong results with far fewer well-structured ads (e.g. **5–8 ads** split across brand-unaware / brand-aware / conversion-ready), so audit for *quality and coverage*, not just raw count. ([Meta docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns), [Skale Strategy field practice](https://www.skalestrategy.com/blog/meta-advantage-plus-shopping-campaigns-2026))

**Audit checks:** active creative count vs. 4 / 6–10 / 15+ bands; is each of static/video/catalog present? are new assets being added weekly?

---

## 6. Existing-customer budget cap

This is the most common ASC misconfiguration and the one most likely to hide poor incrementality.

- The API field is **`existing_customer_budget_percentage`** (0–100) — it caps the share of budget spent on existing customers. ([Meta docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns))
- **Always set a cap.** Without one, ASC "will spend most of your budget retargeting people who were going to buy anyway — great ROAS numbers but minimal incremental revenue." ([search synthesis / field consensus](https://bir.ch/blog/advantage-plus-sales-campaigns-guide))
- **Recommended cap by intent:**
  - **Prospecting-led / acquisition:** **15–25%** (some accounts run 10–20% to push almost all budget to new customers).
  - **Retention-blended:** up to **25–30%**.
  - Most DTC accounts sit **10–30%**. ([field practice via search synthesis](https://bir.ch/blog/advantage-plus-sales-campaigns-guide))

**Audit checks:** is a cap set at all? Is the percentage consistent with the brand's goal (acquisition vs. retention)? A missing/100% cap is **Critical**; a cap far above intent (e.g. 60% on an acquisition brand) is **High**.

---

## 7. Learning phase + budget-edit discipline

- Respect a full **7-day learning window** before making changes; ideally reach **50+ conversions** before editing. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))
- **Every edit** to budget, creative, or settings during learning **resets** the learning phase. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))
- **Do not edit budget more than once per 72h** during learning. When scaling, go **gradually: 10–20% every few days** — scaling too fast disrupts learning and raises costs. ([bir.ch](https://bir.ch/blog/advantage-plus-sales-campaigns-guide))

**Audit checks:** pull the account **activity log** — how many budget/setting edits in the last 7 days? More than one budget edit per 72h during learning is a finding; big step-changes (e.g. +100% overnight) are a finding.

---

## 8. Creative refresh cadence

- Refresh creative **every 10–14 days** to fight fatigue and keep the algorithm in exploration mode; refresh weekly if fatigue signals appear. Stale creative → worse performance and rising CPMs (see §5). ([bir.ch](https://bir.ch/blog/advantage-plus-sales-campaigns-guide), [alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))

**Audit check:** how long has the current creative set been live with no additions? >14 days with no refresh = finding.

---

## 9. Account structure

- **1–2 ASC campaigns** perform best; avoid running more than **2–3**. Consolidate rather than fragment — fragmentation splits signal. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))
- Ad limits: up to **150 ads** per campaign, with a per-ad-set cap of **50**; a single ad set per ASC. ([bir.ch](https://bir.ch/blog/advantage-plus-sales-campaigns-guide), [Meta docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns))
- Budget-allocation strategy while transitioning: start ASC at **20–30% of total Meta budget** alongside manual campaigns, evaluate over **4–6 weeks**, and scale ASC to **50–70%** only if it matches or beats manual ROAS. ([search synthesis](https://bir.ch/blog/advantage-plus-sales-campaigns-guide))

**Audit check:** how many ASCs run in the account? Is budget fragmented across too many?

---

## 10. Severity rubric (how to score findings)

- **Critical** — blocks scale or corrupts measurement: no existing-customer cap (100%), no catalog/Pixel, CAPI absent on a signal-starved account, <4 creatives.
- **High** — materially limits performance: creative volume below 6–10, missing a format, budget edited >1×/72h in learning, cap far off intent, no refresh in >14 days.
- **Medium** — suboptimal but not blocking: 6–10 creatives (below ideal 15+), attribution window mismatch, borderline SKU count.
- **Low** — polish: minor copy-variation gaps, cosmetic structure notes.

Order findings Critical → Low; always lead with the **top 3 blockers to scale**.

---

## Expert YouTube source

- **"How To Structure Advantage+ Shopping Campaigns in 2024"** — YouTube, published **May 10, 2024** (presenter: Nathan). A DTC-focused SOP walkthrough of ASC structure: single-campaign consolidation, feeding the campaign diverse creatives, setting the **existing-customer budget cap**, respecting the learning phase before editing, and refreshing creative to avoid fatigue. https://www.youtube.com/watch?v=jchorlPUaPM
  - *Note:* YouTube transcripts were not machine-retrievable via automated fetch (only page chrome returned), so the specific numeric thresholds in this KB are corroborated from the written expert sources below rather than quoted from the video. The video is cited as the recognized expert walkthrough of the same setup method. A companion expert perspective on consolidating spend into a single ASC is Charley Tichenor's "The ONE Facebook Campaign You Need To Spend $1M This Year" (https://www.youtube.com/watch?v=BV3xJbykFe0).

---

## Sources

- Meta Marketing API — Advantage+ Shopping Campaigns (official docs): https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns
- Marpipe — What is Meta ASC (Advantage+ Shopping Campaign): https://www.marpipe.com/blog/what-is-meta-asc-advantage-shopping-campaign
- bir.ch — Understanding Meta's Advantage+ Sales Campaigns (guide): https://bir.ch/blog/advantage-plus-sales-campaigns-guide
- Alex Neiman — Meta Advantage+ Shopping: What Actually Drives ROAS: https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/
- Skale Strategy — Meta Advantage+ Shopping Campaigns 2026 (structure/feed/scale, field creative-count practice): https://www.skalestrategy.com/blog/meta-advantage-plus-shopping-campaigns-2026
- Confect.io — ASC best setup / learn from top ecommerce brands: https://confect.io/tactics/advantage-shopping-campaigns-best-setup
- Triple Whale — 4 Things To Consider When Running Advantage+ Shopping Campaigns: https://www.triplewhale.com/blog/meta-advantage-campaigns
- YouTube (expert video) — How To Structure Advantage+ Shopping Campaigns in 2024: https://www.youtube.com/watch?v=jchorlPUaPM
- YouTube (companion expert) — Charley Tichenor, The ONE Facebook Campaign You Need: https://www.youtube.com/watch?v=BV3xJbykFe0
