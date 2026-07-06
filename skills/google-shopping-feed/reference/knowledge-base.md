# Google Shopping Feed — Knowledge Base

Distilled, sourced expertise for auditing and optimizing a Google Merchant Center (GMC) product feed. Every threshold below carries its source. Written in English; MLO brands operate ES/EN DTC catalogs across EUR/USD/MXN/COP/GBP — always apply the account's real locale.

---

## 1. Required & conditional attributes (the spec)

Google's official [product data specification](https://support.google.com/merchants/answer/7052112) defines what every item needs.

**Required for all products:**

| Attribute | Limit / format | Notes |
|---|---|---|
| `id` | ≤50 chars, unique | Use the SKU; valid unicode only |
| `title` | ≤150 chars | Accurately describes the product; should match/relate to the landing page |
| `description` | ≤5000 chars | Plain text, matches landing page, no promo language |
| `link` | verified domain, http(s) | RFC-compliant landing page URL |
| `image_link` | JPEG/WebP/PNG/GIF/BMP/TIFF | 500×500px minimum enforced Jan 31, 2027; don't upscale or send thumbnails |
| `price` | ISO 4217, period decimal | Must match landing page; exclude tax for US/CA |
| `availability` | `in_stock` / `out_of_stock` / `preorder` / `backorder` | Only these values |
| `brand` | ≤70 chars | Manufacturer name; required except for movies/books/recordings |

**Conditional / recommended:**

| Attribute | When required | Details |
|---|---|---|
| `gtin` | If manufacturer-assigned a GTIN | Numeric, **no dashes/spaces**, valid GS1 check digit |
| `mpn` | If no GTIN | ≤70 alphanumeric, manufacturer-assigned |
| `identifier_exists` | Optional | Set `no` **only** if the product genuinely has no GTIN/MPN/brand |
| `condition` | If used/refurbished | `new` / `refurbished` / `used` |
| `availability_date` | If `preorder`/`backorder` | ISO 8601 |

**Optional but high-leverage:**

| Attribute | Limit | Use |
|---|---|---|
| `product_type` | ≤750 chars | Merchant-defined category, levels split by `>`; only first value used for bidding |
| `google_product_category` | — | Prefer the numeric taxonomy ID; don't rely on auto-assignment for niche items |
| `sale_price` + `sale_price_effective_date` | — | Submit alongside `price`; ISO 8601 range split by `/` |
| `custom_label_0`–`custom_label_4` | ≤100 chars each | Campaign segmentation; max 1,000 unique values per label |
| `additional_image_link` | up to 10 images | Lifestyle/staged shots |

Sources: [Google product data spec](https://support.google.com/merchants/answer/7052112), [Store Growers — every GMC feed attribute explained](https://www.storegrowers.com/google-merchant-center-feed-attributes/).

---

## 2. Product titles — the single highest-leverage field

Titles are the most impactful attribute in the feed: **81% of high-performing advertisers use different, more keyword-optimized titles in their feeds than on their product pages** ([Store Growers](https://www.storegrowers.com/google-merchant-center-feed-attributes/)).

**Rules ([FeedOps](https://feedops.com/google-shopping-product-title-optimization/)):**
- Limit 150 chars, but the **first 60–70 characters are the most important** because they're most likely to be visible; only ~30–35 chars render in the ad on mobile — front-load them.
- Google weights words at the **start** of the title more heavily. Lead with the most important, most-searched words.
- Include the attributes shoppers use to decide: brand, product type, model, size, color, gender, material, capacity, compatibility, key benefit.
- Use numerals, not spelled-out numbers.

**Category formulas ([FeedOps](https://feedops.com/google-shopping-product-title-optimization/), [Store Growers](https://www.storegrowers.com/google-merchant-center-feed-attributes/)):**
- **Apparel:** Brand + Gender + Product Type + Material/Feature + Color + Size → *"Adidas Women's Lightweight Running Jacket Blue Medium"*
- **Footwear:** Brand + Gender + Product Type + Model + Color + Size → *"Nike Men's Running Shoes Air Zoom Pegasus 40 Black Size 10"*
- **Electronics:** Brand + Size/Model + Product Type + Key Specs → *"Samsung 55 Inch QLED 4K Smart TV HDR Dolby Atmos"*
- **Home:** Brand + Material + Product Type + Style + Size/Capacity → *"IKEA Solid Oak Dining Table Scandinavian Style 6 Seater"*
- **Beauty:** Brand + Product Type + Benefit + Size/Shade → *"CeraVe Hydrating Facial Cleanser Dry Skin 473ml"*

**Six title mistakes to avoid ([FeedOps](https://feedops.com/google-shopping-product-title-optimization/)):** (1) reusing website titles unoptimized, (2) duplicate titles across variants, (3) starting with low-value words (size, SKU), (4) keyword stuffing, (5) omitting decision attributes, (6) promotional language (price, sale, shipping, hype).

Measure title impact via impressions, CTR, conversion rate, search-term coverage, and ROAS ([FeedOps](https://feedops.com/google-shopping-product-title-optimization/)).

---

## 3. GTIN & product identifiers

A **GTIN** (Global Trade Item Number) is a GS1-assigned universal identifier for a specific product variant ([Marpipe](https://www.marpipe.com/blog/what-is-a-gtin-for-google-shopping-2025-guide-for-ecommerce-sellers)).

**Formats / lengths:**
- GTIN-12 (UPC) — 12 digits, mainly US
- GTIN-13 (EAN) — 13 digits, international
- GTIN-8 — 8 digits, small packaging
- GTIN-14 / ITF-14 — 14 digits, multipacks/cases
- ISBN — books

**Formatting rules ([Marpipe](https://www.marpipe.com/blog/what-is-a-gtin-for-google-shopping-2025-guide-for-ecommerce-sellers), [Google spec](https://support.google.com/merchants/answer/7052112)):**
- **No spaces, dashes, or letters.**
- Keep leading zeros (UPC must be exactly 12 digits, EAN 13).
- Last digit is a validating check digit — Google validates against GS1 registries.

**Required vs optional:** If the product has a manufacturer-assigned GTIN, you **must** include it. If none exists, fall back to `mpn` + `brand`. For products that are widely manufactured, submit all three: `gtin`, `mpn`, `brand` ([AdNabu](https://blog.adnabu.com/google-shopping-feed/google-shopping-feed-optimization/)).

**Benchmark:** Retailers who add correct GTINs see roughly a **20% average increase in clicks** (some analyses cite up to 40%) ([WebSearch/industry consensus](https://www.storegrowers.com/google-merchant-center-feed-attributes/), [Store Growers](https://www.storegrowers.com/google-merchant-center-feed-attributes/)).

**Consequences of missing/wrong GTIN ([Marpipe](https://www.marpipe.com/blog/what-is-a-gtin-for-google-shopping-2025-guide-for-ecommerce-sellers)):** product disapprovals, possible account suspension, loss of rich-listing enrichment (reviews/ratings/specs), reduced visibility, lower CTR & conversion. **Never fabricate a GTIN.**

**`identifier_exists=false`:** set to `no` only when the product genuinely lacks a GTIN/MPN/brand — custom, handmade, vintage, or store-exclusive goods. Using it to paper over a missing-but-existing identifier is a disapproval risk ([Google spec](https://support.google.com/merchants/answer/7052112)).

In Shopify, the GTIN lives in the variant **`barcode`** field — pull it from there rather than guessing.

---

## 4. Categorization: google_product_category & product_type

- **`google_product_category`** is Google's standardized taxonomy; use the **numeric ID** and don't trust auto-assignment for niche items, which get miscategorized ([Store Growers](https://www.storegrowers.com/google-merchant-center-feed-attributes/)).
- **`product_type`** is "the most underrated attribute in the feed" — your own hierarchy (levels split by `>`), not bound to Google's taxonomy. It drives granular campaign/bidding structure. Only the first value counts for bidding ([Store Growers](https://www.storegrowers.com/google-merchant-center-feed-attributes/), [Google spec](https://support.google.com/merchants/answer/7052112)).

---

## 5. Custom labels (0–4) for bidding segmentation

Five fields (`custom_label_0`–`4`), ≤100 chars, ≤1,000 unique values each. Common scheme ([Store Growers](https://www.storegrowers.com/google-merchant-center-feed-attributes/)):

| Label | Use | Example values |
|---|---|---|
| `custom_label_0` | Margin tier | high / medium / low |
| `custom_label_1` | Seasonality | summer / winter / evergreen |
| `custom_label_2` | Performance tier | bestseller / average / slow |
| `custom_label_3` | Price range | under-25 / 25-50 / 50-plus |
| `custom_label_4` | Promo status | sale / clearance / full-price |

These let PMax/Shopping campaigns bid differently by margin, season, or performance — e.g. push budget to high-margin bestsellers and cap slow, low-margin SKUs.

---

## 6. Images

Main image best practices ([Store Growers](https://www.storegrowers.com/google-merchant-center-feed-attributes/), [AdNabu](https://blog.adnabu.com/google-shopping-feed/google-shopping-feed-optimization/), [Google spec](https://support.google.com/merchants/answer/7052112)):
- White/solid background, product filling **~75–90%** of the frame.
- **No text, watermark, logo, or promotional overlay** on the main image.
- ≥800×800px recommended; **500×500px minimum enforced from Jan 31, 2027**.
- Don't upscale or submit thumbnails.
- Generative-AI images must retain metadata.
- Use `additional_image_link` (up to 10) for lifestyle/staged shots.

---

## 7. Common disapproval causes → fixes

From [AdNabu](https://blog.adnabu.com/google-shopping-feed/google-shopping-feed-optimization/) and the [Google spec](https://support.google.com/merchants/answer/7052112):

| Disapproval cause | Fix |
|---|---|
| **Price mismatch** (feed vs landing page) — the #1 cause | Sync price across feed, Shopify, website, and structured data; enable automatic item updates |
| **Availability mismatch** | Use accurate `availability` values; enable automatic item updates so stock status stays live |
| **Missing / invalid GTIN** | Add the correct GTIN (no dashes/spaces, valid check digit); if truly none, submit `mpn` + `brand`; only then consider `identifier_exists=no` |
| **Image issues** (low quality, promo overlay, watermark, wrong bg) | Replace with clean ≥800×800 white-bg image, product 75–90% of frame, no text |
| **Condition mismatch** | Set `condition` to reflect reality; keep consistent with landing page + structured data |
| **Prohibited / policy content** | Remove restricted products or claims; review against Merchant Center policies |
| **Missing required attribute** | Populate `title`/`description`/`price`/`availability`/`brand`/`link`/`image_link` |
| **Mismatched language** | Keep every attribute value in the feed's target language; don't mix ES/EN |

---

## 8. Diagnostics workflow

Recommended order ([AdNabu](https://blog.adnabu.com/google-shopping-feed/google-shopping-feed-optimization/), [Store Growers](https://www.storegrowers.com/product-feed-optimization/)):
1. **Review required attributes first** — title, description, availability, price, brand present & valid.
2. **Check consistency** across feed / website / structured data / Shopify (price, availability, condition, GTIN).
3. **Validate** against Google's product data spec.
4. **Use the GMC Diagnostics tab** (or feed-management software) to surface item-level errors before they compound; group by cause.
5. **Prioritize by product value** — optimize high-margin / bestseller SKUs first, then broaden to the full catalog.

Optimization priority order ([Store Growers](https://www.storegrowers.com/google-merchant-center-feed-attributes/)):
1. Fix disapprovals + ensure required attributes match landing pages.
2. Optimize titles & descriptions for relevance.
3. Organize with custom labels & product identifiers.
4. Add competitive enhancements (lifestyle images, product highlights).

---

## 9. 2026 note — AI title rewriting

AI-assisted title rewriting is now the highest-leverage feed automation, but the prompt must **lock and preserve identifiers** — brand, model number, GTIN, color, and size — so the rewrite never drops or alters them ([WebSearch/industry consensus 2026](https://blog.adnabu.com/google-shopping-feed/google-shopping-feed-optimization/)). This maps directly to the title-rewrite step in the skill: keep every decision attribute, just reorder and front-load.

---

## Expert video (anchor)

- **"How To Optimize Your Product Feed & Data In Google Merchant Center"** — YouTube, https://www.youtube.com/watch?v=S1NhYxaPnic. Covers feed data optimization across titles, identifiers, images, and disapprovals. *Note: the video transcript was not machine-retrievable at authoring time, so the concrete thresholds above are cross-verified against recognized expert Dennis Moons (Store Growers), whose written guides mirror the same methodology.*

---

## Sources

- Google — Product data specification: https://support.google.com/merchants/answer/7052112
- Store Growers — Every Google Merchant Center feed attribute explained: https://www.storegrowers.com/google-merchant-center-feed-attributes/
- Store Growers — Product feed optimization: where to focus: https://www.storegrowers.com/product-feed-optimization/
- FeedOps — Google Shopping product title optimization: https://feedops.com/google-shopping-product-title-optimization/
- AdNabu — Google Shopping feed optimization tips: https://blog.adnabu.com/google-shopping-feed/google-shopping-feed-optimization/
- Marpipe — What is a GTIN for Google Shopping (2025 guide): https://www.marpipe.com/blog/what-is-a-gtin-for-google-shopping-2025-guide-for-ecommerce-sellers
- YouTube (expert video) — How To Optimize Your Product Feed & Data In Google Merchant Center: https://www.youtube.com/watch?v=S1NhYxaPnic
