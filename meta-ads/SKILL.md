---
name: meta-ads
description: >-
  End-to-end playbook for planning, building, launching, optimizing, and scaling
  paid ads on Meta (Facebook and Instagram). Use when the user mentions Meta Ads,
  Facebook Ads, Instagram Ads, FB/IG ads, Advantage+, Advantage+ Shopping, Ads
  Manager, Business Manager, the Meta/Facebook Pixel or Dataset, Conversions API
  / CAPI, server-side tracking, custom audiences, lookalike audiences,
  retargeting/remarketing, campaign objectives, ad sets, ad copy or creative,
  hooks, video ads, boosted posts, ad funnels and offers, interest/audience
  targeting, CPA/CPC/CPM/ROAS/relevance, ad fatigue or frequency, scaling ad
  spend, or troubleshooting underperforming campaigns (zero conversions, high
  CPA, ads not converting). Walks the user through the Facebook Flight Plan:
  foundation -> tracking -> funnel/offer -> audiences -> objective -> ad set ->
  creative/copy -> launch -> report -> optimize -> scale -> troubleshoot.
  Surfaces named frameworks (Flight Plan, UPSYD, FANS, BCOP, A.P.B., Michigan
  Method, Five-Tier Scaling, 7 Power Questions, EDIE, STEPPS), benchmark tables,
  and copy-paste templates and checklists.
---

# Meta Ads

A router over a distilled Facebook/Instagram advertising knowledge base. `SKILL.md`
stays lean — it points to the right `references/` file for each stage of the
**Facebook Flight Plan** and pulls paste-ready assets from `checklists/` and
`templates/`. Load reference files on demand; do not dump them.

## When to use / when NOT to use

**Use** when the user wants to plan, build, launch, diagnose, or scale paid ads
specifically on **Meta (Facebook / Instagram)**:
- Designing a campaign from scratch (objective, audiences, funnel, offer, budget).
- Writing ad copy, hooks, or creative briefs for Meta placements.
- Installing/validating the Pixel/Dataset and Conversions API (CAPI) tracking.
- Reading Ads Manager results and deciding what to pause, test, or scale.
- Fixing a broken campaign (zero conversions, high CPA, high CTR / low conversions, ad fatigue, policy/reach warnings).
- Scaling a proven winner while holding target CPA/ROAS.

**Do NOT use** for: Google / TikTok / LinkedIn / other ad platforms (route to a
general paid-ads skill), organic social content, or pure landing-page CRO (hand
off — though this skill does cover ad-to-page "scent" match).

## ⚠️ Accuracy

The `references/` are distilled from a **~2017 book** (*Ultimate Guide to Facebook
Advertising, 3rd ed.*). Its evergreen strategy, copy, and creative thinking still
hold, but its **tracking, targeting defaults, objectives, budgeting, attribution,
diagnostics, and creative specs are outdated**. For anything in those areas
**ALWAYS consult `references/SUPPLEMENT-2025.md` — it overrides the references on
conflict.** Specifically, the supplement supersedes the book on: browser-Pixel-only
tracking (now Pixel + CAPI, "Pixel" renamed "Dataset"), iOS14/ATT and the retired
8-event AEM system, the Advantage+ suite, ODAX objective consolidation (11 → 6),
CBO / Advantage campaign budget, attribution windows (7-day click / 1-day view;
view windows removed Jan 2026), Ad Relevance Diagnostics (the 1–10 Relevance Score
is gone), and vertical-first creative specs (9:16 / 4:5; 20% text rule retired).
Surface these as corrections and flag them to the user.

## The Facebook Flight Plan (workflow)

Run this as a linear-but-revisitable pipeline. Each step names the reference(s) to load.

| # | Stage | Load |
|---|---|---|
| 0 | **Foundation / pre-flight** — identify Business Category (Retail-Local-Service / eCommerce / Digital-Info), place the audience on the UPSYD awareness ladder (default start: Solution-Aware), confirm Page / Business Manager / ad account / Dataset exist. | `references/strategy_mindset.md` + `references/account_setup.md` |
| 1 | **Tracking** — install base Pixel + Standard Events, verify with Pixel Helper. **Gate: configure CAPI (Pixel + server-side, shared `event_id`), domain verification, and EMQ before relying on optimization.** | `references/pixel_tracking.md` + **`references/SUPPLEMENT-2025.md`** |
| 2 | **Funnel & offer** — pick a category funnel (FANS) and one of the Six Proven Offers; engineer hook + lead magnet (splinter / incompleteness / ad scent). | `references/funnels_offers.md` |
| 3 | **Audiences** — warm vs cold; build custom + lookalike audiences; run BCOP interest research; size them. **Check supplement for Advantage+ Audience defaults.** | `references/audiences_targeting.md` (+ supplement) |
| 4 | **Objective** — choose by commitment level and category. **Map legacy objectives to the 6 ODAX outcomes via the supplement.** | `references/campaign_objectives.md` (+ supplement) |
| 5 | **Ad set** — apply A.P.B. (Audience / Placement / Budget), Four Ad Set Groups, and (scale-ready) the Michigan Method; set budget + bidding. **Reconcile with CBO / Advantage campaign budget in the supplement.** | `references/adset_structure_budget.md` (+ supplement) |
| 6 | **Creative + copy** — write with the 7 Building Blocks / 13 Elements, run the 7 Power Questions; brief creative (hook→image, Six Aspects, STEPPS); build video with the Three-Step Formula + EDIE. **Use supplement creative specs (9:16 / 4:5).** | `references/ad_copy.md` + `references/creative_design.md` + `references/hooks_messaging.md` + `references/video_ads.md` |
| 7 | **Launch** — build order Campaign > Ad Set > Ad; clear reach/policy warnings; optionally pre-test "unicorn" creative cheaply via boosting first. | `references/boosted_posts.md` |
| 8 | **Report** — read Ads Manager; CPA primary, CTR/CPC/CPM/relevance secondary; watch frequency/fatigue and attribution window. **Apply supplement attribution + Ad Relevance Diagnostics.** | `references/reporting_optimization.md` (+ supplement) |
| 9 | **Optimize** — sequenced testing: win the image, then the copy, then the audience; mine boosted-post data for hooks; pause zero-converters and high-CPA ad sets. | `references/reporting_optimization.md` |
| 10 | **Scale** — pass the pre-scale readiness gate (≥10 conversions, under target CPA, audience ideally >1M), then run the Five-Tier system **in order** (Duplication → Audience → Alteration → Large Budget → Small Budget); combined = Massive Rapid Scaling. **Reconcile cadence with CBO in the supplement.** | `references/scaling.md` (+ supplement) |
| 11 | **Troubleshoot** (loop back any time) — match against the 5 failure scenarios; run the zero-conversions diagnostic. **Apply supplement for CAPI/attribution/learning-phase issues.** | `references/troubleshooting.md` (+ supplement) |

## Resource index

| Resource | What's in it |
|---|---|
| `references/strategy_mindset.md` | Flight Plan, UPSYD ladder, Customer Buying Cycle, Three Business Categories, 7 Power Questions, Four Definitions of "Working" |
| `references/account_setup.md` | Page / Business Manager / ad account / Pixel install / access roles |
| `references/pixel_tracking.md` | Pixel mechanics, Standard Events, parameters *(supplement: CAPI, EMQ, dedup)* |
| `references/audiences_targeting.md` | Warm/cold, custom audiences, lookalikes, BCOP, geo/demo sizing *(supplement: Advantage+ Audience)* |
| `references/funnels_offers.md` | FANS, Six Proven Offers, Bow Tie Formula, Value-Value-Value-Offer |
| `references/campaign_objectives.md` | Objective categories & build order *(supplement: ODAX 11→6)* |
| `references/adset_structure_budget.md` | A.P.B., Four Ad Set Groups, Michigan Method, bidding *(supplement: CBO/Advantage+)* |
| `references/ad_copy.md` | 7 Ad Building Blocks, 13 Elements of Persuasive Copy, 7 Power Questions |
| `references/creative_design.md` | Hook→image, Six Aspects of Creative, STEPPS, formats/placements *(supplement: 9:16/4:5 specs)* |
| `references/hooks_messaging.md` | UPSYD messaging, STEPPS hooks, copy formulas |
| `references/video_ads.md` | Three-Step Video Formula, EDIE, cold-traffic education |
| `references/boosted_posts.md` | Easy-Button boost, amplification, cheap "unicorn" pre-testing |
| `references/reporting_optimization.md` | Reading Ads Manager, metric priority, sequenced testing *(supplement: attribution, Ad Relevance Diagnostics)* |
| `references/scaling.md` | Five-Tier Scaling System, Massive Rapid Scaling *(supplement: CBO cadence)* |
| `references/troubleshooting.md` | 5 failure scenarios + zero-conversion diagnostic *(supplement: CAPI/attribution/learning phase)* |
| `references/SUPPLEMENT-2025.md` | **Modern Meta corrections — overrides any reference on tracking, targeting, objectives, budgeting, attribution, diagnostics, and creative specs.** |
| `checklists/` | Paste-ready: pre-flight diagnostic, account-setup completeness, pixel install/verify, pre-publish copy check, ad-creative checklist, pre-scale readiness, zero-conversions diagnostic. |
| `templates/` | Copy-paste assets: base Pixel + Lead + Purchase(value, currency) HTML, naming conventions, hook-research surveys, copy formulas, testimonial script, designer brief. |

When a stage has a matching checklist or template, surface that asset directly
rather than reproducing it from a reference.
