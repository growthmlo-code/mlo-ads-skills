---
name: meta-ad-copy
description: Generic, framework-driven engine that writes Meta (Facebook/Instagram) ad copy for a DTC product — Primary Text (A/B variants across distinct angles), Headline (A/B), and Description — tuned to the buyer's awareness level (Eugene Schwartz) and a chosen angle, front-loaded for the ~125-char "See more" cutoff and Meta-policy-safe. ALWAYS use this skill when the user asks for Meta/Facebook/Instagram ad copy in any phrasing — EN: "write the Meta ad", "ad copy for Facebook", "primary text for [product]", "give me Instagram copy variants", "headline and description for this ad", "hooks for my Meta ad"; ES: "copy para Meta", "ad copy Facebook", "primary text para [producto]", "hazme variantes de copy de Instagram", "escribe el anuncio de Meta", "copys para [producto]", "gancho para el anuncio". Fires on casual/partial asks too ("necesito copy para el ad de X"). This is the generic reusable engine; MLO's brand-specific `ad-copy-meta` skill (Figma→Notion) is separate.
---

# Meta Ad Copy Engine (generic)

## What it does
Turns a product/brand brief into launch-ready Meta ad copy: at least **2 distinct Primary Text variants** (each built on a different angle — pain-led, benefit-led, social-proof-led), **2 Headline variants**, and **1 Description**, all matched to the target buyer's **awareness level** and written to survive the **~125-character "See more" truncation**. Output is copy-paste-ready for Ads Manager and Meta-policy-conscious.

This is the **generic, self-contained engine** — framework-driven, works for any brand. MLO already has a brand-specific `ad-copy-meta` skill that reads approved Figma creatives and uploads to Notion; keep this one generic and use it when you just need copy from a brief.

## When to use
- The user wants Meta/Facebook/Instagram ad copy from a product description or brief.
  - EN: "write the Meta ad for X", "ad copy Facebook", "primary text for [product]", "make Instagram copy variants", "headline + description for this ad".
  - ES: "copy para Meta", "escríbeme el anuncio de Meta", "primary text para [producto]", "hazme variantes de copy de Instagram", "copys para [producto]", "dame ganchos para el ad".
- The user hands over a winning angle/hook (from Atria or the `meta-creative-analyzer` skill) and wants it turned into full ad copy.
- The user wants angle A/B variants for a copy test.

## Inputs needed
Ask for what's missing before writing:
1. **Product + one-line offer** (what it is, price/discount, guarantee).
2. **Core benefit + the pain it removes** (the transformation).
3. **Proof** (reviews count, star rating, press, ingredient/spec, a testimonial line).
4. **Target awareness level** — Unaware / Problem-aware / Solution-aware / Product-aware / Most-aware. If unknown, default to **Problem-aware** (the DTC cold-traffic workhorse) and say so.
5. **Angle / hook** if the user has one (else generate 3 candidate angles).
6. **Language + market** (ES/EN; locale, currency).
7. **Landing URL** (for the CTA / display link).

## Data sources
- **Primary input:** the product/brand brief the user provides (or a brand-brain skill if one exists).
- **Optional angle intel:** winning-angle/hook data from **Atria via Chrome** (`claude-in-chrome`) or the output of the `meta-creative-analyzer` / `meta-hook-optimizer` skills.
- No live ad-account pull is required to write copy. If the user wants to publish, that's a separate Meta Marketing MCP (`ads_*`) step — this skill only produces the text.

## Method
1. **Lock the awareness level.** Pick one of Schwartz's 5 (Unaware → Most-aware). It dictates how much you have to teach vs. how directly you can sell. (See knowledge base for the message each level needs.)
2. **Pick the angle per variant.** Produce ≥2 Primary Texts on *different* angles so the test learns something:
   - **Variant A — pain-led** (framework: **PAS** — Problem → Agitate → Solve).
   - **Variant B — benefit-led** (framework: **BAB** — Before → After → Bridge) or **social-proof-led** (lead with the stat/testimonial).
3. **Write the hook line first (first ~125 chars).** This is the whole ad for ~99% of viewers who never tap "See more." One scroll-stopping idea, front-loaded, no throat-clearing. Match the hook style to the awareness level (curiosity/problem for cold; offer/urgency for warm).
4. **Build the body with one framework.** Don't mix PAS and AIDA in the same block. Keep to one clear value prop + one proof element + one CTA.
5. **Close with a CTA line** that names the next action and (softly) the offer ("Shop the [offer] →", "Get yours — [guarantee]").
6. **Write 2 Headlines** (≤40 chars, ideally ≤27 for Feed): one benefit/outcome, one offer/CTA. These sit *below* the image and complement, not repeat, the primary text.
7. **Write 1 Description** (≤25–30 chars): a short reinforcement (offer, guarantee, or proof). Treat as optional — hidden on most placements.
8. **Compliance pass.** Rewrite any line that implies you know the user's personal attributes (health, body, finances) or promises unrealistic/before-after transformations. (See Guardrails.)
9. **Front-load check.** Confirm each Primary Text's first ~125 chars stand alone as a complete mini-ad.
10. **Emoji/formatting pass.** 0–2 purposeful emojis max, line breaks for scannability, no ALL-CAPS walls.

## Rules & thresholds
- **Primary Text:** hard max 2,200 chars (API up to ~4,096), but only **~125 chars show before "See more"** on mobile Feed — front-load. ~1% of users expand.
- **Headline:** recommended **≤40 chars**; Facebook Feed truncates around **27**. Reels overlay as low as 10.
- **Description:** **≤25–30 chars**, shown reliably only on Marketplace / Search / Audience Network / In-stream.
- **Meta lets you enter up to 5 options per text field** (multiple primary texts / headlines / descriptions) and optimizes per person — deliver at least 2 primary + 2 headline.
- **Awareness match is non-negotiable:** cold/Problem-aware traffic needs problem+empathy framing; only Product-/Most-aware traffic tolerates direct offer/urgency copy.
- **One framework per primary text.** Approved: **PAS, BAB, AIDA, 4Ps** (Promise-Picture-Proof-Push).
- **Emojis:** 0–2, meaningful; never in a way that breaks the "See more" line.

## Output
Deliver a single clean block the user can paste into Ads Manager. Shape:

```
AWARENESS LEVEL: Problem-aware   |   MARKET: ES
—
PRIMARY TEXT A — pain-led (PAS)
[Hook line ≤125 chars]
[Agitate → solve → proof]
[CTA line]

PRIMARY TEXT B — social-proof-led
[Hook line ≤125 chars: stat/testimonial]
[What it is → benefit]
[CTA line]

HEADLINES (≤40 chars)
1. [benefit/outcome]
2. [offer/CTA]

DESCRIPTION (≤30 chars)
[short reinforcement]

DISPLAY LINK: brand.com/product
```
For ES markets, write natively in Spanish (not translated) and respect locale.

## Guardrails
- **No personal-attribute targeting.** Never write copy that asserts/implies you know the reader's health, body, weight, mental state, finances, or relationship status. Avoid "Struggling with belly fat?" / "¿Sufres de X?" second-person framing on sensitive topics — reframe to third person or product-first ("This helps with…" / "La rutina que…").
- **No unrealistic or before/after claims,** including *implied* transformations ("results in 7 days", side-by-side body shots). Meta now reads implied meaning semantically.
- **No fabricated proof.** Only use review counts, ratings, press, or testimonials the user actually provided; if none, drop proof-led variant or flag it.
- **Respect currency/locale/language** exactly as briefed.
- **Don't over-emoji or clickbait** past what the landing page delivers (message match matters).
- This skill **writes copy only** — it does not publish. Publishing to an ad account is a separate confirmed step.

## References
See `reference/knowledge-base.md` for the awareness-level playbook, framework templates, hook patterns, character-limit tables, and full compliance detail — every claim cited to source.
