---
name: google-pmax-auditor
description: >
  Runs a structured audit of a Google Ads Performance Max (PMax) campaign and outputs a
  prioritized findings + fix list scored by severity — asset-group coverage & Ad Strength,
  search themes, audience signals, brand exclusions & Search cannibalization, budget pacing
  & tROAS, layered negatives, Final URL expansion, and listing-group/feed health for retail.
  ALWAYS use this skill when the user asks (ES or EN) to "auditar PMax", "PMax audit",
  "revisa mi Performance Max", "por qué PMax gasta mal / gasta de más", "diagnóstico PMax de
  [marca]", "audita la campaña de Performance Max de X", "qué le pasa a mi PMax", "PMax está
  canibalizando la Search", "review my Performance Max", "check my PMax asset groups /
  search themes / audience signals", or asks why a PMax campaign is wasting budget or
  underperforming. Trigger on partial/casual asks too (e.g. "algo raro pasa con la PMax de X").
---

# Google Performance Max Auditor

## What it does
Audits one Performance Max campaign end to end and returns a prioritized, severity-scored
findings table with a concrete fix for each issue. It checks the eight inputs that actually
move PMax performance (assets, search themes, audience signals, brand exclusions,
budget/tROAS, negatives, Final URL expansion, feed/listing groups) and flags waste and
Search-campaign cannibalization using the PMax Search Terms Report (live since March 2025).

## When to use
- The user wants a health check / diagnosis of a PMax campaign.
  - ES: "auditar PMax", "revisa mi Performance Max", "por qué PMax gasta de más", "diagnóstico PMax de [marca]", "la PMax está canibalizando la Search".
  - EN: "PMax audit", "review my Performance Max", "why is PMax wasting budget", "audit the PMax for [brand]".
- Spend is up but conversions/ROAS are flat or dropping in a PMax campaign.
- Before scaling budget on a PMax campaign, or when handing an account to/from a client.

## Inputs needed
Ask for whatever is missing:
- Brand name and which Google Ads account/customer ID (or let the connector list them).
- The specific PMax campaign to audit (name or ID). If unknown, list PMax campaigns first.
- Target tROAS (or target CPA) and account currency/locale — needed to judge pacing.
- Whether the brand runs separate brand/non-brand Search campaigns (for cannibalization check).
- Retail vs lead-gen (retail adds the Merchant Center / listing-group / feed checks).
- Reporting window (default: last 30 days; use 90 days for low-volume accounts).

## Data sources
- **Google Ads** via the Windsor.ai connector `google_ads` (or a Google Ads MCP if connected):
  pull campaign spend/conversions/ROAS, asset-group list, asset counts & Ad Strength, search
  themes, audience signals, the **PMax Search Terms Report**, campaign & account negatives,
  Final URL expansion setting, and listing-group / product-status data for retail.
- **Shopify MCP** (retail): cross-check feed/product availability and top sellers if Merchant
  Center data is thin.
- Be honest about gaps: PMax reporting hides asset-group-level search terms and channel-level
  spend detail. If a data point isn't exposed by the connector, say so and inspect it in the
  Google Ads UI (Insights & reports → Search terms; Asset group → View details) instead of
  guessing.

## Method
Do these in order. Record every finding with a severity (High / Med / Low) and a one-line fix.

1. **Scope & baseline.** Confirm the campaign, window, tROAS/tCPA target, currency, and
   retail-vs-lead-gen. Pull campaign spend, conversions, conv. value, ROAS, CPA. This is the
   yardstick everything else is measured against.
2. **Asset coverage & Ad Strength (per asset group).** For each asset group count text/image/
   video slots filled vs the maximums (15 headlines, 5 long headlines, 5 descriptions, 20
   images, up to 5 videos). Flag any group that is thin (few headlines, one image, no video)
   or below **"Excellent" Ad Strength**. Missing image ratios (1.91:1 landscape, 1:1 square,
   4:5 portrait) and missing video are High severity.
3. **Search themes.** Confirm each asset group has relevant search themes (up to **50 per
   asset group**). Check the "usefulness" indicator; flag themes marked low-usefulness and
   any group with zero themes. Irrelevant themes that pull junk traffic = Med/High.
4. **Audience signals.** Confirm signals are attached and are quality (Customer Match /
   converters / custom segments built from real converting search terms — not a generic
   interest). Signals are hints, not restrictions; a missing or generic signal slows learning.
5. **Brand exclusions & cannibalization.** Check brand exclusions are set correctly relative
   to whether brand traffic should live in Search or PMax. Then open the **PMax Search Terms
   Report** and compare against brand/non-brand Search campaigns: if PMax is eating brand
   queries that a cheaper brand Search campaign should win, flag it High.
6. **Budget pacing & bidding.** Compare daily budget to spend and to target. Rule of thumb:
   daily budget ≈ **3× target CPA**; if budget-constrained or lost-IS-budget is high, note it.
   Check tROAS/tCPA isn't set so aggressively it throttles delivery in learning, and that
   tROAS reflects rule-adjusted conversion values, not raw.
7. **Negatives, layered.** Verify negatives exist and are layered: **Master shared list**
   (brand-safety / always-off terms) → **campaign-level** negatives (up to 10,000/campaign)
   → **surgical** additions from this week's search terms. Account-level negatives (max 1,000)
   apply automatically. No negatives on a spending PMax = High.
8. **Final URL expansion.** Confirm it's ON with URL exclusions for pages you don't want
   (cart, account, blog, out-of-stock) — or intentionally OFF. Unbounded expansion sending
   traffic to junk URLs = Med.
9. **Listing groups / feed health (retail only).** Check Merchant Center is linked, top
   sellers are approved and in stock, listing groups aren't dumping budget into one SKU, and
   feed titles/custom labels are populated. Disapprovals or out-of-stock top sellers = High.
10. **Score & assemble.** Roll every finding into the output table, ordered High → Med → Low,
    each with evidence (the number) and the exact fix. Lead with the 1–3 highest-impact fixes.

## Rules & thresholds
- **Negative keyword limits:** up to **10,000 per PMax campaign** (raised from 100 on
  2025-03-11); **shared negative lists** supported for PMax (rollout completed Aug 2025);
  **account-level negatives max 1,000**. Negatives apply to **Search & Shopping inventory
  only** — not YouTube/Display/Gmail/Discover.
- **PMax Search Terms Report:** live since **March 2025**; gives impressions, clicks, CTR,
  conversions, conv. rate, CPA, ROAS per query — but **no asset-group breakdown**.
- **Search themes:** up to **50 per asset group** (raised from 25 in 2025).
- **Asset maximums per asset group:** 15 headlines, 5 long headlines, 5 descriptions, 20
  images, up to 5 videos. Aim for **Excellent** Ad Strength (moving Good→Excellent lifts
  conversions ~6% on average).
- **Budget:** daily budget ≈ **3× target CPA**; allow **4–6 weeks / enough conversions** in
  learning before judging or changing targets.
- **Audience signals** are directional hints, not hard targeting — never treat them as
  restrictions.
- **Prerequisite reality check:** PMax needs solid conversion data. If the account has thin
  conversion history, flag that PMax may be premature vs Search/Shopping first.

## Output
A markdown (or Notion) **audit table**, findings ordered by severity, e.g.:

| # | Area | Finding (evidence) | Severity | Fix |
|---|------|--------------------|----------|-----|
| 1 | Negatives | 0 negatives on campaign spending $1.4k/30d; PMax Search Terms shows "free", "cheap", competitor terms | High | Attach Master negative list + add 12 surgical negatives (listed) |
| 2 | Cannibalization | PMax captured 63% of brand-term conversions vs brand Search | High | Enable brand exclusions on PMax; route brand to Search |
| 3 | Assets | Asset group "Core" has 3 headlines, 1 image, no video → Ad Strength "Average" | High | Add 12 headlines, 5 images (all ratios), 1 video → target Excellent |
| 4 | tROAS | tROAS 5.0 set; account averages 3.2 → budget-constrained, delivery throttled | Med | Lower tROAS to ~3.5 during learning, re-raise after 30d |

Follow the table with a **Top 3 fixes** summary and, if the user wants, a Notion page or a
Slack draft for the brand channel (write in the brand's language — ES for most MLO brands).

## Guardrails
- **Read-only by default.** Never bulk-apply changes (pause groups, edit budgets/tROAS, add
  negatives at scale) without showing a preview and getting explicit confirmation.
- **Respect currency/locale.** Use the account's real currency; write ES for ES brands.
- **Don't invent Google Ads fields or metrics.** If the connector doesn't expose something
  (e.g. asset-group-level search terms), say so and point to the Google Ads UI location.
- **One campaign at a time.** Audit and report per campaign; don't blend PMax campaigns.
- **Correlation ≠ cause.** Flag cannibalization/waste as hypotheses backed by the numbers,
  not certainties, before recommending structural changes.

## References
See `reference/knowledge-base.md` for the sourced expert criteria, thresholds, and all URLs.
