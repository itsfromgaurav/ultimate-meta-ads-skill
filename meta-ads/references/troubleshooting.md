# troubleshooting

> How to diagnose and fix underperforming Facebook/Instagram ad campaigns — from zero conversions to high CPAs, weak conversion-to-engagement ratios, and policy/reach warnings.

## Core frameworks

### The Five Most Common Troubleshooting Scenarios
When a Facebook ad campaign underperforms, diagnose it against these five recurring failure patterns, each with its own fix path (Troubleshooting: 5 common scenarios):

1. **Zero conversions** — work the Zero Conversions Diagnostic Checklist (below).
2. **CPAs are too high.**
3. **CTR is high but CPC is low** (but conversions don't follow) — see "High CTR / Low CPC but no conversions" below.
4. **Social shares are high but conversions are low** — see the diagnostic order below.
5. **Relevance score drops or is low.**

Other scenarios not covered in depth but worth knowing: low click-through rate (CTR), high cost per click (CPC), high CPA with large target audiences, ads not getting impressions from Facebook, and CPA rising as you scale campaigns.

### High CTR / Low CPC but No Conversions: Three Culprits
A high CTR and low CPC look good, but not if you're getting no conversions or high CPAs. The problem is one of three things (Troubleshooting: 5 common scenarios):

1. **Landing page** — people click but don't convert (not opting in, signing up, or buying). Fix by split testing and reworking the landing/registration/sales page.
2. **Ad scent** — there's no "smell"/continuity between the ad and the landing page. Look at the ad and the landing page side by side, check for similarities or familiar components, then make them match.
3. **Targeting** — you've been sending unqualified traffic; re-examine targeting. Interest-targeting caveat: just because someone likes Oprah doesn't mean they read books — make sure the interest actually correlates with your target market.

### High Social Shares but Low Conversions: Diagnostic Order
High social engagement (likes, comments, shares) does not guarantee conversions. Work through these in order (Troubleshooting: 5 common scenarios):

1. **Re-evaluate your campaign objective FIRST** — if you're running a Traffic or Page Post Engagement objective, the algorithm delivers traffic or engagement, NOT conversions. Switch to a conversion objective.
2. **Look at your ad copy** — is the hook strong, and does the copy lead to the next step in the customer journey? Make the next step crystal clear. (Case study: an ad with very high social shares wasn't converting; they revamped the copy, created a strong offer and call to action, and ADDED A URL in the copy, after which it "started converting like crazy.")
3. **Rework your offer** — high shares mean the ad resonates and the hook is solid, so the offer is most likely missing the mark.
4. **Re-examine ad copy and creative** — the ad may be engaging people for the wrong reasons, so they miss the point that would lead them to convert.

## Tactics & best practices

**Tools**
- **GTmetrix** (https://gtmetrix.com) — test funnel URL load speed when conversions are zero and you suspect a page-load, caching, or other interference issue. If load speed is the problem, bring in a technical person to resolve the issues making URLs load slowly. (Troubleshooting: 5 common scenarios)
- **Facebook Pixel Helper** (Chrome extension) — verify the pixel fires, and that it's the correct pixel, on every page of the funnel. (Troubleshooting: 5 common scenarios)

**Reach/policy warnings**
- If Facebook shows **"Your ad's reach may be slightly lower"** (typically triggered by long copy or a disliked image), it's just a heads-up — Facebook won't disapprove the ad at this stage. Just submit it and see what happens; often it won't affect your impressions at all. After hitting **"Place order,"** double-check in Ads Manager that the campaign is listed with no errors. (Ch. 11)

## Checklists

### Zero Conversions Diagnostic Checklist
When a campaign produces nothing after 24–48 hours (the worst case), work through this in order (Troubleshooting: 5 common scenarios):

- [ ] **Verify the pixel is on EVERY page of the funnel.** Use the Facebook Pixel Helper Chrome extension; click the URL in every ad with zero conversions and confirm the pixel fires.
- [ ] **Verify it's the CORRECT pixel on every page.** Clients can have multiple ad accounts/companies and multiple pixels on one site. Cross-reference: Ads Manager > All Tools dropdown > Pixels, find your Ad Account Pixel ID on the right side, and confirm it matches the Pixel ID shown by the Facebook Pixel Helper on every page.
- [ ] **Confirm you're optimizing for the right conversion event AND that your reporting columns match.** The event you optimize for may not appear in the standard Ads Manager report. Verify the optimized event at the ad set level; then customize report columns to show that conversion event, save the view as a named preset, and set it as the default view.
- [ ] **Check that all funnel URLs are actually loading.** Possible page-load-speed issue, caching issue, or other interference. Test load speed at https://gtmetrix.com; if slow, have a technical person clean it up.
- [ ] **Check the landing pages** — click every single CTA button/link and confirm it goes where it should.
- [ ] **Confirm the landing page actually HAS a CTA button or link at all.** (It has happened that a client wanted conversion traffic to a page with no button or link anywhere.)

## Copy/templates

Example of an income-claim hook that violates policy (avoid; see Pitfalls):

```
make $30,000 in 30 days
how to create a six-figure income as a coach
```

## Pitfalls to avoid

- **Don't make subjective income-claim hooks.** Any hook promising a specific income — and especially with a timeframe (e.g., "make $30,000 in 30 days") — is very likely to cause trouble with Facebook policy. Hooks like "how to create a six-figure income as a coach" make a subjective income claim and may run into policy issues. (Ch. 16: Hacking the Hook)
- **Don't over-react to the "Your ad's reach may be slightly lower" warning.** It's only a heads-up (usually for long copy or a disliked image), not a disapproval — submit anyway, since it often won't affect impressions. (Ch. 11)
- **Don't assume high engagement = conversions.** High social shares, likes, and comments do not guarantee conversions; often the objective is wrong (Traffic/Engagement instead of Conversions) or the offer is missing the mark. (Troubleshooting: 5 common scenarios)
- **Don't trust high CTR / low CPC alone.** Those metrics look good but mean nothing if conversions don't follow — the culprit is usually the landing page, ad scent, or targeting. (Troubleshooting: 5 common scenarios)
- **Don't assume an interest correlates with your market.** Liking Oprah doesn't mean someone reads books — verify the interest actually maps to your target market before targeting it. (Troubleshooting: 5 common scenarios)
