# 🚀 10 Paid-Ads Skills for Claude — Google Ads + Meta Ads

**Turn Claude into a paid-ads operator.** Drop these in and Claude can clean your Google Ads negative keywords, audit a Performance Max campaign, write compliant RSAs, audit your Meta Advantage+ setup, rank your creatives by hook rate, and more — using the same playbooks a growth agency uses.

Built by [**MLO Growth**](https://mlo-growth.com) — a DTC ecommerce growth agency. Every skill is grounded in **real, cited expertise** (official Google/Meta docs, community scripts, and top advertiser sources), not generic AI advice. **Free. MIT-licensed.**

> 💡 New to Claude "skills"? A skill is a folder that teaches Claude how to do one job really well. You install it once and just ask in plain language — "audit my PMax", "clean my search terms". See **[START-HERE.md](START-HERE.md)**.

---

## What's inside

### 🔵 Google Ads
| Skill | What you get |
|---|---|
| **google-negative-keywords** | A clean, match-typed negative keyword list from your Search Terms Report — kills wasted spend |
| **google-pmax-auditor** | A full Performance Max audit (assets, search themes, signals, cannibalization, budget) with prioritized fixes |
| **google-rsa-generator** | Compliant Responsive Search Ads — 15 headlines, 4 descriptions, sitelinks & callouts — built for high Ad Strength |
| **google-search-terms** | Mines your Search Terms Report for new keyword wins, intent clusters & things to negate (n-gram analysis) |
| **google-shopping-feed** | Fixes & optimizes your Merchant Center feed — titles, GTIN, attributes — to stop disapprovals and lift Shopping/PMax |

### 🟣 Meta Ads
| Skill | What you get |
|---|---|
| **meta-ad-copy** | Meta ad copy (primary text, headlines, descriptions) by awareness level & angle, with A/B variants |
| **meta-asc-auditor** | An Advantage+ Shopping Campaign audit against best-practice setup, with a prioritized fix list |
| **meta-audience-builder** | The right audience mix (broad / Advantage+ / interest / lookalike / custom + exclusions) for your account stage |
| **meta-creative-analyzer** | Your creatives ranked by hook rate, hold rate, CTR & fatigue into **scale / iterate / kill** |
| **meta-hook-optimizer** | Diagnoses weak hooks and hands you 5–10 testable opening hooks + a test plan |

---

## Get started in 2 minutes

**The easy way (no code):**
1. Click the green **`< > Code`** button above → **Download ZIP** → unzip it.
2. Copy any skill folder (e.g. `skills/google-negative-keywords`) into your Claude skills folder:
   - Mac/Linux: `~/.claude/skills/`
   - Windows: `%USERPROFILE%\.claude\skills\`
3. Open Claude and just ask: *"clean my Google Ads negative keywords"*. Done.

**The developer way (Claude Code, one command):**
```
/plugin marketplace add growthmlo-code/mlo-ads-skills
/plugin install mlo-ads-skills
```

👉 Full walkthrough (with pictures-worth-of-detail) in **[START-HERE.md](START-HERE.md)**.

*Requires a Claude that supports Agent Skills (Claude Code, or the Claude desktop app). To pull live account data, connect the relevant tool — see below.*

---

## Where the data comes from
Skills use your connected tools when available, and tell you what to paste if not:
- **Google Ads** → a Google Ads MCP or the Windsor.ai `google_ads` connector
- **Shopify / Merchant Center** → the Shopify MCP
- **Meta Ads** → a Meta Marketing API MCP and/or Windsor.ai `facebook`
- **Creative intelligence** → Atria

No tools connected? Every skill also works if you paste in an export (CSV / report) — it'll tell you exactly what it needs.

---

## Why trust these
Each skill ships with a `reference/knowledge-base.md` citing exactly where its rules come from — Google/Meta's own docs, open-source scripts, and named advertiser sources. Read them, challenge them, improve them. That's the point.

---

## Made by M.L.O Growth
We run paid growth for DTC ecommerce brands. If these help you, the best thank-you is a follow.

- 🌐 [mlo-growth.com](https://mlo-growth.com)
- 💼 Connect with **Marcel López** on LinkedIn
- ⭐ Star this repo so others find it

_MIT-licensed — use them, fork them, ship them. v0.1.0_
