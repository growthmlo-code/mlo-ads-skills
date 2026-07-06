---
name: meta-asc-auditor
description: Audits a Meta Advantage+ Shopping Campaign (ASC / Advantage+ Sales) against best-practice setup and returns a prioritized, severity-scored findings + fix list. Checks catalog health, Pixel + Conversions API, creative volume and mix, the existing-customer budget cap, learning-phase discipline, budget-edit frequency, and refresh cadence. ALWAYS use this skill when the user says (EN) "audit my Advantage plus", "Advantage+ Shopping audit", "why won't my ASC scale", "review my ASC setup", "diagnose my Advantage+ Sales campaign"; or (ES) "auditar ASC", "auditar mi Advantage plus", "revisa mi Advantage plus", "por qué mi ASC no escala", "diagnóstico ASC de [marca]", "revisa la campaña Advantage+ de [marca]". Trigger on partial or casual asks about an ASC / Advantage+ Shopping / Advantage+ Sales campaign that isn't performing or scaling.
---

# Meta ASC Auditor (Advantage+ Shopping)

## What it does
Pulls the structure, budget, catalog, tracking and creative of a Meta Advantage+ Shopping / Advantage+ Sales campaign and grades it against a best-practice checklist. Outputs a prioritized findings table — each finding gets a severity (Critical / High / Medium / Low), the observed value vs. the benchmark, and a concrete fix. The goal is a one-glance diagnosis of *why an ASC isn't scaling* and an ordered action list to fix it.

## When to use
- User wants a health check on an existing ASC. EN: "audit my Advantage plus", "review my ASC", "why won't my ASC scale". ES: "auditar ASC", "revisa mi Advantage plus", "por qué mi ASC no escala".
- A brand's ASC has flat or falling ROAS, rising CPMs, or is stuck in learning. ES: "diagnóstico ASC de [marca]".
- Before scaling budget on an ASC — verify the setup can take spend first.
- Casual asks: "está bien montada la Advantage+ de X?", "is my Advantage+ Sales campaign set up right?".

## Inputs needed
Ask if missing:
- Which brand / ad account (map to the account IDs in memory, e.g. Meta account for that brand).
- The specific ASC campaign name or ID (an account may run several). If unknown, list Advantage+ Shopping campaigns and confirm.
- Reporting window (default: last 14 days, plus lifetime for learning-status context).
- Store currency/locale (never assume USD — many MLO brands run MXN, COP, EUR, GBP).

## Data sources
- **Meta Ads (primary)** via the `ads_*` Meta Marketing MCP: campaign objective/type, budget (`daily_budget`/`lifetime_budget`), `existing_customer_budget_percentage`, ad set count, ad/creative count, learning status, and linked catalog/pixel. Use `ads_get_ad_entities` / campaign + ad set + ad reads, `ads_catalog_*` for catalog health and diagnostics, and `ads_get_datasets` / `ads_pixel_event_read` for Pixel + Conversions API firing status.
- **Windsor `facebook` connector** as a fallback for spend/CPM/ROAS trend when the MCP metrics are thin.
- **Creative intel (optional)** via Atria in Chrome to judge creative freshness/fatigue beyond raw counts.
- Be honest about gaps: if catalog SKU count or CAPI status can't be read via the connected tools, say so and ask the user to confirm from Commerce Manager / Events Manager.

## Method
1. **Identify the campaign.** Confirm it is a true Advantage+ Shopping / Advantage+ Sales campaign (single ad set, automated audience). If it's a manual Sales campaign the user *thinks* is ASC, flag that first — the checklist below doesn't apply the same way.
2. **Catalog check.** Confirm a catalog is connected and verified, count active SKUs, and pull catalog diagnostics (rejected items, missing fields). Flag if <50 active SKUs or if diagnostics show meaningful rejections.
3. **Tracking check.** Confirm the Pixel fires AND Conversions API is set up and sending (dataset/event quality). Flag if only one is firing, or event match quality is poor.
4. **Creative volume + mix.** Count active ads/creatives in the ASC. Bucket by format (static image / video / catalog-dynamic). Flag low volume (<4 = fatigue risk), sub-ideal volume (<6–10), and missing formats.
5. **Existing-customer budget cap.** Read `existing_customer_budget_percentage`. Judge against intent: prospecting-led acquisition wants a low cap; retention-blended wants higher. Flag a missing/100% cap (no cap = overspend on warm buyers, inflated ROAS, low incrementality).
6. **Learning + budget discipline.** Check learning status and recent budget-edit history from the activity log. Flag budget edits made more than once per 72h during learning, or edits inside the 7-day learning window that reset it.
7. **Refresh cadence.** Look at how long the current creatives have been live and whether new assets are being added. Flag if no refresh in >14 days.
8. **Score + order.** Assign each finding a severity, then sort Critical → Low. Write a fix per finding. Summarize the top 3 blockers to scale.

## Rules & thresholds
- **Catalog:** connected + verified, aim for ≥50 active SKUs; resolve catalog diagnostic rejections before scaling. `pixel_id` is required to run an ASC. ([bir.ch](https://bir.ch/blog/advantage-plus-sales-campaigns-guide), [Meta docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns))
- **Tracking:** Pixel **and** Conversions API both firing; standard ecom attribution 7-day click / 1-day view (7-day click only for high-consideration items over ~$200). ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))
- **Data prerequisite:** ~50+ purchase conversions per week (or ≥50 in the last 30 days) before ASC performs reliably. ([bir.ch](https://bir.ch/blog/advantage-plus-sales-campaigns-guide), [alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/))
- **Creative volume:** 6–10 variants day one; ideal 15+ / run 10–15 active. **<4 creatives → faster fatigue + ~20–30% higher CPMs within 2 weeks.** Add ~3–5 new assets/week. Only ~6% of ads drive most spend, so volume matters. ASC supports up to 150 creative combinations. ([alexneiman.com](https://alexneiman.com/meta-advantage-plus-shopping-campaigns-guide/), [Meta docs](https://developers.facebook.com/documentation/ads-commerce/marketing-api/advantage-shopping-campaigns))
- **Format mix:** run static + video + catalog/dynamic together; a missing format is a finding.
- **Existing-customer budget cap:** set it — never leave it uncapped. Prospecting-led: **15–25%**; retention-blended: up to **25–30%**. Most DTC accounts sit 10–30%. No cap → ASC overspends retargeting warm buyers = high ROAS, low incremental revenue. ([field practice — see KB](reference/knowledge-base.md))
- **Learning phase:** respect a full **7-day** learning window; ideally reach 50+ conversions before editing. Any edit to budget/creative/settings during learning **resets** it.
- **Budget edits:** do **not** edit budget more than once per **72h** during learning; scale gradually at **10–20% every few days**, not in big jumps.
- **Refresh cadence:** refresh creative every **10–14 days** to fight fatigue.
- **Account structure:** 1–2 ASC campaigns perform best; avoid running more than 2–3.

## Output
A findings table plus a top-3 summary. Concrete shape:

```
ASC Audit — [Brand] — [Campaign name] — window [dates] — currency [XXX]

Top 3 blockers to scale:
1. No existing-customer cap → burning budget on warm buyers.
2. Only 3 active creatives → fatigue + rising CPMs.
3. Budget edited 4× in last 5 days → learning never stabilized.

| # | Area              | Observed          | Benchmark            | Severity | Fix                                   |
|---|-------------------|-------------------|----------------------|----------|---------------------------------------|
| 1 | Existing-cust cap | not set (100%)    | 15–25% prospecting   | Critical | Set cap to 20% in campaign settings   |
| 2 | Creative volume   | 3 active          | 6–10 (ideal 15+)     | High     | Add 5–7 assets; mix video + static    |
| 3 | Learning edits    | 4 budget edits/5d | ≤1 per 72h           | High     | Freeze budget 7d; then +15%/3d         |
| 4 | Catalog SKUs      | 62 active, 0 rej. | ≥50, no rejections   | OK       | —                                     |
| 5 | Tracking          | Pixel only        | Pixel + CAPI         | High     | Enable Conversions API                |
```

Deliver in chat by default. If the user asks, also draft it into the brand's Notion page or a Slack draft to the client channel (respect ES/EN by brand). Never auto-apply changes.

## Guardrails
- **Read-only by default.** This skill diagnoses; it does not change the campaign. Never edit budget, cap, or creatives without showing the fix list and getting explicit confirmation.
- **Respect currency/locale.** Report spend/CPM in the account's native currency; MLO brands run MXN, COP, EUR, GBP — do not convert or assume USD.
- **Don't reset learning yourself.** If you propose a fix that would reset learning, say so explicitly so the user chooses the timing.
- **Distinguish correlation from setup.** Flat ROAS can be creative, offer, or seasonality — not just setup. Note when a finding is a hypothesis vs. a hard misconfiguration.
- **Confirm ASC type.** If the campaign isn't actually Advantage+ Shopping/Sales, say so before applying this checklist.

## References
See [reference/knowledge-base.md](reference/knowledge-base.md) for the full cited criteria, benchmarks, and sources (including the expert YouTube video).
