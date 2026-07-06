---
name: meta-audience-builder
description: Designs a Meta (Facebook/Instagram) audience strategy for a DTC brand — recommends the right mix of broad / Advantage+ Audience / interest / lookalike / custom audiences plus the correct exclusions, calibrated to the ad account's maturity, conversion signal and budget. Encodes the 2025 changes (Meta consolidated detailed interests and REMOVED detailed-targeting exclusions, so recent-purchaser suppression now needs CUSTOM AUDIENCE exclusions). ALWAYS use this skill when the user asks (ES or EN): "estrategia de audiencias Meta", "qué audiencias uso", "broad vs intereses", "broad vs interest targeting", "lookalike de [marca]", "cómo targeteo en Meta", "how do I target on Meta", "Advantage+ audience o intereses", "a quién le pongo los anuncios", "audiencias para escalar", "audience strategy for [brand]", "should I use broad or Advantage+". Trigger on casual/partial asks about who to target, exclusions, lookalikes or audience layering for any DTC brand.
---

# Meta Audience Builder

## What it does
Produces a concrete, account-specific Meta audience plan for a DTC brand: which audience type to run at each ad set (broad, Advantage+ Audience, interest, lookalike, custom/retargeting), which exclusions to apply, how to split budget, and a decision tree keyed to the account's maturity (cold-start vs scaling). It reflects Meta's 2025 targeting changes so the recommendations are still valid — most importantly, that exclusions of recent purchasers now require custom audiences, not detailed-targeting exclusions.

## When to use
- User asks how to target on Meta: "qué audiencias uso", "cómo targeteo en Meta", "how do I target on Meta".
- The broad-vs-interest debate: "broad vs intereses", "broad vs interest targeting", "¿pongo Advantage+ o intereses?".
- Building or seeding a lookalike: "lookalike de [marca]", "seed audience para lookalike".
- Setting up exclusions: "cómo excluyo compradores", "how do I exclude recent buyers".
- Scaling / restructuring: "audiencias para escalar", "audience strategy for [brand]", "reestructurar audiencias".

## Inputs needed
Ask for whatever is missing before recommending:
1. **Brand + Meta ad account** (account ID, market/country, currency/locale — ES/EN, EUR/USD/MXN/COP/GBP).
2. **Daily budget** at the account and per-ad-set level.
3. **Account maturity signal**: weekly purchase conversions (pixel), pixel/CAPI age, prior audience structure.
4. **Custom-audience seeds available**: pixel events, Shopify customer/purchaser list size, IG/FB engagers, video viewers.
5. **Goal**: cold-start (first profitable spend) vs scaling an already-profitable account.

## Data sources
- **Meta Ads** via the `ads_*` Meta Marketing MCP: `ads_get_ad_account_custom_audiences` / `ads_get_custom_audience` (existing custom audiences + sizes), pixel/dataset signal via `ads_get_datasets` / `ads_get_dataset_stats` / `ads_get_dataset_quality`, and account structure via `ads_get_ad_entities`. Weekly conversion volume and CPA from account insights. Use `ads_create_custom_audience` / `ads_update_custom_audience_users` only after the user approves.
- **Windsor `facebook`** connector as an alternative for account-level spend/conversion pulls.
- **Shopify MCP** (`list-customers`) to size a customer/purchaser list for a custom-audience or lookalike seed. Honest note: pushing a customer list into Meta as a custom audience requires the Meta MCP's audience tools (and the brand's data/consent) — flag if that connection isn't set up.
- **Atria (Chrome)** optional, only to sanity-check which creative angles map to which audience intent.

## Method
1. **Read the account's current state.** Pull existing custom audiences (names, sizes, retention windows), pixel/dataset quality, weekly purchase volume, and per-ad-set budget. Note the market and currency.
2. **Classify maturity** using the decision tree in Rules & thresholds: cold-start (low/no signal, <20–50 conv/wk, or <$30–50/day/ad set) vs scaling (50+ purchases/wk/ad set and $50+/day).
3. **Pick the prospecting core:**
   - **Scaling account →** default to **broad / Advantage+ Audience** as the primary prospecting engine (70–80% of budget). Provide interest/lookalike names only as *suggestions/hints* — the system expands past them.
   - **Cold-start account →** start with **1–2 interest or lookalike layers** to give the algorithm a focused starting direction and reach the learning-phase conversion volume faster; plan to graduate to broad once signal builds (typically 2–4 weeks).
4. **Design the lookalike layer (if seed exists).** Confirm the seed audience meets the size floor (min 100 from one country; recommend 1,000–5,000+). Start at 1% LAL, then test larger % for reach. Prefer high-intent seeds (purchasers, high-AOV customers) over generic engagers.
5. **Design the retargeting tier.** Custom audiences from site visitors, ATC/IC, catalog viewers, IG/FB engagers, customer list. Allocate ~10–20% of budget. Keep windows long enough for a usable pool.
6. **Set exclusions the 2025 way.** To suppress recent purchasers/existing customers, add a **CUSTOM AUDIENCE exclusion** in Audience Controls — detailed-targeting exclusions were removed (Ads Manager Mar 2025, boosted posts Jun 2025) and no longer exist. Exclude retargeting audiences from prospecting to avoid overlap.
7. **Allocate budget** by tier and write the plan as an ad-set-level table (see Output). State which audiences to build vs already exist.
8. **Confirm before creating anything.** Show the plan; only build custom audiences after explicit approval.

## Rules & thresholds
- **Advantage+ Audience = full AI mode.** Only *location and minimum age* are hard constraints; interests, lookalikes and custom audiences entered are **suggestions/hints**, and Meta expands beyond them. [conversios, adligator]
- **Broad / Advantage+ works best when:** 50+ purchase conversions/week per ad set, clean pixel/CAPI signal, **$50+/day per ad set** ($50–$100+/day to clear the learning phase), and 5–10 distinct creatives ready. [turbamedia, adligator, conversios]
- **Use interest / detailed targeting for cold-start:** new accounts, <20–50 weekly conversions, **budget under ~$30/day per ad set**, hyper-niche/regulated verticals, or new markets with no pixel history. [conversios, adligator]
- **Learning phase:** ad sets need ~50 conversions/week to exit learning and stabilize. During initial learning, ~120–150% of target daily budget can accelerate calibration. [adligator]
- **Lookalike source size:** minimum **100 people from one country**; **1,000–5,000 recommended** for stable results (5,000–10,000 is the quality sweet spot). Start at **1% LAL**, then scale %. [optmyzr, flighted, adnabu]
- **Exclusions (2025 change):** detailed-targeting exclusions were **removed** — Ads Manager **March 2025**, boosted posts **June 2025**. Suppress recent purchasers/customers with a **custom-audience exclusion** only. Meta also consolidated granular interests into broader groups (rolled out from June 2025), so narrow interest stacks no longer work. [conversios, adligator]
- **Budget split (scaling account):** ~70–80% broad/Advantage+, ~10–20% retargeting, ~5–10% interest/lookalike testing. [adligator]
- **Expected lift:** DTC accounts with pixel history often see ~15–32% lower CPA on Advantage+/broad vs interest stacks; broad often shows higher CPM but lower CPA. [conversios, adligator]

## Output
A short written recommendation plus an **ad-set-level plan table**, and a flagged list of audiences to build vs. existing. Example shape:

| Ad set | Audience type | Definition / seed | Exclusions | Budget/day | Notes |
|---|---|---|---|---|---|
| Prospecting-Broad | Advantage+ Audience | Location ES, 18+, no interests | Purchasers-180d (custom) | €40 | Primary engine, 70% |
| LAL-1%-Purchasers | Lookalike 1% | Seed: Shopify purchasers (2,300) | Purchasers-180d | €10 | Seed ≥ min; scale % if wins |
| Retargeting-ATC | Custom (ATC 14d) | Site ATC last 14d | Purchasers-30d | €8 | ~15% of budget |

Close with: (a) the maturity verdict (cold-start vs scaling), (b) the 2025 exclusion note, (c) next step (which custom audiences to create, pending approval). Deliver in the account's language (ES/EN) and currency.

## Guardrails
- **Never create, modify, or push a custom audience / customer list without showing a preview and getting explicit confirmation** — customer-list uploads carry data/consent implications.
- **Do not recommend detailed-targeting exclusions** — they no longer exist post-2025. Always route purchaser suppression through custom audiences.
- **Respect account currency and locale** ($/€/MXN/COP/GBP; ES vs EN). Never quote USD thresholds to a EUR/MXN account without converting the intent.
- **Don't over-segment.** With Advantage+/broad, stacking many narrow interests fights the algorithm; suggestions are hints, not walls.
- **Verify seed size before proposing a lookalike** — a 100-person seed is technically valid but too thin; flag it and recommend 1,000+.
- Match creative volume to a broad strategy (5–10+ concepts); broad with one creative starves the test.

## References
See `reference/knowledge-base.md` for the full cited knowledge base (all thresholds, the 2025 change timeline, and source URLs).
