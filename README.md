# Ultimate Meta Ads Skill

A drop-in [Claude Code](https://claude.com/claude-code) **skill** that turns Claude into a Meta (Facebook & Instagram) advertising strategist. It packages the evergreen strategy, copywriting, creative, and scaling frameworks from *Ultimate Guide to Facebook Advertising (3rd ed.)* into a structured, paste-ready knowledge base — and **corrects every outdated mechanic** against the 2025–2026 state of Meta Ads via a dedicated supplement that overrides the book on conflict.

> **TL;DR** — Install the `meta-ads/` folder into your skills directory. Then just talk to Claude about Facebook/Instagram ads and it will pull the right framework, checklist, or template automatically.

---

## What's inside

```
meta-ads/
├── SKILL.md                    # The router. Loads on demand; maps each step of the
│                               #   "Facebook Flight Plan" to the right reference.
├── references/   (16 files)    # 15 distilled knowledge domains + the modern supplement
│   └── SUPPLEMENT-2025.md       # ⭐ Modern Meta corrections — OVERRIDES the book on conflict
├── checklists/   (11 files)    # Runnable, paste-ready checklists (pre-launch, pre-scale, etc.)
└── templates/    (8 files)     # Copy-paste frameworks & fill-in-the-blank copy formulas
```

**The 15 knowledge domains:** strategy & mindset · account setup · pixel/tracking · audiences & targeting · funnels & offers · campaign objectives · ad set structure & budget · ad copy · creative design · hooks & messaging · video ads · boosted posts · reporting & optimization · scaling · troubleshooting.

**Named frameworks it surfaces:** Facebook Flight Plan · UPSYD awareness ladder · BCOP audience research · A.P.B. ad-set method · Four Ad Set Groups · Michigan Method · Five-Tier Scaling System · 7 Ad Building Blocks · 13 Elements of Persuasive Copy · 7 Power Questions · Three-Step Video Formula (EDIE) · Six Proven Offers.

---

## ⚠️ Accuracy model (important)

The source book is from **~2017**. Its *strategy, copywriting, and creative thinking are evergreen* — but its *tracking, targeting defaults, objectives, budgeting, attribution, diagnostics, and creative specs are outdated.*

This skill handles that with a **two-layer design**:

1. **`references/`** — the book's evergreen brain, used as-is.
2. **`references/SUPPLEMENT-2025.md`** — web-researched corrections (Meta official docs) that **win on any conflict**. It covers:
   - Pixel → **Dataset** rename, **Conversions API (CAPI)** + `event_id` deduplication, **Event Match Quality (EMQ 0–10)**
   - **iOS 14 / ATT**, retirement of the manual **8-event Aggregated Event Measurement** system (June 2025), domain verification
   - The **Advantage+** suite (Advantage+ Sales / Audience / Placements / Creative)
   - **ODAX** objective consolidation (11 legacy objectives → 6 outcomes) with a mapping table
   - **Advantage campaign budget** (formerly CBO) vs. ABO
   - **Attribution windows** (7-day click / 1-day view default; view windows removed Jan 12, 2026)
   - **Ad Relevance Diagnostics** (the 1–10 Relevance Score is gone) and current learning-phase mechanics (~50 events / 7 days)
   - **Vertical-first creative specs** (9:16 Reels/Stories, 4:5 Feed; the 20% text rule is retired)

`SKILL.md` instructs Claude to consult the supplement for anything in those areas, so the skill stays accurate against today's Meta.

---

## Install

A Claude Code skill is just a folder containing a `SKILL.md`. Put the `meta-ads/` folder anywhere Claude Code looks for skills:

### Option A — Personal skill (all your projects)
```bash
git clone https://github.com/itsfromgaurav/ultimate-meta-ads-skill.git
mkdir -p ~/.claude/skills
cp -R ultimate-meta-ads-skill/meta-ads ~/.claude/skills/meta-ads
```

### Option B — Project skill (one repo / team)
```bash
mkdir -p .claude/skills
cp -R ultimate-meta-ads-skill/meta-ads .claude/skills/meta-ads
# commit it so your whole team gets it
```

### Option C — Symlink (stay up to date with `git pull`)
```bash
git clone https://github.com/itsfromgaurav/ultimate-meta-ads-skill.git
ln -s "$(pwd)/ultimate-meta-ads-skill/meta-ads" ~/.claude/skills/meta-ads
```

Then start (or restart) Claude Code. Confirm it's loaded:
```
/skills        # meta-ads should appear in the list
```

> Works the same way in the Claude Code CLI, the desktop app, and IDE extensions — anywhere skills are supported. No API keys or dependencies required; it's pure Markdown.

---

## How to use it

The skill triggers automatically when your prompt is about Meta/Facebook/Instagram advertising. Just ask naturally:

- *"Help me plan a Facebook ad campaign for my Shopify store."*
- *"Write 5 ad copy variations using the 7 building blocks for a webinar funnel."*
- *"My ad set has high CTR but zero conversions — what's wrong?"*
- *"I have a winner at $18 CPA. How do I scale it without breaking it?"*
- *"Set up my pixel and CAPI correctly for 2025."*
- *"Which campaign objective should I use for lead gen now?"*

Behind the scenes, Claude walks the **Facebook Flight Plan** pipeline and loads only the reference(s) it needs:

```
0 Foundation → 1 Tracking → 2 Funnel/Offer → 3 Audiences → 4 Objective →
5 Ad Set → 6 Creative/Copy → 7 Launch → 8 Report → 9 Optimize → 10 Scale → 11 Troubleshoot
```

You can also point it at an asset directly:
- *"Run my landing page through the pre-launch checklist."*
- *"Use the BCOP template to research audiences for a vegan meal-prep brand."*
- *"Give me the modern pixel + CAPI setup order."* (pulls `SUPPLEMENT-2025.md`)

---

## How others can use & adapt this

- **Use as-is:** install and go (above).
- **Customize for your niche:** edit any file in `references/`, add your own benchmarks to the tables, or drop brand-specific templates into `templates/`. It's all plain Markdown.
- **Extend the supplement:** Meta changes fast. Add new corrections to `references/SUPPLEMENT-2025.md` and bump the date — it always overrides the references, so new platform changes slot in cleanly.
- **Fork it:** PRs welcome for updated specs, new frameworks, or additional checklists. Keep the "evergreen reference vs. dated-mechanic supplement" separation intact.
- **Reuse the pattern:** the structure (lean `SKILL.md` router → `references/` → `checklists/` + `templates/`, with a dated supplement that overrides) is a reusable template for turning *any* book or knowledge source into a skill.

### Keeping it current
Re-verify the supplement against [Meta Business Help Center](https://www.facebook.com/business/help) and [Meta for Developers](https://developers.facebook.com/docs/marketing-apis/) roughly **quarterly** — ad-platform mechanics drift fast.

---

## Attribution & disclaimer

- **Source material:** *Ultimate Guide to Facebook Advertising, 3rd Edition* by Perry Marshall, Keith Krance, Thomas Meloche, and contributing authors. This repository contains a **transformative, summarized distillation** of that book's frameworks for use as an AI tool — not the book itself. The original text, the raw extracted chapters, and the source file are **not** included. If you want the full material, **buy the book** — it's worth it.
- **Not affiliated with or endorsed by** Meta Platforms, Inc. or the book's authors/publisher.
- **No guarantees.** Advertising results vary; nothing here is financial or legal advice. Always validate against Meta's current official documentation and your own data.
- The skill's structure, supplement research, checklists, and templates are released under the license below.

## License

[MIT](./LICENSE) — for the skill structure, organization, supplement, checklists, and templates authored in this repo. The underlying advertising *ideas and frameworks* belong to their original authors; please support them.
