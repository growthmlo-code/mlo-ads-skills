# Knowledge base — Google RSA Generator

Distilled, cited expertise for generating high-Ad-Strength, compliant Responsive Search Ads. Every threshold below is sourced; the full URL list is at the bottom.

---

## 1. Hard specs & character limits (official)

Responsive Search Ads are Google's default search ad format: you supply many assets and Google's ML assembles combinations per query.

| Asset | Min | Max | Char limit each |
|---|---|---|---|
| Headlines | 3 | **15** | **30** |
| Descriptions | 2 | **4** | **90** |
| Display-URL paths | 0 | **2** | **15** |
| RSAs per ad group | — | **3** | — |

- Google assembles up to **3 headlines and 2 descriptions** into a shown ad; unpinned assets rotate dynamically. ([Google Ads Help — About RSAs](https://support.google.com/google-ads/answer/7684791?hl=en))
- Character limits and asset counts confirmed by Google and multiple 2025–2026 references. ([Google Ads Help](https://support.google.com/google-ads/answer/7684791?hl=en); [Semrush](https://www.semrush.com/blog/responsive-search-ads/))

### Sidecar assets (formerly "extensions")
- **Sitelinks**: title **≤25 chars** (12 in double-width languages e.g. CJK); optional two description lines **≤35 chars** each. Google recommends **4+ sitelinks**; **≥6 across account/campaign/ad group** helps reach "Good+" Ad Strength. ([Google Ads Help — sitelinks](https://support.google.com/google-ads/answer/2375416?hl=en); [Adsbot](https://adsbot.co/google-ads-sitelink-character-limits/))
- **Callouts**: **≤25 chars** each (12 in double-width). Punchy standalone claims ("Free UK Delivery", "No Setup Fees", "30-Day Returns"). Deliver **≥4**. ([Google Ads Help / knowledge bases](https://knowledgebase.tagdigital.co.uk/knowledge/what-are-the-character-limits-for-google-ads))

---

## 2. Ad Strength — what it measures and how to max it

Ratings scale: **Incomplete → Poor → Average → Good → Excellent**. Ship bar is **Good**; goal is **Excellent**. Ad Strength is a **diagnostic, not a serving/performance metric** — it does not change eligibility and a "Poor" ad can outperform an "Excellent" one on CTR/CVR. ([Google Ads Help — Ad Strength](https://support.google.com/google-ads/answer/9921843?hl=en); [Optmyzr](https://www.optmyzr.com/blog/ad-strength-responsive-search-ads/))

Google's own improvement levers (encode these):
1. **Include keywords in headlines/descriptions** — add text from your ad group keywords to improve relevance.
2. **Add more headlines & descriptions** — fill toward 15 / 4 to expand combinations.
3. **Make headlines/descriptions unique** — distinct selling points and CTAs; near-duplicates hurt.
4. **Add sitelinks** — ≥6 across the account to reach Good+.
5. **Use pinning sparingly** — avoid pinning multiple identical/near-identical assets to one position.

Business case: advertisers who move Ad Strength **Poor → Excellent** average **~15% more clicks and conversions**. ([Google Ads Help](https://support.google.com/google-ads/answer/7684791?hl=en))

Google recommends **≥2 RSAs with Good/Excellent Ad Strength per ad group**, each with a unique final URL, and testing a 3rd. ([pattern.com](https://au.pattern.com/blog/best-practices-for-responsive-search-ads-rsa-in-2025/))

---

## 3. Headline architecture (how experts actually fill the 15)

Write headlines by **role**, not at random, so Google can combine freely and Ad Strength stays high:

- **Keyword headlines (3–4)** — contain the exact/near target keyword. Boosts relevance.
- **Benefit headlines (3–4)** — the outcome the buyer wants.
- **Feature/USP headlines (2–3)** — what's different (ingredient, warranty, material).
- **Offer/urgency headlines (2–3)** — promo, free shipping threshold, guarantee.
- **CTA / social-proof headlines (2–3)** — "Shop Now", "Rated 4.8★ by 10k+".

Key expert rules:
- **Don't put the keyword in every headline** — at least ~3 headlines should be non-keyword (benefit/feature/CTA). ([WordStream](https://www.wordstream.com/blog/ws/2022/04/05/responsive-search-ad-copy))
- **Keep headlines distinct** — "Google will not show similar variations"; sameness lowers Ad Strength. ([WordStream](https://www.wordstream.com/blog/ws/2022/04/05/responsive-search-ad-copy); [Growth Minded Marketing](https://growthmindedmarketing.com/blog/responsive-search-ads/))
- **Vary length** — mixing short and long headlines lets Google show 2–3-headline layouts. ([WordStream](https://www.wordstream.com/blog/ws/2022/04/05/responsive-search-ad-copy))
- **Quality over quota** — target 8–10 strong headlines minimum before padding; don't add filler just to hit 15. Aim for 15 *distinct* lines when the offer supports it. ([Growth Minded Marketing](https://growthmindedmarketing.com/blog/responsive-search-ads/); [pattern.com](https://au.pattern.com/blog/best-practices-for-responsive-search-ads-rsa-in-2025/))
- **Identity-trigger tactic**: insert the niche/audience into a headline to signal relevance ("462 leads/week" → "462 *dental* leads/week"). ([coreyhaines31 marketingskills](https://github.com/coreyhaines31/marketingskills/blob/main/skills/ads/SKILL.md))

---

## 4. Description frameworks (the 4 slots)

Use all 4 descriptions; each ≤90 chars; each says something different; don't restate headline wording; 2 should end with a CTA. Assume **Description 2 may not show** — each must stand alone. ([WordStream](https://www.wordstream.com/blog/ws/2022/04/05/responsive-search-ad-copy))

Assign one framework per slot (from the marketing-skills library):
- **PAS — Problem → Agitate → Solve → CTA.** e.g. "Dull skin dragging you down? It only gets worse untreated. Fix it with X. Shop now."
- **BAB — Before → After → Bridge.** e.g. "Tired of frizz? Picture sleek hair daily. X gets you there in 2 weeks."
- **Social-proof / offer lead.** e.g. "Loved by 12,000 buyers (4.8★). Free shipping over €40. Try risk-free 30 days."
- **Feature-stack + CTA.** e.g. "Vegan, cruelty-free, dermatologist-tested. Made in Spain. Order today."
([coreyhaines31 marketingskills](https://github.com/coreyhaines31/marketingskills/blob/main/skills/ads/SKILL.md))

---

## 5. Pinning — the discipline

- **Default = pin nothing.** Pinning caps how many combinations Google can test and directly suppresses Ad Strength. ([Google Ads Help](https://support.google.com/google-ads/answer/9921843?hl=en); [Growth Minded Marketing](https://growthmindedmarketing.com/blog/responsive-search-ads/))
- Pin **only** legally mandatory or brand-mandatory copy (disclaimers, trademark lockups, a required seasonal line). ([Growth Minded Marketing](https://growthmindedmarketing.com/blog/responsive-search-ads/))
- If you must pin, **pin 2–3 distinct assets to the same position** so Google retains choice, and don't pin near-identical assets to one slot. ([WordStream](https://www.wordstream.com/blog/ws/2022/04/05/responsive-search-ad-copy); [Google Ads Help](https://support.google.com/google-ads/answer/9921843?hl=en))
- **Guaranteed positions**: Headline 1, Headline 2, Description 1. **Not guaranteed**: Headline 3, Description 2 — never put must-see legal text there unpinned. ([Google Ads Help](https://support.google.com/google-ads/answer/7684791?hl=en))

---

## 6. Learning from top-performing ads (Google's own tooling)

Two official Google Marketing Solutions repos define the state of the art for AI-assisted RSA generation:

- **rsa-ai-generator** — generates headlines/descriptions from a campaign's existing **keywords** using Google LLMs, inside an Apps Script + Sheet workflow. Core idea: automate the "make as many varied headline/description variations as possible" best practice that's tedious by hand. ([GitHub](https://github.com/google-marketing-solutions/rsa-ai-generator))
- **copycat** — learns **brand voice from your best existing ads** and writes new RSAs in that style. Method to replicate manually:
  - Feed it high-quality existing ads (headlines + descriptions + keywords); ~**100+ varied examples** is optimal but it works with fewer.
  - Uses **Affinity Propagation clustering** to pick diverse *exemplars* (diversity, minimal redundancy) instead of all ads.
  - Generates a written **style guide** (tone/voice), optionally augmented with brand-guideline PDFs.
  - Generates via **few-shot prompting**: style guide + in-context exemplars + new keywords.
  - Quality gates: **memorization detection** (don't copy training ads verbatim), **style similarity**, **keyword similarity**. ([GitHub](https://github.com/google-marketing-solutions/copycat))

Practical takeaway for this skill: when Google Ads is connected, pull the ad group's **"Best"-labeled assets** to seed voice and winning angles, avoid **"Low"** assets, and never copy an existing headline verbatim (write in-voice, not clone).

---

## 7. Compliance & DTC notes (MLO context)

- Avoid **unverifiable superlatives** ("#1", "best", "guaranteed results") in regulated verticals (supplements, health, finance) unless substantiated; Google editorial policy and local ad law both bite here. Prefer specific, provable proof: "4.8★, 12k reviews", "Clinically tested", "Made in Spain".
- Honor **per-brand approved-claims guardrails** (e.g. the ALMA copy guardrails skill) before shipping copy.
- **Locale/currency**: MLO brands span ES/EN and €, $, MXN, COP. Write copy in the account's language and price in its currency — never default to English or €.
- Ad Strength ≠ performance: report it, but a sharply relevant "Good" ad can beat a generic "Excellent" one. ([Optmyzr](https://www.optmyzr.com/blog/ad-strength-responsive-search-ads/); Aaron Young video below)

---

## 8. Pre-flight checklist (run before delivering)

- [ ] 15 headlines, all ≤30 chars, all materially distinct
- [ ] Target keyword in 3–4 headlines (not all)
- [ ] Mix present: keyword / benefit / feature / offer / CTA+proof
- [ ] 4 descriptions, all ≤90 chars, one each PAS / BAB / social-proof / feature+CTA, 2 with CTA
- [ ] ≤2 paths, ≤15 chars each
- [ ] Pins: none unless legal/mandatory (and justified)
- [ ] ≥4 sitelinks (≤25) + ≥4 callouts (≤25)
- [ ] Language + currency = account's
- [ ] No unsubstantiated superlatives; claims within brand guardrails
- [ ] Projected Ad Strength stated (Good/Excellent) with reason
- [ ] Char count printed next to every line

---

## Expert video source

**"Do you NEED an Excellent Rating for Responsive Search Ads? | Google Ads 2023"** — Aaron Young (Define Digital Academy), YouTube: https://www.youtube.com/watch?v=x95HgGpwmhc
Key takeaway used here: an "Excellent" rating is **not mandatory** — Ad Strength doesn't affect serving eligibility and is a diagnostic to spot improvement opportunities, not a performance guarantee; a well-targeted "Good" RSA can outperform an "Excellent" one. This reinforces: aim for Good/Excellent, but never sacrifice real keyword relevance or brand voice to chase the badge. (Transcript not machine-retrievable; attribution and thesis confirmed via search + corroborated by Google's own Ad Strength documentation.)

---

## Sources
- Google Ads Help — About responsive search ads: https://support.google.com/google-ads/answer/7684791?hl=en
- Google Ads Help — About Ad Strength for RSAs: https://support.google.com/google-ads/answer/9921843?hl=en
- Google Ads Help — About sitelink assets: https://support.google.com/google-ads/answer/2375416?hl=en
- Google Marketing Solutions — rsa-ai-generator: https://github.com/google-marketing-solutions/rsa-ai-generator
- Google Marketing Solutions — copycat: https://github.com/google-marketing-solutions/copycat
- coreyhaines31 marketingskills — ads SKILL: https://github.com/coreyhaines31/marketingskills/blob/main/skills/ads/SKILL.md
- WordStream — RSA copy best practices: https://www.wordstream.com/blog/ws/2022/04/05/responsive-search-ad-copy
- Growth Minded Marketing — RSAs 2026 guide: https://growthmindedmarketing.com/blog/responsive-search-ads/
- pattern.com — RSA best practices 2025: https://au.pattern.com/blog/best-practices-for-responsive-search-ads-rsa-in-2025/
- Semrush — RSA ultimate guide: https://www.semrush.com/blog/responsive-search-ads/
- Optmyzr — Does Ad Strength impact RSAs: https://www.optmyzr.com/blog/ad-strength-responsive-search-ads/
- Adsbot — sitelink character limits: https://adsbot.co/google-ads-sitelink-character-limits/
- Tag Digital — Google Ads character limits: https://knowledgebase.tagdigital.co.uk/knowledge/what-are-the-character-limits-for-google-ads
- Aaron Young (Define Digital Academy) — Do you NEED an Excellent Rating for RSAs?: https://www.youtube.com/watch?v=x95HgGpwmhc
