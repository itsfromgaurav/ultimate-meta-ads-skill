# Troubleshooting / Diagnostic Checklist

> Diagnose and fix underperforming Meta (Facebook/Instagram) campaigns — zero conversions, high CPAs, high CTR but no conversions, high shares but low conversions, and low relevance scores. Source: *Ultimate Guide to Facebook Advertising (3rd ed.)*, Troubleshooting + Ch. 29.

---

## The Five Most Common Troubleshooting Scenarios

1. Zero conversions → work the Zero Conversions Diagnostic Checklist (below)
2. CPAs are too high → work "Fixing High CPAs by Pausing Ad Sets" (below)
3. CTR is high but CPC is low, but no conversions → Three Culprits (below)
4. Social shares are high but conversions are low → Diagnostic Order (below)
5. Relevance score drops or is low → fix message-to-market match (below)

---

## 1. Zero Conversions Diagnostic Checklist

> When a campaign produces nothing after 24–48 hours, work through in order:

- [ ] **Verify the pixel is on EVERY page of the funnel** (use Facebook Pixel Helper; click each zero-conversion ad's URL and confirm it fires)
- [ ] **Verify it's the CORRECT pixel on every page** — cross-reference Ads Manager → All Tools → Pixels → your Ad Account Pixel ID against the ID shown by the Pixel Helper
- [ ] **Confirm you're optimizing for the right conversion event AND that reporting columns match** — verify the optimized event at the ad set level; customize columns to show it, save as a named preset, set as default view
- [ ] **Check that all funnel URLs are actually loading** — test load speed at https://gtmetrix.com; if slow, have a technical person clean it up
- [ ] **Check the landing pages** — click every single CTA button/link and confirm it goes where it should
- [ ] **Confirm the landing page actually HAS a CTA button or link at all**

## 2. Fixing High CPAs by Pausing Ad Sets (Troubleshooting)

- [ ] Know your target CPA
- [ ] Sort your reporting view by the last seven days
- [ ] Sort ad sets by cost of conversion, greatest to least
- [ ] Pause every ad set converting at **2–3x your target CPA**
- [ ] Catch zero-converters: sort ad sets by Amount Spent (greatest to least) and turn off any that spent **2x your CPA with zero conversions**

## 3. High CTR / Low CPC but No Conversions — Three Culprits

- [ ] **Landing page** — people click but don't convert; split test and rework the landing/registration/sales page
- [ ] **Ad scent** — no continuity between ad and landing page; view them side by side and make them match
- [ ] **Targeting** — unqualified traffic; re-examine. (Liking Oprah doesn't mean someone reads books — verify the interest correlates with your market)

## 4. High Social Shares but Low Conversions — Diagnostic Order

- [ ] **Re-evaluate your campaign objective FIRST** — Traffic/Engagement objectives deliver traffic/engagement, NOT conversions; switch to a conversion objective
- [ ] **Look at your ad copy** — is the hook strong? Make the next step crystal clear; add a URL in the copy
- [ ] **Rework your offer** — high shares mean the hook resonates, so the offer is most likely missing the mark
- [ ] **Re-examine ad copy and creative** — the ad may be engaging people for the wrong reasons

## 5. Fix a Low Relevance Score = fix message-to-market match (Troubleshooting)

- [ ] Confirm the offer is what people actually want
- [ ] Rewrite copy to hit their biggest pains, desires, and fears
- [ ] Move the prospect from the undesirable BEFORE state to the desirable AFTER state

## 6. Reach / policy warnings

- [ ] If Facebook shows **"Your ad's reach may be slightly lower"** (usually long copy or a disliked image), it's only a heads-up — submit anyway; often won't affect impressions
- [ ] After hitting **"Place order,"** double-check in Ads Manager that the campaign is listed with no errors

---

## Diagnostic pitfalls to avoid

- [ ] Don't assume high engagement = conversions (often the objective is wrong or the offer misses)
- [ ] Don't trust high CTR / low CPC alone — meaningless if conversions don't follow
- [ ] Don't assume an interest correlates with your market — verify first
- [ ] Don't make subjective income-claim hooks (e.g., "make $30,000 in 30 days") — likely Policy trouble
- [ ] Don't over-react to the "reach may be slightly lower" warning — it's not a disapproval
- [ ] Don't judge an ad set on lead cost alone — the most expensive leads can be the highest quality; check downstream sales/revenue before pausing

---

## Tools

| Tool | Use |
|---|---|
| GTmetrix (https://gtmetrix.com) | Test funnel URL load speed when conversions are zero |
| Facebook Pixel Helper (Chrome ext.) | Verify the pixel fires, and that it's the correct pixel, on every page |

## Key numbers / thresholds

| Item | Value |
|---|---|
| Zero-conversion review window | 24–48 hours |
| Pause threshold (high CPA) | converting at 2–3x target CPA |
| Zero-converter kill threshold | spent 2x CPA with zero conversions |
| Relevance Score scale | 1–10 (10 best) |
| Ad fatigue zone | Frequency ~10+ |
