---
name: google-rsa-generator
description: Generates a complete, policy-compliant Google Responsive Search Ad (RSA) — 15 headlines (≤30 chars), 4 descriptions (≤90 chars), up to 2 display paths (≤15 chars), plus sidecar assets (≥4 sitelinks, ≥4 callouts) — from a brand brief and/or top-performing keywords, engineered for "Good/Excellent" Ad Strength. Uses PAS/BAB/social-proof frameworks, pins sparingly, and keeps headlines distinct so Google can combine them. ALWAYS use this skill when the user (ES/EN) says "generar RSA", "hazme los anuncios de búsqueda", "responsive search ad", "copys de Google Ads para [marca]", "RSA de [marca]", "anuncios de search para [marca]", "genera headlines para Google Ads", "write RSA copy", "search ad headlines and descriptions", or asks for Google Search Ads copy for any DTC brand. Trigger on partial/casual asks about Google Ads text ads too.
---

# Google RSA Generator

## What it does
Produces a ready-to-paste Responsive Search Ad for one ad group: 15 headlines, 4 descriptions, up to 2 display-URL paths, plus the sidecar assets Ad Strength needs (sitelinks + callouts). Copy is built from the brand's value props and the ad group's target keyword, using proven direct-response frameworks (PAS, BAB, social-proof lead), and is engineered to hit "Good" or "Excellent" Ad Strength while staying inside every hard character limit. Output includes a live character count next to every line so nothing gets truncated at upload.

## When to use
- User asks for Google Search Ad copy: "generar RSA", "hazme los anuncios de búsqueda de [marca]", "copys de Google Ads para [marca]", "RSA de [marca]".
- EN: "write the responsive search ad", "give me 15 headlines and 4 descriptions", "RSA copy for [brand] targeting [keyword]".
- After the `google-search-terms` skill surfaces a winning keyword and the user wants an ad built around it.
- When refreshing a low-Ad-Strength or fatigued RSA in an existing ad group.

## Inputs needed (ask if missing)
1. **Brand + offer**: what's sold, the core value props / USPs, the promo or hook if any, the final URL.
2. **Target keyword(s)** for this ad group (1–3 tightly themed). Ask which keyword the ad group is built around — RSAs are per-ad-group.
3. **Locale + currency + language** (ES vs EN copy; € / $ / MXN / COP). MLO brands run across ES/EN and multiple currencies — never assume.
4. **Any legally mandatory phrasing** (needs pinning) — e.g. regulated health/finance claims, "results may vary", trademark lockups.
5. Optional: existing top-performing ads to learn voice from (see Data sources).

## Data sources
- **Keywords / existing top ads**: Google Ads via the Windsor.ai `google_ads` connector (or a Google Ads MCP if connected). Pull the ad group's keywords and, if available, the current best RSA's headlines/descriptions and asset performance labels ("Best"/"Good"/"Low") to learn brand voice and retire weak lines. If neither connector is wired, ask the user to paste the keyword list and any existing ad copy.
- **Brand brief / value props**: the user, the brand's MLO brand-brain skill, or the CRO/landing copy.
- **Currency/locale**: confirm with the user or the brand-brain; respect it in every number and CTA.
- Be honest: if Google Ads isn't connected, the skill still works from a pasted brief + keywords — it just can't auto-learn from live winners or auto-flag fatigued assets.

## Method
1. **Frame the ad group.** Confirm the single target keyword theme, the final URL, language, and currency. One RSA is written per ad group; note that up to 3 RSAs are allowed per ad group if the user wants variants.
2. **Mine raw material.** List the brand's USPs, offers, objections, and proof (reviews, stars, guarantees, shipping). If Google Ads is connected, pull existing "Best" assets to echo winning angles and mark "Low" assets to avoid repeating.
3. **Build the 15 headlines by role**, not at random — this is what drives Ad Strength and combinability:
   - 3–4 **keyword headlines**: include the exact/near target keyword (Ad Strength rewards keyword coverage).
   - 3–4 **benefit** headlines (the outcome the customer wants).
   - 2–3 **feature/USP** headlines (what makes it different).
   - 2–3 **offer/urgency** headlines (promo, free shipping, guarantee, "Shop the Sale").
   - 2–3 **CTA/social-proof** headlines ("Shop Now", "Rated 4.8★ by 10k+").
   Keep every headline ≤30 chars and semantically distinct — no two should be near-duplicates, or Google suppresses them.
4. **Write 4 descriptions** using direct-response frameworks, each ≤90 chars, each saying something different:
   - One **PAS** (Problem → Agitate → Solve), one **BAB** (Before → After → Bridge), one **social-proof/offer**, one **feature-stack + CTA**.
   - Don't restate headline wording; end 2 of them with a CTA. Assume Description 2 may not always show — each must stand alone.
5. **Write up to 2 display paths** (≤15 chars each) reinforcing the keyword/category, e.g. `/Skincare` `/Vegan`.
6. **Pin only if mandatory.** By default pin nothing. Pin ONLY legally required or brand-mandatory lines, and if you must, pin ≥2–3 distinct assets to the same position so Google still has choices. Flag every pin explicitly in the output.
7. **Generate sidecars for Ad Strength**: ≥4 sitelinks (specific destinations, ≤25 chars titles) and ≥4 callouts (punchy standalone claims, ≤25 chars). Google wants ≥6 sitelinks account-wide for "Good+".
8. **Self-audit against the checklist** (see Rules & thresholds) and report the projected Ad Strength ("Good"/"Excellent") with the reason.
9. **Present, then stop.** Show the full ad + char counts; do not push anything to Google Ads without explicit confirmation.

## Rules & thresholds (HARD — encode exactly)
- **Headlines**: up to **15**, each **≤30 characters**. Minimum 3. Aim to fill all 15 with distinct lines; if you can't write 15 genuinely different ones, deliver at least 10–12 strong ones rather than padding near-duplicates.
- **Descriptions**: up to **4**, each **≤90 characters**. Minimum 2; always deliver 4.
- **Display paths**: up to **2**, each **≤15 characters**.
- **RSAs per ad group**: max **3**.
- **Sitelinks**: deliver **≥4** (≤25-char titles; optional descriptions ≤35 chars). Account should have ≥6 total for "Good+" Ad Strength.
- **Callouts**: deliver **≥4**, each **≤25 characters**.
- **Keyword coverage**: include the target keyword in **several** (3–4) headlines, but NOT all — leave room for benefits/CTAs. Don't keyword-stuff.
- **Distinctness**: every headline and description must be materially different; Google won't show near-duplicates and it lowers Ad Strength.
- **Pinning**: use sparingly, only for legal/brand-mandatory positions. Over-pinning caps combinations and Ad Strength. Positions: Headline 1, Headline 2, Description 1 are guaranteed; Headline 3 / Description 2 are not.
- **Ad Strength target**: "Good" is the minimum ship bar; "Excellent" is the goal. Ad Strength is a diagnostic, not a performance metric — never trade real relevance for a green badge. Moving Poor→Excellent averages ~15% more clicks/conversions.
- **Compliance**: avoid unverifiable superlatives ("#1", "best", "guaranteed results") in regulated verticals (health, supplements, finance) unless substantiated; prefer specific proof ("4.8★, 12k reviews", "Clinically tested"). Respect the brand's approved-claims list (e.g. ALMA guardrails).

## Output
A single copy block for the ad group, in the account's language, e.g.:

```
RSA — [Brand] · Ad group: "[keyword theme]" · Lang: ES · Final URL: example.com/x
Projected Ad Strength: Excellent (15 distinct headlines, keyword in 4, 4 descriptions, 0 pins)

HEADLINES (max 30)
 1. Crema Vegana Antiedad        (24)   [keyword]
 2. Piel Firme en 4 Semanas      (23)   [benefit]
 ...
15. Envío Gratis +40€            (17)   [offer]

DESCRIPTIONS (max 90)
 1. [PAS]  ¿Piel apagada? Recupera luminosidad con activos veganos. Notarás el cambio. (78)
 ...

PATHS (max 15):  /Skincare   /Vegana
PINS: none  (or: H1 pinned "…" — legal)

SITELINKS (≥4, ≤25):  Best Sellers · Rutina Antiedad · Opiniones · Envíos y Devoluciones
CALLOUTS (≥4, ≤25):   Envío Gratis +40€ · Vegano y Cruelty-Free · 4.8★ 12.000 Reseñas · 30 Días
```
Deliver in chat by default; offer to drop it into a Notion doc or Slack draft, or CSV for bulk upload, if the user wants.

## Guardrails
- Never exceed a character limit — count every line and print the count; if borderline, trim rather than risk truncation.
- Never bulk-push or edit live Google Ads assets without showing the full preview and getting explicit confirmation.
- Respect account currency/locale/language in every headline, price, and CTA — don't default to € or English.
- Don't pin by default; each pin removes combinations. Justify any pin in the output.
- Don't fabricate reviews, ratings, awards, or claims. Use only proof the brand can substantiate; honor per-brand claim guardrails.
- Ad Strength is guidance, not gospel — flag it, but tell the user a "Good" ad with sharp relevance can beat an "Excellent" generic one.

## References
See `reference/knowledge-base.md` for the cited limits, Ad Strength factors, framework templates, and source URLs.
