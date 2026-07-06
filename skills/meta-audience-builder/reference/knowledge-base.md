# Meta Audience Builder — Knowledge Base

Distilled, cited expertise for designing a DTC Meta audience strategy in 2025–2026. Every threshold below has a source URL. This is the auditable layer behind `SKILL.md`.

---

## 1. The 2025 targeting changes (why old playbooks break)

Meta materially changed how targeting and exclusions work in 2025. Any pre-2025 audience playbook that relies on narrow interest stacks or detailed-targeting exclusions is now partly broken.

- **Detailed-targeting exclusions removed from Ads Manager: March 2025.** You can no longer exclude an interest/behavior at the detailed-targeting level. ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))
- **Interest consolidation began June 23, 2025.** Meta folded specific interest categories (e.g. "EDM fans", "SUVs", "vegan food") into broader groupings, eliminating granular interest stacking. ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))
- **Detailed-targeting exclusions removed from boosted posts: June 2025.** ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))
- **January 15, 2026:** active campaigns still using discontinued interests stopped delivering unless the targeting was updated. ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))

**Consequence for exclusions:** to suppress recent purchasers or existing customers you must now use a **custom audience placed in Audience Controls**, not an interest-based/detailed-targeting exclusion. ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))

---

## 2. How Advantage+ Audience actually works

Advantage+ Audience is Meta's AI-driven audience mode — "you are now handing the keys to Meta's AI and letting it find the right people for you." ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))

- **Only two hard constraints:** location and minimum age. Everything else (interests, custom audiences, lookalikes) is a **soft suggestion / starting hint** that the algorithm can and will expand beyond to find higher-performing users. ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/), [adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))
- **"Advantage detailed targeting" expansion is on by default** — you must explicitly opt out to keep strict audience controls. The algorithm draws on cross-advertiser conversion patterns that no manual interest stack can replicate. ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))
- **Lookalikes inside Advantage+ act as "optimization hints,"** not hard walls — used as starting signals, then expanded past. ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))
- Practitioner note: in-platform audiences (e.g. FB/IG engagers over 90 days) have been observed to outperform client-provided email lists and pixel data as Advantage+ signals. ([optmyzr](https://www.optmyzr.com/blog/meta-ads-targeting-strategies/))

---

## 3. Broad / Advantage+ vs interest targeting — when each wins

### Use broad / Advantage+ when (scaling)
- **50+ purchase conversions per week per ad set** (Meta's optimization threshold). ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026), [conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))
- **$50–$100+/day budget** to clear the learning phase. ([turbamedia](https://turbamedia.io/post/broad-targeting-vs-interest-targeting---the-definitive-2025-guide))
- Clean conversion signal (Pixel + CAPI) on a valuable event (purchase/lead). ([turbamedia](https://turbamedia.io/post/broad-targeting-vs-interest-targeting---the-definitive-2025-guide))
- Product has broad appeal, and **5–10 distinct creative concepts** ready to test. ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))
- Tolerance for 3–7 days of volatile learning-phase performance. ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))

### Use interest / detailed / hybrid when (cold-start)
- Fewer than **20–50 weekly conversions**. ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026), [conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))
- **Daily budget under ~$30 per ad set.** ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/), [adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))
- Hyper-niche (~0.1% of user base), regulated verticals (healthcare, finance), hyper-local, or brand-new markets with zero pixel history. ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/), [adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))
- Interest targeting also stays useful for **building lookalike seed audiences** and for early testing to validate core interests. ([turbamedia](https://turbamedia.io/post/broad-targeting-vs-interest-targeting---the-definitive-2025-guide))

### Performance you can expect
- Advantage+ / broad: up to **32% lower CPA** in ecommerce, **11–15% higher CTR**, 13% lower cost per catalog sale, 7% lower cost per conversion vs manual targeting. ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))
- DTC accounts with established pixel data see **15–30% lower CPA** vs interest stacks; broad often shows higher CPM but lower CPA (higher-intent user identification). ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))

---

## 4. Learning phase and budget mechanics

- Ad sets need roughly **50 conversions/week** to exit the learning phase and stabilize. ([conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/))
- Broad campaigns need **$50–$100+/day** to gather enough signal to navigate learning. ([turbamedia](https://turbamedia.io/post/broad-targeting-vs-interest-targeting---the-definitive-2025-guide))
- During the initial learning window, allocating **120–150% of target daily budget** can accelerate algorithm calibration. ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))
- Broad with a single creative starves the test — pair broad with 5–10 concepts (competitive cadence 10–15/month; aggressive scaling 20+). ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))

---

## 5. Lookalike audiences

- **Minimum source: 100 people from one country.** Technically valid but too thin — not enough signal for the algorithm. ([optmyzr](https://www.optmyzr.com/blog/meta-ads-targeting-strategies/), [flighted](https://www.flighted.co/blog/meta-lookalike-audiences-complete-guide))
- **Recommended source: 1,000–5,000 people** for stable results; **5,000–10,000 is the quality sweet spot**; 10,000+ optimal for broad 5–10% lookalikes. ([flighted](https://www.flighted.co/blog/meta-lookalike-audiences-complete-guide), [adnabu](https://blog.adnabu.com/facebook/facebook-lookalike-audiences/))
- **Start at 1%** (closest match to seed), then gradually test larger % for more reach/volume. ([optmyzr](https://www.optmyzr.com/blog/meta-ads-targeting-strategies/))
- Prefer **high-intent seeds** (purchasers, high-AOV customers, high-value events) over generic engagers for a cleaner lookalike.
- In 2025+, lookalikes are most useful as a **cold-start seed / hint** — inside Advantage+ they are expanded past, not enforced. ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))

---

## 6. Custom audiences & retargeting

Common custom-audience seeds for prospecting-signal and retargeting: website visitors, leads, newsletter subscribers, customers, product-catalog viewers, Facebook engagers, Instagram engagers. ([optmyzr](https://www.optmyzr.com/blog/meta-ads-targeting-strategies/))

- Retargeting is a **separate budget tier — typically 10–20% of total budget.** ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))
- Use a **longer lookback window** so the pool is large enough for the system to serve efficiently. ([optmyzr](https://www.optmyzr.com/blog/meta-ads-targeting-strategies/))
- Post-privacy changes, exclusions are less surgically powerful than in the hyper-segmentation era, but still matter for suppressing recent purchasers and preventing fatigue. ([optmyzr](https://www.optmyzr.com/blog/meta-ads-targeting-strategies/))

---

## 7. Budget allocation for a scaling DTC account

A typical mature-account split: **70–80% broad/Advantage+, 10–20% retargeting, 5–10% interest/lookalike testing.** New accounts with zero pixel data should seed with interest-targeted or lookalike-seeded campaigns for **2–4 weeks** to build conversion signal, then transition to broad. ([adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026))

---

## 8. Decision tree by account maturity

```
START → How many purchase conversions/week per ad set? And budget/ad set?

├─ COLD-START  (<20–50 conv/wk  OR  <$30–50/day/ad set  OR  new pixel/market)
│   → Prospecting core: 1–2 INTEREST or LOOKALIKE layers (focused starting signal)
│   → Lookalike only if a seed ≥100 (ideally 1,000–5,000+) exists; start 1%
│   → Small retargeting tier if any site/engagement pool exists
│   → Exclude purchasers via CUSTOM AUDIENCE
│   → After 2–4 weeks of signal → graduate to broad
│
└─ SCALING  (50+ conv/wk/ad set  AND  $50+/day)
    → Prospecting core: BROAD / ADVANTAGE+ AUDIENCE (70–80% budget)
       interests/lookalikes only as hints; keep 5–10 creatives live
    → Lookalike/interest testing tier: 5–10% budget
    → Retargeting tier: 10–20% budget
    → Exclude recent purchasers via CUSTOM AUDIENCE (30–180d)
    → Push learning budget to 120–150% of target early, then normalize
```
Sources: [conversios](https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/), [adligator](https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026), [turbamedia](https://turbamedia.io/post/broad-targeting-vs-interest-targeting---the-definitive-2025-guide), [optmyzr](https://www.optmyzr.com/blog/meta-ads-targeting-strategies/).

---

## 9. DTC / MLO application notes

- Convert all $ thresholds to the account's currency (EUR/USD/MXN/COP/GBP) before advising — a $50/day floor is intent, not a literal figure for a MXN account.
- Seed lookalikes from the **Shopify purchaser list** (via Shopify MCP `list-customers`) when the pixel purchaser pool is small; confirm the list clears the 1,000+ recommendation.
- For small ES/EU niche brands (common in MLO's book), cold-start with 1–2 interest layers is usually correct — don't force broad on a €20/day ad set.
- Always show the audience plan and get approval before creating/uploading any custom audience (data + consent).

---

## Expert video source (YouTube)

- **"The ONLY Meta Ads Targeting Tutorial You Need" (2025/2026), Lyfe Marketing** — https://www.youtube.com/watch?v=-CsBl3tv-X0
  Covers the same 2025 shift used above: Advantage+ Audience as default, broad-over-interest for accounts with signal, and using custom audiences for exclusions. *Note: YouTube transcripts are not machine-retrievable via the fetch tool used here, so this video is cited as an expert reference and its recommendations were cross-checked against the written expert sources below (Jon Loomer's Meta targeting guidance and the four anchor blogs).* Jon Loomer (jonloomer.com) is the widely recognized Meta Ads authority whose 2026 targeting guidance aligns with these thresholds.

---

## Sources

- Conversios — Meta Advantage+ Audience vs Detailed Targeting: 2026 Guide: https://www.conversios.io/blog/meta-advantage-audience-vs-detailed-targeting-2026-guide/
- Turba Media — Broad Targeting vs Interest Targeting: The Definitive 2025 Guide: https://turbamedia.io/post/broad-targeting-vs-interest-targeting---the-definitive-2025-guide
- Optmyzr — Meta Ads Targeting Strategies: https://www.optmyzr.com/blog/meta-ads-targeting-strategies/
- Adligator — Meta Broad Targeting & Advantage+ Audiences 2026: https://adligator.com/blog/meta-broad-targeting-advantage-plus-audiences-2026
- Flighted — Meta Lookalike Audiences: Complete Guide for 2026: https://www.flighted.co/blog/meta-lookalike-audiences-complete-guide
- AdNabu — How To Use Facebook Lookalike Audiences (2026): https://blog.adnabu.com/facebook/facebook-lookalike-audiences/
- Jon Loomer — A Guide to Meta Ads Targeting in 2026: https://www.jonloomer.com/meta-ads-targeting-2026/
- YouTube (Lyfe Marketing) — The ONLY Meta Ads Targeting Tutorial You Need: https://www.youtube.com/watch?v=-CsBl3tv-X0
