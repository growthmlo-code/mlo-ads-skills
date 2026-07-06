---
name: google-shopping-feed
description: >
  Audits and optimizes a Google Merchant Center product feed end-to-end — titles, GTIN/identifiers,
  required attributes, images, and custom labels — to clear disapprovals and lift Shopping/PMax
  visibility. Cross-checks GMC feed data against the live Shopify catalog and returns a prioritized
  fix list plus rewritten, front-loaded titles. ALWAYS use this skill when the user says "optimizar el
  feed", "revisa/audita el feed", "Merchant Center", "GMC", "shopping feed de [marca]", "por qué me
  rechazan productos en GMC / en Merchant Center", "productos desaprobados", "mejorar/optimizar títulos
  de shopping", "fix my feed", "product disapprovals", "GTIN", "custom labels", "google_product_category",
  or asks why Shopping/PMax impressions are low for a brand. Trigger on partial or casual asks like
  "arréglame el feed de X" or "por qué no salen mis productos en Google".
---

# Google Shopping Feed Optimizer

## What it does
Runs a structured audit of a brand's Google Merchant Center feed and returns (1) a prioritized fix list of disapprovals and missing/weak attributes, and (2) rewritten, front-loaded product titles built from the attributes shoppers actually search. It cross-references GMC feed fields against the live Shopify catalog so mismatches (price, availability, GTIN, brand) get caught before they cause suspensions. The goal is more approved products and higher Shopping/PMax impression share and CTR.

## When to use
- "Optimizar el feed" / "revisar el feed de [marca]" / "fix / audit my feed".
- "Merchant Center" / "GMC" / "por qué me rechazan productos" / "productos desaprobados" / "product disapprovals".
- "Mejorar / optimizar títulos de shopping" / "rewrite my product titles".
- Questions about GTIN, MPN, `identifier_exists`, `google_product_category`, `product_type`, or custom labels.
- Shopping or PMax impressions/CTR are low for a brand and the feed is a suspected cause.

## Inputs needed
Ask only for what's missing:
- Brand + Shopify store handle (for the catalog side).
- Access to the GMC feed data (an export/CSV, the Diagnostics tab screenshot, or the primary-feed contents). If the user can't share GMC directly, work from the Shopify catalog and flag which checks need the GMC side.
- Target country / currency / language (drives locale rules — never assume USD/EN; MLO brands run ES/EN, EUR/USD/MXN/COP/GBP).
- Optional: margin / bestseller / seasonality data to populate custom labels.

## Data sources
- **Shopify catalog** via the Shopify MCP (`get-product`, `search_products`, `graphql_query`): pull `title`, `product_type`, `vendor` (brand), `barcode` (GTIN), variant `price`, `inventory`/availability, and image URLs. This is the source of truth for price/availability/GTIN consistency checks.
- **Google Merchant Center feed data**: the user must provide it — a Content API export, a feed CSV, or the Diagnostics view. There is no first-party GMC MCP in this stack; be honest that the GMC-side pull depends on what the user shares. If GMC data isn't available, audit the Shopify catalog and mark GMC-only checks (disapproval reasons, item-level issues) as "needs GMC export."
- Google product taxonomy (for `google_product_category` IDs) is a public reference file — look up the correct category ID when recategorizing.

## Method
1. **Scope.** Confirm brand, Shopify handle, target country/currency/language, and how the GMC feed will be provided. Pull the Shopify catalog.
2. **Required-attribute completeness check.** For every product verify the required set is present and valid: `id`, `title`, `description`, `link`, `image_link`, `price`, `availability`, `brand`, `gtin` (or `mpn`), `product_type`, `google_product_category`, `condition`. Flag any missing.
3. **Consistency check (GMC vs Shopify vs landing page).** Compare `price`, `availability`, `brand`, and `gtin` across feed and Shopify. Any mismatch = disapproval risk; list each.
4. **Disapproval triage.** From the GMC Diagnostics data, group item-level issues by cause (price mismatch, image quality/promo overlay, missing/invalid GTIN, availability mismatch, policy/prohibited content, missing identifiers). Map each to its fix (see Rules). Order by product value: high-margin / bestseller SKUs first.
5. **GTIN / identifier logic.** For each product: if a manufacturer-assigned GTIN exists (Shopify `barcode`), require it, strip dashes/spaces, and validate length (8/12/13/14 digits, check digit). Never fabricate a GTIN. Only set `identifier_exists=false` for genuinely custom/handmade/vintage or exclusive products with no GTIN/MPN — never as a shortcut to hide a missing one.
6. **Title rewrite.** Rewrite weak titles using the category formula (Brand + Product Type + key attributes), most-important words first, all decision attributes (size/color/style/gender/model/material) inside the first ~70 chars, ≤150 chars total, same language as the feed locale. Strip promo/CAPS/keyword-stuffing.
7. **Category + product_type.** Assign the correct `google_product_category` ID (don't rely on auto-assignment for niche items) and set a granular `product_type` hierarchy (levels split by `>`) to enable bidding segmentation.
8. **Custom labels.** Propose values for `custom_label_0–4` from margin / bestseller / season / price-range / promo so campaigns can bid by segment.
9. **Deliver.** Output the prioritized fix list + rewritten titles as a table; hand off changes as a preview for the user to apply (or paste back into the feed rules / Shopify metafields). Never bulk-edit without confirmation.

## Rules & thresholds
- **Title:** ≤150 chars; front-load the first ~70 chars (only ~30–35 render in the ad on mobile) with the most important, most-searched words. Feed titles should differ from page titles — 81% of high-performing advertisers use more keyword-optimized feed titles. No promo language, no ALL CAPS, no keyword stuffing; numerals not spelled-out numbers.
- **Title structure by category:** Apparel = Brand + Gender + Product Type + Attribute + Color + Size; Electronics = Brand + Model + Product Type + Key Specs; Beauty = Brand + Product Type + Benefit + Size/Shade; Home = Brand + Material + Product Type + Style + Size.
- **GTIN:** required when manufacturer-assigned; submit **without dashes or spaces**, keep leading zeros, valid GS1 check digit. Correct GTINs are worth ~20% more clicks on average. Wrong/fabricated GTINs → disapproval and possible account suspension.
- **identifier_exists=false:** only for products that genuinely have no GTIN/MPN/brand (custom, handmade, vintage, store-exclusive). Misusing it is a disapproval risk.
- **Images:** main image on white/solid background, product filling ~75–90% of the frame, no text/watermark/promo overlay; ≥800×800px recommended (Google enforces a 500×500 minimum from Jan 31, 2027). Don't upscale or submit thumbnails.
- **Description:** ≤5000 chars, plain text, matches the landing page, no promo/shipping claims.
- **Consistency:** `price` and `availability` in the feed must match Shopify and the landing page exactly (same currency, ISO 4217, period decimal) — the #1 disapproval cause.
- **Language:** all attribute values in the feed's target language; don't mix ES/EN inside one feed.
- **Custom labels:** up to 5 (`0–4`), 100 chars each, max 1,000 unique values per label — use for margin, bestseller/performance tier, season, price range, promo.

## Output
A prioritized audit deliverable, e.g.:

**1. Disapproval fixes (by priority)**

| SKU / id | Issue | Cause | Fix | Priority |
|---|---|---|---|---|
| SKU-102 | Disapproved | Price mismatch (feed 29€ vs Shopify 34€) | Sync price via automatic item updates | High (bestseller) |
| SKU-210 | Warning | Missing GTIN (barcode present in Shopify) | Add gtin `8412345678905`, no dashes | High |
| SKU-355 | Disapproved | Image has promo overlay | Replace with clean white-bg image | Med |

**2. Rewritten titles**

| id | Old title | New title (≤150, front-loaded) |
|---|---|---|
| SKU-102 | "Camiseta oferta!!" | "Fajitex Camiseta Térmica Hombre Manga Larga Algodón Negro Talla L" |

Plus proposed `google_product_category`, `product_type`, and `custom_label_0–4` values. Deliver as a table (and CSV/Notion if requested).

## Guardrails
- Never fabricate a GTIN or set `identifier_exists=false` to dodge a missing one — both risk suspension.
- Never bulk-apply feed/Shopify edits; always show a preview and get confirmation.
- Respect the account's country, currency (ISO 4217), and language — do not default to USD/English. Confirm locale first.
- Keep feed price/availability in sync with Shopify and the landing page; flag mismatches instead of guessing which side is right.
- If GMC feed data wasn't provided, say clearly which checks couldn't run and what to export.

## References
See `reference/knowledge-base.md` for the sourced attribute spec, GTIN rules, title formulas, disapproval catalog, and the diagnostics workflow, with citation URLs.
