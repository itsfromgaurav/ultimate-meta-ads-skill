# SUPPLEMENT-2025 — Modern Meta Corrections
> Load this alongside any reference it overrides. Where this conflicts with a reference, THIS wins.

This file corrects a ~2017 Facebook Ads book against the state of Meta advertising in 2025–2026. The 2017 material predates iOS 14.5 App Tracking Transparency, the Conversions API, the Pixel→Dataset rename, ODAX objective consolidation, the Advantage+ suite, Campaign Budget Optimization being renamed Advantage campaign budget, the 2026 attribution-window removals, the deprecation of the manual 8-event AEM system, Ad Relevance Diagnostics, and vertical-first creative. Treat any 2017 instruction touching these areas as outdated.

## How to use this file

| Topic | Overrides reference(s) | One-line correction |
|---|---|---|
| Conversions API & server-side tracking | pixel_tracking, reporting_optimization, troubleshooting | Run BOTH browser Pixel and CAPI for the same events with a shared event_id; "Pixel" is now a "Dataset." |
| iOS14 ATT, AEM & domain verification | pixel_tracking, account_setup, audiences_targeting | The manual 8-event AEM system is gone (June 2025); signal quality (EMQ via CAPI) is the lever; verify your domain. |
| Advantage+ suite (Sales/Audience/Placements/Creative) | audiences_targeting, campaign_objectives, adset_structure_budget, creative_design | ASC is now "Advantage+ Sales"; targeting is mostly soft "suggestions"; placements and creative are auto by default. |
| ODAX objective consolidation | campaign_objectives | The 11 legacy objectives collapsed into 6 outcomes; "Conversions" and "Catalog Sales" are now sub-settings of Sales. |
| Advantage campaign budget (CBO) vs ABO | adset_structure_budget, scaling | CBO renamed "Advantage campaign budget"; ad-set spend caps are now AVERAGE not hard; Advantage+ is the new default. |
| Attribution windows & settings | reporting_optimization, pixel_tracking | Attribution is ad-set level; default is 7-day click + 1-day view; 7d/28d VIEW windows removed Jan 12, 2026. |
| Ad relevance diagnostics & learning phase | reporting_optimization, troubleshooting | The 1–10 Relevance Score is gone (2019); three rankings replace it; learning phase = ~50 events/7 days. |
| Creative specs | creative_design, video_ads, troubleshooting | Vertical-first: 9:16 for Reels/Stories, 4:5 for Feed; the 20% text rule is retired; Advantage+ Creative auto-generates variants. |

---

## Conversions API (CAPI) & Server-Side Tracking

**What changed.** Tracking is now a hybrid, redundant setup — not "drop a pixel and it works." The browser Meta Pixel (client-side JavaScript) and the Conversions API / CAPI (server-to-server) are used TOGETHER to send the SAME events, because browser-only tracking loses large amounts of data to iOS App Tracking Transparency (ATT, since iOS 14.5), ad blockers, browser cookie restrictions (Safari ITP, Chrome tracking protections), and consent gating. Meta also renamed "Pixel" to "Dataset" in Events Manager (rolled out through 2024).

**What the book says (now wrong).** The ~2017 book treats the browser Pixel as the sole, sufficient tracking mechanism — "install the pixel and it just works," reliably capturing PageView, ViewContent, AddToCart, Purchase, etc. directly from the browser. It assumes near-complete client-side capture, treats the "Pixel ID" as the canonical tracking entity, and frames reporting/optimization/troubleshooting entirely around browser-fired events. It has no concept that browser-only tracking now silently loses a large share of conversions.

**What's true today.**
- **Datasets (renamed):** A Dataset is a container that unifies web (Pixel), server (CAPI), app, offline, and messaging events under one ID. For existing pixels, **Dataset ID = the old Pixel ID** — no re-tagging required. Events Manager now says "Dataset ID" / "Connect a new data source" where it said "Pixel."
- **Why both are needed:** The Pixel still captures rich browser signals — notably the `_fbp` cookie → `fbp` parameter, and the `fbclid` click ID → `fbc` parameter. CAPI fires the same event from your server with first-party/CRM data (hashed email, phone, name, IP, user agent) that survives browser/cookie loss. Running both maximizes events received and match rate.
- **Deduplication via `event_id`:** Each conversion gets a unique `event_id` sent IDENTICALLY on both the Pixel event and the CAPI event, and the `event_name` must match (e.g., Purchase, AddToCart). Meta also uses `fbp` as a secondary match signal. Same `event_name` + same `event_id` → Meta keeps one, discards the duplicate. **Deduplication window is ~48 hours.** Misconfigured `event_id` is the #1 cause of double-counted conversions.
- **Event Match Quality (EMQ):** Meta scores how well events match Meta user profiles on a **0–10 scale**, shown per event in Events Manager. **Aim for 6.0+; 8.0+ is strong.** Hashed (SHA-256) email is the single strongest identifier; phone, fbc, fbp, IP, and user agent raise the score. Higher EMQ = better attribution and cheaper optimization.
- **Conversions API Gateway (CAPI Gateway):** Meta-provided low/no-code way to deploy CAPI on your own cloud (typically AWS) without custom dev work — self-serve in Events Manager (Settings → Conversions API → Set up Gateway), ~10–15 min deploy. Captures Pixel events server-side and forwards them, auto-updating with host-admin consent. Note: Meta has been steering many advertisers toward partner integrations rather than self-hosting the Gateway.
- **Setup options (Meta's official comparison):** (1) **Partner/commerce integration** — Shopify, WooCommerce, WordPress, Wix, BigCommerce, Google Tag Manager (server container), Tealium, Zapier; few clicks, low/no code, often recommended. (2) **CAPI Gateway** — self-hosted on cloud, low-code. (3) **Direct (manual) integration** — developers call the Graph API `/events` endpoint directly; most control, most effort. Shopify/major platforms include CAPI at no extra Meta cost.

**Do this now.**
- [ ] Confirm you run BOTH the browser Pixel and CAPI for the same events.
- [ ] Find your Dataset ID in Events Manager (it equals your old Pixel ID); replace "Pixel ID" → "Dataset ID" and "Pixel" → "Dataset (Pixel data source)" in docs/skill copy.
- [ ] Implement deduplication: unique, matching `event_id` on Pixel AND CAPI events with identical `event_name`; verify in Events Manager Test Events that events show "Deduplicated." Window is ~48h.
- [ ] Check EMQ per event; target 6.0+ (ideally 8.0+). Add hashed (SHA-256) email and phone, plus fbc (from fbclid), fbp (from `_fbp`), client IP, and user agent to CAPI payloads.
- [ ] Pick a setup path: easiest is a partner/commerce integration (Shopify, WooCommerce, WordPress, GTM server-side, Tealium, Zapier); otherwise deploy the CAPI Gateway (~10–15 min on AWS); use direct Graph API only if you need full control.
- [ ] Use Events Manager Test Events + Diagnostics tab to troubleshoot — verify CAPI events arrive, dedup works, no required parameters missing — instead of debugging only the browser pixel.

**Sources.**
- https://developers.facebook.com/docs/marketing-api/conversions-api
- https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/
- https://www.facebook.com/business/help/433493041367251
- https://developers.facebook.com/docs/marketing-api/gateway-products/conversions-api-gateway/setup
- https://analyzify.com/hub/event-deduplication-for-meta-conversions
- https://www.leadsie.com/blog/all-you-need-to-know-about-facebook-metas-new-datasets
- https://docs.getelevar.com/docs/how-to-find-facebook-pixel-or-dataset-id
- https://stape.io/blog/how-to-improve-event-match-quality-facebook
- https://www.datahash.com/docs/meta-conversions-api-gateway/

---

## iOS14 ATT, Aggregated Event Measurement & Domain Verification

**What changed.** MAJOR CHANGE — the manual AEM system in the book and most online guides is GONE. As of **June 2025**, Meta removed the 8-event-per-domain cap and eliminated manual event prioritization/ranking. The standalone "Aggregated Event Measurement" / Event Configuration tab in Events Manager was retired. AEM is now fully automated.

**What the book says (now wrong).** The ~2017 book predates ATT entirely. It assumes deterministic Pixel tracking with full IDFA/user-level matching, large stable Custom/Lookalike Audiences, and a default 28-day-click/28-day-view attribution model — none of which hold. It has no concept of ATT, AEM, the (now-removed) 8-event cap, event prioritization, domain verification, the Conversions API, EMQ, modeled conversions, or SKAdNetwork. `account_setup` omits domain verification (now a required Brand Safety step); `audiences_targeting` overstates retargeting/lookalike reliability for iOS opted-out users.

**What's true today.**
- **AEM is automated:** Meta automatically aggregates all eligible standard events and custom conversions behind the scenes — **no 8-event list, no drag-and-drop ranking, no per-domain prioritization.** The old mechanics (8 prioritized events per eTLD+1 primary domain, one highest-priority event reported per session, 72-hour cool-down after reshuffling, value optimization consuming a 4–8 slot range) no longer apply to day-to-day setup.
- **What replaced it — signal quality, not event selection:** The lever you control is **Event Match Quality (EMQ), a 1–10 score.** Pixel-only typically yields EMQ ~3.5–5.0; **Pixel + CAPI properly configured raises it to ~7.5–9.0. Target EMQ above 7.0.** Requires consistent schema across Pixel and CAPI (matching `event_id`, `event_name`, value, currency) plus deduplication. **CAPI is now effectively mandatory** for competitive performance, especially for Advantage+ Shopping/Sales.
- **ATT impact (still real):** Apple's ATT prompt still gates the IDFA. Opt-in rates vary by source — roughly **25%** low end, **~35%** average (Adjust Q2 2025), up to **~50%** (AppsFlyer global). Opted-out iOS traffic loses deterministic user-level matching, shrinks retargeting/custom-audience sizes, and slows the learning phase. Meta fills the gap with **modeled (statistical) conversions** blended into reporting, plus **SKAdNetwork (SKAN 4.0: up to 4-digit campaign IDs = 10,000 options, multiple conversion windows/postbacks)** for app campaigns.
- **Attribution windows (second major change):** Default is now **7-day click + 1-day view.** The 7-day-view and 28-day-view windows were removed **Jan 12, 2026** (Ads Insights API / reporting). Remaining selectable windows: 1-day view, 1-day click, 7-day click, and 28-day click (reporting only, not optimization). Expect **30–40% fewer attributed conversions** on awareness/long-cycle campaigns purely from the shorter view window — not a performance drop.
- **Domain verification (still required, process unchanged):** Verify in **Business Settings > Brand Safety > Domains** (Business Portfolio). Three methods, pick ONE: (1) **DNS TXT record** — add Meta's TXT record at your DNS host (Host = @), wait for propagation (minutes, up to 72 hours), click Verify; (2) **HTML file upload** — download Meta's HTML file, upload to site root, confirm it loads, click Verify; (3) **Meta-tag** — paste the `<meta>` tag into the homepage `<head>`, confirm in source, click Verify. Applies to the primary domain (eTLD+1). Keep the record/file/tag in place. Needed to control link editing and for conversion-measurement trust.

**Do this now.**
- [ ] Stop trying to configure or rank 8 events in Events Manager — the AEM Event Configuration tab no longer exists (removed June 2025). Meta aggregates eligible events automatically.
- [ ] Verify your primary domain (eTLD+1) under Business Settings > Brand Safety > Domains using ONE method (DNS TXT is most durable); leave the record in place.
- [ ] Install CAPI alongside the Pixel and deduplicate (shared `event_id`, matching `event_name`/value/currency). This is the #1 lever now.
- [ ] Check EMQ per event and push every key event **above 7.0** by sending hashed customer data (email, phone, external_id, fbp/fbc, IP, user agent).
- [ ] Update attribution expectations: default is 7-day click + 1-day view. The 7-day and 28-day VIEW windows were removed Jan 12, 2026 — don't benchmark against old 28-day-view counts.
- [ ] Don't expect deterministic tracking from ATT opted-out iOS users; rely on modeled conversions and (for apps) SKAdNetwork. Size retargeting/lookalike audiences accordingly.
- [ ] Favor broad Advantage+ campaigns fed by clean, high-EMQ purchase signal over narrow manual audiences that ATT signal loss erodes.

**Sources.**
- https://www.facebook.com/business/help/721422165168355
- https://www.facebook.com/business/help/126789292407737
- https://www.facebook.com/business/help/387440828988900
- https://developers.facebook.com/docs/sharing/domain-verification/verifying-your-domain/
- https://en-gb.facebook.com/business/help/321167023127050
- https://www.facebook.com/business/help/286768115176155
- https://en-gb.facebook.com/business/help/193250612476055
- https://www.facebook.com/business/help/378857770047703
- https://seresa.io/blog/ad-platform-event-specifications/meta-removed-the-8-event-cap-in-june-2025
- https://www.conversios.io/blog/meta-aggregated-event-measurement/
- https://www.jonloomer.com/meta-announces-big-changes-to-website-conversion-campaigns/
- https://www.dataslayer.ai/blog/meta-ads-attribution-window-removed-january-2026
- https://www.jonloomer.com/meta-ads-attribution-2026/
- https://segwise.ai/blog/meta-aem-vs-skan-2025-ios-attribution
- https://splitmetrics.com/blog/apple-skadnetwork-guide/
- https://www.adsgo.ai/blog/meta-conversion-api-2026/

---

## Meta Advantage+ Suite (Sales / Audience / Placements / Creative)

**What changed.** "Advantage+ Shopping Campaigns" (ASC) was renamed **"Advantage+ Sales campaigns"** in early 2025 — same engine, broader positioning (no longer ecommerce-only; works for Sales, Leads, App Promotion). The old ASC name/abbreviation is deprecated. By 2025 Meta made Advantage+ the **DEFAULT (and often only)** setup path for Sales, Leads, and App campaigns; for Sales objectives you can no longer pick a fully manual campaign setup — you toggle Advantage+ features off inside the Advantage+ flow.

**What the book says (now wrong).** The ~2017 book teaches: (1) build precise saved audiences by stacking many Detailed-Targeting interests/behaviors, narrow with AND/exclusions, rely on Lookalikes/Custom Audiences as hard targeting; (2) pick from the long legacy objective list with everything manual, no AI Advantage+ path; (3) many granular ad sets, one audience each, ad-set budgets, manual placement picking; (4) upload fixed creative that runs exactly as uploaded, no automatic AI alteration. All four are outdated: interest stacking/exclusions are deprecated or demoted to soft suggestions, objectives default to AI flows, structure is broad-and-consolidated, and creative is auto-modified by default unless you opt out.

**What's true today.**
- **Advantage+ Sales structure:** Old ASC was rigid (one ad set, ~150-ad cap, an existing-customer budget cap slider, almost no targeting input). Now: **multiple ad sets supported (each up to ~50 ads)**, plus real audience inputs. The existing-vs-new-customer budget cap remains an optional control. Meta-cited: Advantage+ Sales with Advantage+ Audience **~7.2% lower cost per result**; broader vendor benchmarks ~12% lower cost per purchase vs manual and up to ~32% lower CPA (directional).
- **Advantage+ Audience — controls vs suggestions:**
  - **CONTROLS = HARD limits Meta strictly obeys:** Locations, Minimum age, Excluded custom audiences, Languages (Locations > Edit > Show more options).
  - **SUGGESTIONS = SOFT priors only:** Custom audiences, Lookalikes, Age, Gender, Detailed Targeting interests — Meta serves these first but goes outside them when it predicts better performance. Adding interests no longer locks targeting; it seeds the AI.
  - Advantage+ Audience is **ON by default for Leads/App/Sales.** Switch to **"original audiences"** (formerly just Audiences) for hard targeting (awareness/traffic, regulated targeting, very small/cold pixels).
  - **DEPRECATED:** Detailed Targeting **EXCLUSIONS removed January 2025.** Special Ad Category forces Advantage+ Audience with limited control.
- **Advantage+ Placements:** Default and recommended; spreads across **25+ placements** (FB/IG feeds, Stories, Reels, Marketplace, Search, Messenger, Audience Network, etc.). 2025/2026 **SOFT-OVERRIDE:** excluding placements at ad-set level on Sales/Leads triggers a default-ON checkbox letting Meta spend **up to 5% of budget PER excluded placement** when likely to improve performance (exclude 4 → up to ~20% can leak). To truly block: uncheck that box per exclusion, or use account-level **Advertising Settings > Placement controls** (bypasses override, up to 48h to apply).
- **Advantage+ Creative Enhancements:** ~20+ AI enhancements, most ON by default.
  - **Safe/low-risk:** Visual touch-ups, Adjust brightness & contrast, Relevant comments, catalog ones (Dynamic media, Adapt to placement, Dynamic description).
  - **Test carefully:** Enhance CTA, Add overlays, Expand image (outpainting), Generate background, 3D/image animation, Dynamic overlays, video touch-ups.
  - **High-risk (often turn OFF):** Text improvements (rewrites copy, can break disclaimers), Music (off-tone audio), Site links.
  - Toggle per ad in Ads Manager under the Advantage+ creative section > Edit; preview before publishing.

**Do this now.**
- [ ] Stop hard-stacking 5+ interests. In Advantage+ Audience leave Detailed Targeting empty or add only 1–3 broad seed interests as a SUGGESTION; feed strong/refreshed creative plus clean pixel/CAPI data instead.
- [ ] Use Audience CONTROLS (hard) only for non-negotiables: location, minimum age, language, excluded custom audiences (e.g., exclude recent purchasers). Everything else goes in SUGGESTIONS, knowing Meta can exceed them.
- [ ] Run a clean test via Ads Manager Experiments split test (not duplicated campaigns): Cell A = Advantage+ Sales + Advantage+ Audience + Advantage+ Placements; Cell B = manual control (original audiences + interest stack + manual placements). Hold objective, creative, optimization event, and budget constant; run 7+ days to stat-sig and let each exit learning (~50 conversions/week per ad set).
- [ ] Prefer Advantage+ broad when the account has volume: ~50+ weekly conversions, ~$50+/day budget, a few hundred+ pixel conversion events. For thin/cold pixels or regulated targeting, keep original audiences with hard constraints until signal builds.
- [ ] Audit Advantage+ Creative per ad before launch: turn OFF Text improvements, Music, and Site links for brand/compliance-sensitive ads; keep low-risk touch-ups. Review image expansion/background generation so AI doesn't crop logos or distort product.
- [ ] Fix placement leakage: when excluding placements (e.g., Audience Network) on Sales/Leads, UNCHECK the default "allow limited spending to excluded placements" box, or enforce at account-level Advertising Settings > Placement controls (up to 48h).
- [ ] Update playbooks/skill docs: replace "Advantage+ Shopping/ASC" with "Advantage+ Sales," note Detailed Targeting exclusions removed (Jan 2025), and that full manual campaign setup is unavailable for Sales objectives.
- [ ] Use the existing/new-customer budget cap inside Advantage+ Sales to control prospecting vs retargeting mix instead of separate manual campaigns.

**Sources.**
- https://www.facebook.com/business/help/938372127764391
- https://www.facebook.com/business/help/273363992030035
- https://www.facebook.com/business/ads/meta-advantage-plus/audience
- https://www.facebook.com/business/ads/meta-advantage/advantage-plus-shopping-ads
- https://www.jonloomer.com/meta-advertising-changes-2025/
- https://www.jonloomer.com/advantage-audience-vs-original-audiences/
- https://www.jonloomer.com/advantage-plus-audience-best-practices-guide/
- https://www.jonloomer.com/advantage-plus-creative-enhancements/
- https://blog.adnabu.com/facebook/meta-advantage-plus-sales-campaigns/
- https://blog.adnabu.com/facebook/meta-advantage-plus-audience/
- https://theoptimizer.io/blog/meta-ads-placement-control-in-2026-how-to-actually-block-placements-its-not-as-simple-anymore
- https://adsuploader.com/blog/advantage-plus-creative-enhancements
- https://www.foxwelldigital.com/blog/metas-new-ad-campaign-type-what-it-is-why-it-matters-and-how-to-make-it-perform

---

## ODAX Objective Consolidation: 11 Legacy Objectives → 6 Outcomes

**What changed.** Meta's **Outcome-Driven Ad Experiences (ODAX)** replaced the legacy objective system. Announced late 2021, rolled out through 2022, and the ONLY system available since 2022–2023 — fully standard across Facebook, Instagram, Threads, Messenger, and Audience Network as of 2025–2026. The old 11 objectives (grouped into Awareness / Consideration / Conversion columns) collapse into **6 outcome-based objectives** chosen at the CAMPAIGN level as the first setup step.

**What the book says (now wrong).** The ~2017 book instructs advertisers to pick from ~10–11 separate campaign objectives in three funnel columns — choose "Conversions" for website purchases, "Lead Generation" for forms, "Brand Awareness"/"Reach" for top-of-funnel, "Video Views"/"Messages"/"Engagement" as distinct consideration objectives. That selection screen no longer exists. Any instruction to "select the Conversions objective" or "select Catalog Sales" is wrong — those are now sub-settings (conversion location + performance goal) inside Sales.

**What's true today.**

**The 6 objectives (exact Ads Manager names):** 1. Awareness  2. Traffic  3. Engagement  4. Leads  5. App promotion  6. Sales

**Old-to-new mapping (legacy 11 → 6):**
- Brand Awareness + Reach → **AWARENESS**
- Traffic → **TRAFFIC**
- Engagement (Post/Page) + Video Views + Messages → **ENGAGEMENT**
- Lead Generation → **LEADS**
- App Installs → **APP PROMOTION**
- Conversions + Catalog Sales + Store Traffic → **SALES**

- **Where conversions live now:** Standalone "Conversions" and "Catalog Sales" no longer exist. Website/app purchase optimization lives under **SALES.** After picking Sales, set a **Conversion location** (Website, App, Website and app, Messaging apps/Messenger/WhatsApp/Instagram, or Calls) and a performance goal (Maximize number of conversions, Maximize value, optimizing for Purchase, Add to Cart, Initiate Checkout, etc.). Catalog Sales is now a Sales campaign using a product catalog (the Advantage+ catalog ads format). Requires Meta Pixel/dataset + Conversions API.
- **Where lead options live now:** Old "Lead Generation" is now **LEADS.** Choose Conversion location: Instant forms (native on-Meta), Instant forms + Messenger, Messenger, **Website** (website lead forms — these used to require the Conversions objective), Calls (phone leads), or App. **"Conversion leads"** optimization (CRM-integrated, optimizes for down-funnel lead quality) lives here. Advantage+ leads campaigns are an AI-automated build of the Leads objective.
- **Other conversion locations by objective:**
  - **Awareness:** optimize for Reach, Impressions, Ad recall lift, ThruPlay/2-sec video views. No tracked conversion location.
  - **Traffic:** destination = Website, App, Messaging apps, Instagram profile, Calls; optimize for Landing page views (recommended) or Link clicks.
  - **Engagement:** conversion locations include On your ad (post engagement/video views), Messaging apps (Messenger/WhatsApp/Instagram Direct), Website, App, Facebook Page. Absorbs the deprecated Messages and Video Views objectives.
  - **App promotion:** app installs or app events; uses Advantage+ app campaigns (AAA) with Advantage+ placements.
- **Renamed/deprecated:** Brand Awareness, Reach, Post Engagement, Video Views, Messages, Lead Generation, App Installs, Conversions, Catalog Sales, Store Traffic, and standalone "Page Likes" no longer appear as selectable objectives. Store Traffic was effectively retired (folded into Sales/awareness use cases).

**Do this now.**
- [ ] When creating a campaign, expect exactly 6 objectives: Awareness, Traffic, Engagement, Leads, App promotion, Sales. Pick the outcome, not a legacy objective name.
- [ ] For website/app purchases: choose SALES → Conversion location = Website (or App) → performance goal optimizing for Purchase/Add to Cart/etc. Don't look for a "Conversions" objective — it's gone.
- [ ] For product-catalog (DPA/dynamic) ads: choose SALES and attach a catalog; "Catalog Sales" is no longer top-level.
- [ ] For lead capture: choose LEADS → Conversion location = Instant forms, Messenger, Website, Calls, or App. Website lead forms now live here.
- [ ] For higher-quality leads, enable Conversion leads optimization under LEADS (requires CRM/offline event integration).
- [ ] For messaging/DMs and video views: choose ENGAGEMENT (standalone Messages and Video Views were merged into it).
- [ ] Ensure Meta Pixel/dataset + CAPI are configured before running Sales or website-based Leads campaigns.
- [ ] Consider Advantage+ variants (Advantage+ Sales, Advantage+ App, Advantage+ Leads) as AI-automated builds layered on Sales/App/Leads.

**Sources.**
- https://www.facebook.com/business/help/1438417719786914
- https://www.facebook.com/business/help/535561519986477
- https://www.facebook.com/business/help/1362234537597370
- https://www.facebook.com/business/ads/meta-advantage-plus/leads
- https://www.facebook.com/business/help/309994246788275
- https://www.socialmediaexaminer.com/how-to-create-facebook-ad-campaigns-with-odax/
- https://bir.ch/blog/facebook-ad-objectives
- https://www.flighted.co/blog/every-meta-campaign-objective-explained
- https://www.jonloomer.com/odax-facebook-simplifies-campaign-objectives/

---

## Advantage Campaign Budget (formerly CBO) vs Ad-Set Budgets (ABO)

**What changed.** "Campaign Budget Optimization (CBO)" was renamed by Meta to **"Advantage campaign budget"** (part of the Meta Advantage / Advantage+ automation suite) in 2022; the mechanic is unchanged. Ad-set-level budgeting (one budget per ad set) is the alternative, commonly called **"ABO"** by practitioners — Meta's UI just calls it an "ad set budget." The official label is the **"Advantage campaign budget" toggle** (on = campaign budget, off = ad set budgets).

**What the book says (now wrong).** The ~2017 material assumes budgets live at the ad-set level by default, with the advertiser manually allocating and rebalancing spend across ad sets, and "scaling" meaning manually increasing individual ad-set budgets. It predates CBO entirely (launched late 2018, near-mandatory 2019, renamed Advantage campaign budget 2022). It doesn't cover campaign-level optimization, average (vs hard) ad set spend limits, the ~50-events learning threshold, current cost cap/bid cap strategies, or the Advantage+ consolidation now deprecating legacy manual structures.

**What's true today.**
- **How it works:** With Advantage campaign budget ON, you set ONE budget at the campaign level. Meta's delivery distributes spend across ad sets in real time toward the lowest-cost / best-performing opportunities (using the auction, not a fixed allocation). With ad-set budgets, each ad set has its own fixed daily/lifetime budget.
- **Budget type & constraints:** Campaign budget can be **Daily or Lifetime.** All ad sets in a campaign-budget campaign must **share the same budget type** (no mixing). Set the on/off choice and budget type at creation; toggling later resets the learning phase.
- **Ad-set spend limits (changed mechanic):** You can still steer spend with ad set spend limits, but Meta converted these from HARD caps to **"AVERAGE" limits.** A "maximum ad set spend limit" now means Meta won't exceed that amount **PER DAY ON AVERAGE** (may exceed a given day, balanced over ~7 days), not a hard daily ceiling. A **minimum ad set spend limit** forces a floor of spend into specific ad sets (useful to guarantee each exits learning). Daily overspend tolerance: **~25%** over an ad set's daily budget normally, **up to ~75%** when budget sharing/campaign budget is active, balanced across a 7-day window.
- **Bid strategies:** Highest volume / Highest value (`LOWEST_COST_WITHOUT_CAP`), Cost per result goal / Cost cap (`COST_CAP`), Bid cap (`LOWEST_COST_WITH_BID_CAP`), and ROAS goal. The API-approved strategies for the Advantage+ structure are explicitly `LOWEST_COST_WITHOUT_CAP`, `COST_CAP`, and `LOWEST_COST_WITH_BID_CAP`.
- **When to use which:** Use **Advantage campaign budget (CBO)** for SCALING and when you have multiple SIMILAR ad sets and want Meta to push spend to winners; reduces manual work, per-Meta data ~4.6% lower CPA and improved ROAS in multi-audience setups. Use **ad-set budgets (ABO)** for clean TESTING (forcing equal spend per audience/creative for a fair read), protecting spend across distinct audiences, and at low budgets where CBO would starve smaller ad sets. Common workflow: **TEST in ABO, then SCALE in CBO.**
- **Learning phase:** Still **~50 optimization events per ad set per week** to exit learning. With CBO, the campaign needs roughly 50 events across the relevant ad sets; significant edits (budget change >~20%, changing optimization event, toggling Advantage campaign budget) reset learning ("Learning limited" if it never accumulates enough events).
- **Broader 2025–2026 shift:** Meta is consolidating manual Sales/Leads/App campaigns into the unified Advantage+ structure. **Marketing API v24.0 (Oct 8, 2025)** blocked creation of new legacy Advantage Shopping (ASC) and Advantage App (AAC) campaigns; **v25.0 (Q1 2026)** makes this a breaking change across versions. A campaign is in "Advantage+ state" when three levers are on: Advantage+ campaign budget, Advantage+ audience, and Advantage+ placements. The `existing_customer_budget_percentage` field is being deprecated (use separate ad sets with custom audiences instead).

**Do this now.**
- [ ] Decide CBO vs ABO by goal: ABO for testing new audiences/creatives (equal spend = clean read), CBO for scaling proven winners. Don't test in CBO unless you add minimum ad set spend limits.
- [ ] When using CBO, set MINIMUM ad set spend limits to guarantee each ad set exits the learning phase (~50 events/week); remember MAXIMUM limits are now AVERAGE caps, not hard daily ceilings.
- [ ] Keep all ad sets in a CBO campaign on the same budget type (all daily or all lifetime) — Meta forbids mixing.
- [ ] Scale by raising the campaign budget ~20% every 2–3 days to avoid resetting the learning phase; avoid large jumps.
- [ ] For big scaling jumps, DUPLICATE the campaign at the higher target budget and run both rather than editing the original (preserves the winner's learning history); compare after ~1 week. Duplication restarts learning on the copy, so prefer incremental increases when possible.
- [ ] To add new creative to a winning ad set, duplicate the ad set and add creative in the copy rather than editing the original, to protect existing learning.
- [ ] Set the Advantage campaign budget toggle and budget type at campaign CREATION; toggling later resets learning.
- [ ] Choose bid strategy deliberately: Highest volume (no cap) to spend full budget, Cost cap to hold a target CPA while scaling, Bid cap for strict auction control.
- [ ] Audit API/automation workflows for the legacy ASC/AAC deprecation (API v24.0 Oct 2025, v25.0 breaking Q1 2026) and migrate to the unified Advantage+ structure; stop relying on `existing_customer_budget_percentage` (use separate custom-audience ad sets).

**Sources.**
- https://www.facebook.com/business/help/454681230514942
- https://www.facebook.com/business/help/153514848493595
- https://www.jonloomer.com/qvt/ad-set-spending-limits-change/
- https://www.jonloomer.com/advantage-campaign-budget-best-practices/
- https://ppc.land/meta-deprecates-legacy-campaign-apis-for-advantage-structure/
- https://www.socialmediatoday.com/news/meta-changes-ad-budgets-charges-for-campaigns/758359/
- https://theoptimizer.io/blog/meta-ads-ad-set-budget-sharing-what-it-is-when-to-use-it-and-when-to-turn-it-off
- https://leadenforce.com/blog/meta-ads-budgets-explained-daily-vs-lifetime-and-cbo-vs-abo
- https://www.adamigo.ai/blog/cbo-best-practices-meta-ads

---

## Meta Ads Attribution Windows & Settings

**What changed.** Attribution moved from account-level (2017) to **ad-set level** (2021), the default is now **7-day click + 1-day view**, and on **Jan 12, 2026** Meta permanently removed the 7-day-view and 28-day-view windows from the Ads Insights API. Pixel-only tracking is no longer sufficient; some conversions are now modeled.

**What the book says (now wrong).** The ~2017 book assumes the OLD regime: a default 28-day click / 1-day view (or 28-day view) window set at the AD-ACCOUNT level, fully deterministic Pixel tracking (browser cookies only), no view-window deprecation, no engaged-view/engage-through category, no incremental/causal model, and no modeled or aggregated conversions. None of that is current.

**What's true today.**
- **Default attribution setting (ad-set level):** For a conversion ad set (Website conversion location, "maximize number of conversions") the default is **7-day click + 1-day engaged-view/engage-through + 1-day view.** Set under the ad-set "Attribution setting" section. The 1-day view window is bundled into the default — NOT removed for ad-set optimization; only the longer view windows were removed.
- **Available windows (ad-set optimization, 2026):** 1-day click, 7-day click, plus 1-day view and 1-day engaged-view ("engage-through"). The 28-day-click option exists for reporting comparison; **7-day click is the standard/default for delivery optimization.**
- **Jan 2026 removal (the big change):** On **Jan 12, 2026** Meta permanently removed **7d_view and 28d_view** from the Ads Insights API (announced Oct 13, 2025, ~90 days notice). Applies across ALL API versions — no legacy escape. Requests for deprecated windows now return **EMPTY datasets, not errors (silent failures).** Retained API windows: 1-day click, 7-day click, 28-day click, 1-day view, 1-day engaged-view. Many advertisers saw conversions drop ~Jan 12, 2026 (industry reports of 30–40% of conversions previously from the 8–28 day view window now uncounted). New data-retention limits: unique-count & hourly breakdowns = 13 months, frequency breakdowns = 6 months, aggregate totals = 37 months; MMM breakdowns moved to async-only jobs.
- **Engage-through (renamed March 2026):** Old "engaged-view" was renamed/expanded to **"engage-through."** Engaged-view previously = watched a video ≥10s (or ≥5s in some setups) then converted within 1 day. Now engage-through covers video engaged-view PLUS non-link interactions (likes, shares, saves, comments, bookmarks). Video threshold halved to **5 seconds** (97% of length for sub-5s videos).
- **Compare Attribution Settings column (reporting):** In Ads Manager, Columns dropdown > Customize columns (or the "Compare Attribution Settings" tab) to view results across multiple windows side-by-side: 1-day/7-day/28-day click, 1-day view, 1-day engaged-view. **Reporting-only — does NOT change delivery optimization** (which stays locked to the ad-set's attribution setting). It exposes **"First conversion" vs "All conversions":** First conversion counts only the first qualifying event per person per window (more accurate, avoids inflation); All conversions aggregates every qualifying action (can inflate frequent events like purchases).
- **Incremental Attribution (launched April 2025):** Optional attribution MODEL (alternative to standard rules-based), chosen at the ad-set level. Optimizes delivery toward conversions a model predicts were CAUSED by the ad (holdout/Lift methodology — a matched control group never sees ads; incremental = lift above the holdout rate). Available for Conversions, Sales (purchase-optimized), and Catalog/Product Catalog Sales objectives; needs ~50+ conversions/week. View via Columns > Custom > Compare Attribution Settings > Advanced Options > check "Incremental Attribution" > Apply. Data available retroactively from **April 1, 2025.**
- **Modeled / aggregated conversions:** Aggregated Event Measurement (AEM) measures web/app events from iOS 14+ users (post-ATT): removes identifiers, adds differential privacy, aggregates across users. Where signal is incomplete (ATT opt-outs), Meta fills gaps with **MODELED** (probabilistic) conversions shown directly in Ads Manager. AEM is built into Ads Manager natively; modeled conversions appear regardless of budget and are less precise than deterministic pixel/CAPI events. Best practice: pair the Pixel with CAPI to keep AEM accurate. *(Note: this finding references configuring/prioritizing 8 web events — see the ATT/AEM section above, which supersedes it: as of June 2025 the manual 8-event configuration tab was removed and AEM is now automated.)*

**Do this now.**
- [ ] Set/verify each conversion ad set's Attribution setting to 7-day click + 1-day view (the current default); attribution is configured at the AD-SET level, not the account level.
- [ ] Stop relying on 7-day-view or 28-day-view numbers — removed Jan 12, 2026. If any dashboard/API pull still requests them, it returns empty data silently; switch those calls to retained windows (1d/7d/28d click, 1d view, 1d engaged-view).
- [ ] Use Columns > Compare Attribution Settings to view 1d/7d/28d-click and 1d-view side by side, and toggle First conversion vs All conversions (use First conversion to avoid inflated counts on repeat purchases).
- [ ] Pair the Meta Pixel WITH CAPI so AEM and modeled conversions stay accurate for iOS 14+ traffic. (Do NOT manually rank 8 events — that tab was removed June 2025.)
- [ ] Test Incremental Attribution (Columns > Custom > Compare Attribution Settings > Advanced Options > Incremental Attribution) on high-volume conversion/sales ad sets (~50+ conversions/week) to gauge true ad-caused lift vs last-touch credit.
- [ ] Re-baseline reporting/ROAS expectations after Jan 2026: expect reported conversions to look lower than pre-2026 because view-through credit shrank; don't mistake the methodology change for a performance drop.

**Sources.**
- https://www.facebook.com/business/help/854500742637772
- https://ppc.land/meta-restricts-attribution-windows-and-data-retention-in-ads-insights-api/
- https://docs.supermetrics.com/docs/facebook-ads-new-historical-limitations-attribution-window-and-metric-removals-january-12-2026
- https://www.jonloomer.com/meta-ads-attribution-2026/
- https://www.jonloomer.com/compare-attribution-settings/
- https://madgicx.com/blog/metas-new-attribution-first-conversion-vs-all-conversions
- https://www.seerinteractive.com/insights/we-tested-metas-new-incremental-attribution-setting-on-1m-in-ad-spend.-heres-how-it-works
- https://support.appsflyer.com/hc/en-us/articles/19228737402129-Meta-Ads-Aggregate-Event-Measurement-AEM-for-iOS
- https://www.mediaperformance.co.uk/meta-engage-through-attribution/

---

## Meta Ad Relevance Diagnostics & Learning Phase

**What changed.** Meta retired the single 1–10 **"Relevance Score"** on **April 30, 2019** and replaced it with **three separate, per-ad diagnostics.** The formal Learning Phase and "Learning Limited" delivery statuses (~50 events/7 days) are now standard.

**What the book says (now wrong).** A ~2017 book references the single "Relevance Score" metric (1–10) as the way to judge ad quality and frames troubleshooting/reporting around optimizing that one number. That's wrong — Relevance Score was deprecated April 30, 2019. The book also predates the standardized Ad Relevance Diagnostics, the formal Learning Phase / Learning Limited statuses, Advantage Campaign Budget signal pooling, and the 10-results/3-day UI progress indicator. Older "Power Editor" / single-score workflows no longer match today's Ads Manager.

**What's true today.**
- **Ad Relevance Diagnostics** (live system, shown as breakdown columns via Columns > Customize Columns > "Performance"):
  1. **Quality Ranking** — perceived quality vs other ads competing for the same audience. Driven by feedback/quality signals: hides, reports, marked misleading/spam, plus engagement-bait, withholding-info, and sensationalized-language penalties.
  2. **Engagement Rate Ranking** — expected engagement (clicks, likes, comments, shares, saves, expands) vs ads competing for the same audience.
  3. **Conversion Rate Ranking** — expected conversion rate vs ads with the SAME optimization goal competing for the same audience.
- Each is rated **Above Average / Average / Below Average** (Below Average also bucketed as "Bottom 35% / 20% / 10% of ads"). A dash ("-") appears when the ad has **fewer than ~500 impressions** — read diagnostics only after ≥500 impressions and ideally after exiting the learning phase. Diagnostics are **diagnostic only — not used in the auction**, no direct delivery weight; they tell you WHICH lever to pull (Quality = creative/landing-page relevance & negative feedback; Engagement = creative hook; Conversion = offer/landing page/optimization-event match).
- **Learning phase:**
  - An ad set enters "Learning" whenever it starts or is significantly edited; Meta explores audience segments to find who converts.
  - **Exit threshold: ~50 optimization events within a 7-day window** since the last significant edit, to reach "Active" delivery. Count is at the AD SET level (with Advantage Campaign Budget / CBO, signal can pool at campaign level).
  - **Learning Limited:** if the ad set can't realistically reach ~50 events in 7 days, the delivery column shows "Learning Limited" — Meta stops optimizing and CPA becomes volatile. Causes: optimization event too rare, budget too low vs cost-per-event, audience too small/narrow, too many ad sets splitting signal, over-restrictive bid/cost cap. Fix structurally: higher-funnel/more-frequent optimization event, raise budget, broaden audience or use Advantage+/broad targeting, consolidate ad sets, or move budget to campaign level (Advantage Campaign Budget).
- **Edits that reset learning ("significant edits"):** changing the optimization event/goal; changing targeting/audience; changing creative/ad (including adding/swapping ads); changing bid strategy or bid/cost-cap amount; a significant budget change; pausing 7+ days (restarts on resume). Minor edits (small budget tweaks, name changes, schedule end-date changes) generally do NOT reset. Each reset re-enters the ~50-event/7-day clock.
- **2024–2026 nuance:** In many accounts Meta's UI progress bar now shows a shortened target of **"10 results" over up to 3 days** rather than the classic "50 over 7 days" (roughly half the old signal volume). Meta hasn't formally rewritten the 50/7 help-center guidance, so both circulate; **50/week remains the safe planning rule of thumb**, but check the in-product progress indicator for the live target.

**Do this now.**
- [ ] In Ads Manager, customize columns to add Quality Ranking, Engagement Rate Ranking, and Conversion Rate Ranking; do NOT look for the old "Relevance Score" — it no longer exists.
- [ ] Only read diagnostics after an ad has ≥500 impressions and has exited learning; ignore the dash ("-") before then.
- [ ] Use diagnostics to target fixes: Below-Average Quality → reduce negative feedback / improve creative & landing-page match; Below-Average Engagement → stronger hook/creative; Below-Average Conversion → fix offer, landing page, or switch optimization event.
- [ ] Aim for ~50 optimization events per ad set per week to exit learning; if events are rarer, expect Learning Limited.
- [ ] If an ad set shows "Learning Limited," fix structurally: raise budget, broaden/Advantage+ the audience, choose a more frequent optimization event, consolidate ad sets, or move to Advantage Campaign Budget — don't just wait.
- [ ] Avoid significant edits (optimization event, audience, creative, bid strategy, large budget changes, 7+ day pauses) while learning, since each resets the ~50-event/7-day clock; batch changes and let ad sets stabilize.
- [ ] Check the in-product learning progress bar for the live target — some accounts now show 10 results / 3 days instead of 50 / 7 days.

**Sources.**
- https://www.facebook.com/business/help/403110480493160
- https://www.facebook.com/business/help/303639570334185
- https://www.facebook.com/business/help/112167992830700
- https://www.jonloomer.com/qvt/is-the-learning-phase-changing/
- https://www.adstellar.ai/blog/meta-ads-performance-metrics-explained
- https://adriselab.com/learn/ad-relevance-diagnostics
- https://campaignpros.io/learning-center/facebook-learning-phase
- https://www.usewonderful.com/blog/meta-ads-learning-phase-50-conversions-per-week-help-center

---

## Current Meta Ad Creative Specs: Vertical 9:16, 4:5 Feed, Placement Inventory

**What changed.** Meta's creative system is now **mobile-vertical-first** and largely automated via Advantage+ Creative. The official spec source is the Meta Ads Guide (facebook.com/business/ads-guide), which lists specs per format (Image, Video, Carousel, Collection) and per placement.

**What the book says (now wrong).** The ~2017 book treats the link-ad image of **1200×628** (and older 1200×444) as the canonical ad image, and assumes square (1:1, 1200×1200) and landscape 16:9 are the primary shapes, with the desktop/right-column News Feed as the center of gravity. It predates Stories ads (2017), Reels (2020+), the 4:5 and 9:16 recommendations, the placement-inventory model (Marketplace/Search/Explore), automatic placements, and Advantage+ Creative's AI-generated variations. The old "20% text rule" overlay grid it may reference was retired (text density now only affects delivery, no hard rejection). Its troubleshooting around image rejection for text overlay and fixed single-size creative is outdated.

**What's true today.**
- **Recommended aspect ratios by placement:**
  - **Facebook Feed & Instagram Feed:** **4:5** recommended for images and video (Meta cites ~1% higher CTR for 4:5 vs 1:1 images, ~7% higher CTR for 9:16 video). Also supported: 1:1, 1.91:1, 16:9.
  - **Stories (IG/FB/Messenger), Reels (IG/FB), WhatsApp Status:** **9:16** full-screen vertical, 1080×1920 min, 1440×2560 high-res.
  - **Facebook Marketplace:** 1:1 recommended (16:9, 9:16 supported).
  - **Facebook Right Column:** 1.91:1 (1200×628) or 1:1.
  - **Search results (FB/IG):** ~1:1 to 4:5 image, 9:16 video.
  - **Carousel:** 1:1 (1080×1080) per card, consistent across cards.
  - **In-stream / Audience Network:** 9:16 / 4:5 / 1:1 depending on surface.
- **Dimensions / min resolution:** 1:1 → 1080×1080 min (1440×1440 ideal); 4:5 → 1080×1350 (1440×1800); 9:16 → 1080×1920 (1440×2560); 1.91:1 → 1200×628.
- **Images:** JPG/PNG, max 30MB, min 600×600 (1080×1080+ recommended).
- **Video:** MP4, MOV, GIF; H.264 codec, square pixels, fixed frame rate, progressive scan; AAC stereo 128kbps+; max 4GB. Length: Feed up to ~241 min (15–60s performs best); Stories ~15s per card; Reels up to ~30s; 1s minimum. Captions and sound recommended.
- **Safe zone (Reels/Stories, unified early 2026):** keep text/logos/CTAs out of top ~14%, bottom ~20–35%, and ~6% each side; central safe area ~1080×1440 on a 1440×2560 canvas.
- **Text limits:** primary text ~125 chars before truncation; headline ~40 chars; description ~25–30 chars.
- **Advantage+ Creative:** Replaced manual per-placement asset upload as the default. Upload one/few source assets and Meta auto-generates variations: aspect-ratio adjustments/cropping per placement, image-to-video/animation, 3D motion/depth, background generation/expansion (generative fill to 9:16), text/music/filter enhancements, dynamic combinations per user/placement. Legacy "Placement Asset Customization" (manually swapping a file per placement) still exists but is no longer the default.
- **Recent changes:** Instagram profile grid moved to **3:4** previews in 2025 (Reels still uploaded 9:16). Stories and Reels safe zones unified (early 2026). Instagram **Explore feed placement removed/folded into Reels** (early 2026). Meta is steering advertisers away from square (1:1) toward 4:5 and 9:16.

**Do this now.**
- [ ] Design vertical-first: build the master asset at 9:16 1080×1920 (ideally 1440×2560) for Reels/Stories, plus a 4:5 1080×1350 version for Feeds. Treat 1:1 as legacy/secondary.
- [ ] Stop using 1200×628 / 1200×444 / square-only as the primary ad image; use 1.91:1 only for right-column and link previews.
- [ ] Respect the unified Reels/Stories safe zone: keep text, logos, CTAs out of top ~14%, bottom ~20–35%, side ~6%; keep key content in the central ~1080×1440 area.
- [ ] Turn on Advantage+ Creative and let Meta auto-generate per-placement variations (aspect-ratio cropping, background expansion to 9:16, animation, music) instead of manually uploading one fixed size.
- [ ] Keep video to 15–60s (Reels ≤30s), use MP4/MOV H.264 + AAC, under 4GB, and add captions plus sound (most viewing is sound-on-mobile).
- [ ] Use Advantage+ Placements (automatic placements) so the ad runs across Feeds, Reels, Stories, Marketplace, Search, and Audience Network, then supply the right aspect ratios so each surface gets native creative.
- [ ] Ignore the retired 20% text rule as a hard blocker, but still minimize on-image text for better delivery.
- [ ] Verify exact current numbers per objective in the Meta Ads Guide (facebook.com/business/ads-guide) before each campaign — specs vary by objective/placement and change frequently.

**Sources.**
- https://www.facebook.com/business/ads-guide/update
- https://www.facebook.com/business/ads-guide/update/video/facebook-facebook-reels
- https://www.facebook.com/business/help/2222978001316177
- https://www.facebook.com/business/ads/facebook-instagram-reels-ads
- https://www.facebook.com/business/news/reels-ads-updates-performance-features-automated-creative-suitability-solutions
- https://adsuploader.com/blog/meta-ads-aspect-ratios
- https://adsuploader.com/blog/meta-ads-size
- https://www.jonloomer.com/recommended-aspect-ratios-by-placement-for-meta-ad-creative/
- https://billo.app/blog/meta-ads-safe-zones/
- https://www.bestever.ai/post/meta-video-ad-specs

---

## Old objective → new ODAX outcome

| Legacy objective (2017, ~11) | Funnel column (old) | New ODAX outcome (6) | Where the old setting lives now |
|---|---|---|---|
| Brand Awareness | Awareness | **Awareness** | Optimize for Ad recall lift / Reach |
| Reach | Awareness | **Awareness** | Optimize for Reach / Impressions |
| Traffic | Consideration | **Traffic** | Destination + Landing page views (recommended) |
| Post/Page Engagement | Consideration | **Engagement** | Conversion location = On your ad / Page |
| Page Likes | Consideration | **Engagement** | Folded into Engagement (no standalone objective) |
| Video Views | Consideration | **Engagement** | Conversion location = On your ad (ThruPlay) |
| Messages | Consideration | **Engagement** | Conversion location = Messaging apps |
| App Installs | Consideration | **App promotion** | Advantage+ app campaigns (AAA) |
| Lead Generation | Consideration | **Leads** | Conversion location = Instant forms / Website / Calls / Messenger / App |
| Conversions | Conversion | **Sales** | Conversion location = Website/App + performance goal (Purchase, etc.) |
| Catalog Sales | Conversion | **Sales** | Sales campaign + attached product catalog |
| Store Traffic / Store Visits | Conversion | **Sales** (retired) | Effectively retired; folded into Sales/awareness use cases |

---

## Quick modern setup order

1. **Verify your domain.** Business Settings > Brand Safety > Domains. Verify the primary domain (eTLD+1) with ONE method — DNS TXT (most durable), HTML file upload, or meta-tag. Leave the record in place.
2. **Confirm AEM is automated — don't rank 8 events.** The manual 8-event Event Configuration tab was removed June 2025; Meta aggregates eligible events automatically. Your lever is now signal quality (EMQ), not event selection.
3. **Set up Pixel + Conversions API (Dataset).** Find your Dataset ID (= old Pixel ID) in Events Manager. Run BOTH the browser Pixel and CAPI for the same events. Deduplicate with a shared, unique `event_id` and matching `event_name`/value/currency (~48h window). Send hashed email/phone + fbp/fbc + IP + user agent. Target EMQ above 7.0; verify in Test Events + Diagnostics. Pick a setup path: partner integration (Shopify/WooCommerce/GTM/Tealium/Zapier), CAPI Gateway (~10–15 min on AWS), or direct Graph API.
4. **Set the attribution setting (ad-set level).** Use the default 7-day click + 1-day view. Don't request or benchmark against 7d/28d-view windows (removed Jan 12, 2026 — they return empty data silently). Re-baseline reporting vs pre-2026.
5. **Decide Advantage+ vs manual.**
   - Pick the ODAX outcome (Awareness / Traffic / Engagement / Leads / App promotion / **Sales**), set conversion location + performance goal.
   - Advantage+ broad when you have volume (~50+ weekly conversions, ~$50+/day, a few hundred+ pixel events): Advantage+ Sales + Advantage+ Audience (interests as soft suggestions; hard controls only for location/age/language/exclusions) + Advantage+ Placements + reviewed Advantage+ Creative (turn OFF Text improvements, Music, Site links for sensitive ads).
   - Manual/original audiences for thin/cold pixels, regulated targeting, or clean A/B testing — and TEST in ABO (equal spend), SCALE in CBO (Advantage campaign budget, ~+20% every 2–3 days, minimum ad-set spend limits to exit learning).
   - Remember: full manual setup is unavailable for Sales objectives; legacy ASC/AAC API creation blocked (v24.0 Oct 2025, breaking v25.0 Q1 2026).
6. **Build creative vertical-first.** 9:16 1080×1920 master for Reels/Stories + 4:5 1080×1350 for Feed; respect the unified safe zone; let Advantage+ Creative generate per-placement variants. Ignore the retired 20% text rule.
7. **Monitor with the current diagnostics.** Add Quality / Engagement Rate / Conversion Rate Ranking columns (no "Relevance Score"); read only after ≥500 impressions. Watch the learning phase (~50 events/7 days, or the in-product 10/3-day indicator); fix "Learning Limited" structurally and avoid significant edits while learning.
