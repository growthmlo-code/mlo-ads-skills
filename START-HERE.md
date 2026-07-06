# Start here 👋

New to Claude "skills"? This page gets you from zero to running these skills, even if you've never touched code.

## What is a "skill"?
A skill is just a folder of instructions that teaches Claude how to do one specific job — like auditing a Performance Max campaign — really well. You install it once, then ask Claude in plain language and it follows the playbook.

## What you need
- **Claude with Agent Skills support** — that means either:
  - **Claude Code** (the free CLI / desktop coding assistant), or
  - the **Claude desktop app** with skills enabled.
- (Optional) A connected data tool if you want Claude to pull your live account numbers — Google Ads, Meta Ads, or Shopify. You can skip this and paste an export instead.

---

## Install (the no-code way)

1. **Download** — on the repo page, click the green **`< > Code`** button → **Download ZIP**. Unzip it.
2. **Find your skills folder** on your computer (create it if it doesn't exist):
   - **Mac / Linux:** `~/.claude/skills/`
   - **Windows:** `%USERPROFILE%\.claude\skills\`
3. **Copy in the skills you want.** Each folder inside `skills/` is one skill. Copy the whole folder. For example, drag `skills/meta-hook-optimizer` into `~/.claude/skills/`.
4. **Restart Claude** (close and reopen) so it picks up the new skills.

That's it.

## Install (the one-command way, for Claude Code)
```
/plugin marketplace add growthmlo-code/mlo-ads-skills
/plugin install mlo-ads-skills
```
This installs all 10 at once.

---

## How to use them
Just describe what you want in normal language. Claude will recognize which skill fits and run it. Examples:

| You say… | Skill that fires |
|---|---|
| "Clean my Google Ads negative keywords" | google-negative-keywords |
| "Audit my Performance Max campaign" | google-pmax-auditor |
| "Write me responsive search ads for [product]" | google-rsa-generator |
| "What search terms should I add or block?" | google-search-terms |
| "Fix my Shopping feed / Merchant Center" | google-shopping-feed |
| "Write Meta ad copy for [product]" | meta-ad-copy |
| "Audit my Advantage+ Shopping campaign" | meta-asc-auditor |
| "What audiences should I use on Meta?" | meta-audience-builder |
| "Which creatives should I scale or kill?" | meta-creative-analyzer |
| "Give me stronger hooks for this ad" | meta-hook-optimizer |

## No account connected? No problem.
If you haven't connected Google/Meta/Shopify, the skill will ask you to paste an export (like a Search Terms Report CSV) and work from that.

---

## Troubleshooting
- **Claude doesn't seem to use the skill?** Make sure the folder is directly inside your skills directory (e.g. `~/.claude/skills/meta-hook-optimizer/SKILL.md` should exist), then restart Claude.
- **Want to see what a skill actually does?** Open its `SKILL.md` — it's readable. The `reference/knowledge-base.md` shows the sources behind it.

Questions? Reach out to [MLO Growth](https://mlo-growth.com).
