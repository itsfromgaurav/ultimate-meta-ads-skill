# audiences_targeting

> How to define, build, and scale Meta (Facebook/Instagram) ad audiences — warm vs. cold, custom audiences, lookalikes, interest research, and geo/demographic targeting — drawn from *Ultimate Guide to Facebook Advertising (3rd ed.)*.

## Core frameworks

### Warm vs. Cold Audiences (the foundational mental model)
Divide ALL targeting into two buckets:
- **Warm audiences** = people who have already had contact with your business: fans, website visitors, ad/page engagers, video viewers, your CRM lists (Infusionsoft, aWeber, Salesforce), pixel hits. Unique to your business, built from your own data. Principle: "it's cheaper to keep an existing customer than attract a new one." Secondary role: they are seed material for finding cold audiences via lookalikes.
- **Cold audiences** = people unfamiliar with you — the vast majority of Facebook. Vital for scaling (no growth without new customers), but never show your message to *just anyone*; get it in front of people most likely to be interested.
- You must target **BOTH**. There's a **synergy/feedback loop**: you need warm audiences to get better at targeting cold (lookalike source), and you need cold audiences to grow your warm audiences. This is why you should start collecting your own Facebook data ASAP. (Ch. 24)

**Two sources of warm audiences:** (1) Fans — automatically stored as a targetable audience, nothing extra needed; (2) Custom Audiences — four types by source: Contact Lists (leads/customers), Engagement on Facebook, Website Visitors, Mobile App Engagement. Up to **500 custom audiences per ad account**. (Ch. 24)

**Two ways to find cold audiences:** (1) Leverage Facebook's own user data — location, demographics, interests, behaviors, offline spending (interest research). (2) *Most powerful* — combine your data with Facebook's to create **lookalikes**. (Ch. 24)

### UPSYD audience awareness / intent ladder
Match message to audience based on level of **awareness, intent, and trust**. Progression mirrors the Facebook Flight Plan: Unaware of the problem → Problem Aware (intent to solve) → Solution Aware → intent to buy your specific product. The book centers on "five critical audience awareness levels and stages of intent" that drive ad-building frameworks for long-running, scalable campaigns. Moving targeting *up* the UPSYD ladder (e.g., from broad "guns" to "owns specific gun brands") often performs better while still staying large enough. (Ch. 2, Ch. 13, Ch. 23)

### BCOP — Audience Research Process (Brainstorm, Confirm, Organize, Prioritize)
For **ecommerce, digital, and information products** (NOT local businesses — they use geo targeting). End goal: identify a handful of starting interests with the highest probability of success, then use that success data to choose what to target next. Start with ~**20 interests** for larger budgets, ~**5** for small budgets. (Ch. 23)

**Step 1 — Brainstorm.** Prerequisites first: (a) know your avatar, (b) have a great hook and offer, (c) know which UPSYD segment you're targeting. Use the Interest Research Template spreadsheet. No right/wrong answers — capture as many ideas as possible. Use the **Six Brainstorming Triggers** (below) and analyze your warm-audience assets in Audience Insights (Page Likes).

**Step 2 — Confirm.** Verify any interest (especially ones found in Audience Insights) is an *actual targetable interest* in Power Editor — some show in Audience Insights but won't appear in Power Editor. Record each interest's potential reach. (Can skip if you used the Power Editor Suggestion Tool and already recorded reaches.)

**Step 3 — Organize & Combine.** Sort interests into categories/sub-categories by theme; order largest reach → smallest. Sub-categorizing lets you combine small-reach interests to hit the reach requirement. Any interest with reach **> 3 million** goes in the "Large Audiences" column → use the **Narrow** feature in Power Editor to build combinations landing in the **400K–2M** sweet spot → record in "Combined Interests."

**Step 4 — Prioritize by Avatar Match.** Pick best matches using two questions: (1) Does this interest sound like my avatar, *including where they are on UPSYD*? (2) Does a **LARGE PERCENTAGE** of this interest sound like my avatar? Prioritize interests that pass both.

### Five-Tier Scaling System — Tier 2: Audience Scaling
Get ads in front of more people similar to *winning* audiences by mining Facebook's data for related interests/behaviors (not only lookalikes). E.g., if "Frank Kern" works, "Ryan Deiss" likely works too. Notes: (a) if highly relevant audiences miss the 400K–2M reach requirement, group several similar ones; (b) compare what winning ad sets' targeting has in common vs. losers and reuse the positive attributes. (Ch. — Five-Tier Scaling System)

Process using **Audience Insights**: 1) Set calendar to last 7 days. 2) Sort ad sets by CPA smallest→largest. 3) Screen for ad sets with significant conversions + lowest CPA. 4) Record their targeting. 5) Insert interest into Audience Insights. 6) Choose "Page Likes." 7) Record new relevant interests. 8) Confirm in Power Editor + record reach.

Process using **Power Editor Suggestion Tool** (steps 1–4 same): 5) In detailed targeting, insert your interest. 6) Click "Suggestion." 7) Record relevant interests. (Advantage: only lists *targetable* interests.) Recommendation: use both — Suggestion Tool first, then Audience Insights.

After identifying **5–20** new relevant, appropriately-sized interests: 8) Highlight ad sets to scale and **Duplicate**. 9) Insert new interests into duplicates (e.g., "Robert Kiyosaki" → 3 duplicates with Tony Robbins, Brendan Burchard, Dave Ramsey). Housekeeping: rename ad sets to reflect the new interest, verify reach stays 400K–2M, and insert the **Post ID** to keep social proof.

## Tactics & best practices

**Lookalikes (the highest-leverage cold-targeting tactic)**
- Ask Facebook to find the people most like your customers — Facebook's algorithm analyzes your source (fans or a custom audience) and matches by demographics, location, interests, behaviors. Larger + more ideal-customer-like source = better lookalike. (Ch. 24)
- If you lack 1,000 customers, step **up the funnel** and use leads as the source (e.g., 200 customers but 4,000 leads → leads may be the better source). Trade-off: quantity of data vs. quality. Test to see what wins. (Ch. 24)
- **Customer Lifetime Value lookalikes:** upload LTV as an extra data field so Facebook builds lookalikes off your *highest-value* customers, not just any customer. (Ch. 24)
- **Video view audiences are among the best lookalike seeds** — they build large, cheap data pools fast, giving Facebook lots of data. (Ch. 13, Ch. 23)
- Large-metro local option: build a **10% lookalike** from your best custom audience, then overlay geo + demographic targeting (needs a large enough population). (Ch. 23)

**Custom audiences — building & using**
- Upload a customer phone/email list → Facebook recognizes **~half (~50%)**. (Opportunity ch.) Always have **permission** to collect the data — scraping violates Facebook Policy. (Ch. 24)
- **More data fields = better match rate.** Submit first name, last name, email, phone, city, zip — not email alone. (Ch. 24)
- **Engagement custom audiences are dynamic:** people are added as they engage and dropped once their engagement passes the time window. (Ch. 24)
- **Video view custom audiences** ("quality custom audiences" / "invisible lists"): segment by % watched; often "10x better and 2–3x cheaper" than a website click; gains compound as the algorithm learns who watches. (Ch. 13, Video Ad Formula ch.)
- **Abandoned-cart audience:** Website Traffic → Custom Combination → switch dropdown from URL to **Event** → include `AddToCart`, exclude `Purchase`. (Ch. 25)
- **Combine multiple custom audiences in one ad set** to retarget your entire warm audience with a single ad (saved audiences can't be combined). (A.P.B. ch.)

**Retargeting hot audiences**
- A **hot audience** = people who started but didn't complete the buying process (often just distracted — online attention span ~5 seconds). Without a system to recover them you leave easy money on the table. (Ch. 15)
- Repeated retargeting exposure exploits the **salience bias**: seeing the same ad over and over makes even a small brand feel like "a really big deal." (Ch. 20)

**Geographic / local targeting (local businesses are primarily geo, rarely interest-based)** (Ch. 23, A.P.B. ch.)
- Two methods: **type a city** (radius 10–50 mi) or **drop a pin** (radius 1–50 mi, finer minimum control).
- Geo levels: country, state/province, city, congressional district, zip/postcode, plus worldwide/regions/free-trade-areas/iTunes-store-countries/emerging markets.
- **Four location refinement modes:** (1) *Everyone in this location* (default — currently in area); (2) *People who live in this location*; (3) *People recently in this location* (phone location — powerful for local, hit them near the store); (4) *People traveling in this location* (>125 miles from home — great for travel/tourism).
- Increase your radius only by building **authority/expert status** (post useful content; fund a branding campaign) and **social proof** (friends who liked the ad/page shown on the ad) so people will travel to you.
- **Hyperlocal proximity:** reach visitors traveling within ~10 miles with a real-time offer (e.g., "Come in for 30% off!"). (Opportunity ch.)

**Detailed targeting logic**
- Stacking criteria in one "include" box = **OR** targeting (broad — meets *at least one*). Use **audience narrowing** for **AND** targeting (must meet *all*, e.g., homeowner AND likes cooking AND parent). (A.P.B. ch.)
- **Don't pile all suggested interests into one ad set** — separate interests into separate ad sets so you can compare response per interest. (Ch. 11)
- Target **large audiences** to leverage the algorithm (4–5M, best case 40–50M) — but only works above a conversion-volume threshold: **20–30 conversions/week per ad set** minimum (ideally 10–20+/day), using the Website Conversions objective. For smaller-population countries (e.g., Australia), use 100K–500K instead. (Five-Tier Scaling ch.)

**Connection & exclusion targeting**
- **Connection types** (with custom audiences / new audiences only — NOT saved audiences): fans of your page, **friends of fans**, app users, friends of app users, event responders. (A.P.B. ch.)
- **Friends of Fans** grows exponentially: 10K fans → ~200K friends-of-fans audience; growing to 12K fans can lift it to ~230K. Adds instant credibility (appears friend-recommended). (Ch. 11)
- **Exclusions protect ad spend:** exclude existing leads/customers on conversion campaigns; exclude your **fans** to reach a truly cold audience; can also exclude geos, interests, connections. (A.P.B. ch.)

**Reusable / saved audiences**
- Pre-build a Saved Audience of **influencers** (magazines, radio, papers, TV, bloggers, conference attendees) so it's one click when boosting. (Boosted Posts ch.)
- **Media Inception Audience:** target people who *work at* Forbes / CNN / WSJ (not their readers) so they may write about or share your content; build as a reusable Saved Audience (e.g., "mega media inception"). (More Boosted Posts ch.)
- **Match the audience to each post** — the right audience differs per post (e.g., a "hustle"-themed article → Gary Vaynerchuk fans). Most tuning work is trying audience combinations, not making new posts. (More Boosted Posts ch.)

**Three audience choices when building an ad set** (A.P.B. ch.): (1) a **Saved** audience (interest/demo built earlier); (2) a **Custom** audience (all custom, lookalikes, or just custom); (3) create a **New** audience inline.

**Strategy notes**
- End goal: build large **warm** audiences and let Facebook find your best **cold** audiences via lookalikes; best starting point for feeding data is **interest & behavior targeting**. (Ch. 23)
- In the takeoff (0–100) phase, **don't focus on building warm audiences yet** — keep it simple with your two starter campaigns (Like ad + Website Conversions link-post ad). (Flight Plan ch.)
- Run **different ad styles (long-copy AND short-copy) to the SAME audiences** — each audience holds people at different awareness/intent levels, so varied messaging captures more of them. (Flight Plan ch.)
- Every audience contains multiple **buyer personas** — Impulsive, Analytical, Emotional/humanistic, Competitive (per Kolbe "Fact Finder" scale) — so create varied messaging to resonate with each. (Flight Plan ch.)
- **Identify your avatar AND your IDEAL avatar** (most valuable customer = one you'll pay more to acquire; spends more, refers more). Watch for sub-avatars; the more specific the hook to the sub-avatar, the better (e.g., "Learn Eddie Van Halen's Top 10 Guitar Licks" vs. generic "how to play guitar"). (Ch. 16)
- **Content-to-offer retargeting:** segment visitors by which article/topic they consumed, then retarget each segment with the topically matched offer (tennis content → tennis racquet; vertical-leap content → basketball program). (Pixel ch.)
- **Act on breakdown data:** e.g., ages 25–34 gave cheapest leads while 55–64 gave most revenue → add new audiences + demographic targeting to maximize budget. (Ch. 29)

## Checklists

### The Six Brainstorming Triggers (Ch. 23)
- [ ] Competitors
- [ ] Leaders and gurus in your market
- [ ] Tools / Equipment / Services
- [ ] Publications (blogs, TV shows, books, magazines, podcasts)
- [ ] Organizations your avatar might belong to
- [ ] Other Behavior (ideas that fit no category)

### Website Custom Audience — Rule Selection options (Ch. 24)
Standard Rules:
- [ ] All Website Visitors (everyone in last ≤180 days)
- [ ] URL Contains / URL Doesn't Contain / URL Equals
- [ ] Frequency (visited a particular number of times)
- [ ] Device (visited using a specific device)
- [ ] Visitors by Time Spent (those who spent the most time)

Pixel Event Rules:
- [ ] URL (specific URL) · Frequency · Device

### Lookalike Audience rules & limits (Ch. 24)
- [ ] Country-specific — must name the country/countries
- [ ] Source must contain ≥100 people from the SAME country (those 100 needn't be from the target country — a U.S. source can build a U.K. lookalike)
- [ ] Size = 1–10% of population (1% = most similar/smallest, 10% = broadest)
- [ ] Up to 500 lookalikes per single source audience
- [ ] Source members are excluded from the lookalike UNLESS the source is a pixel

### Contact-list custom audience — uploadable fields (Ch. 24)
- [ ] email, phone, first name, last name, city, state/province, country
- [ ] date of birth, year of birth, age, zip/postal code, gender
- [ ] mobile advertiser ID, Facebook ID

### Build a Lookalike Audience (Ch. 24)
- [ ] Ads Manager → Audiences → Create Audience → Lookalike Audience
- [ ] Choose Source → Select Country/Countries → Select Size (1–10%) → Create
- [ ] Allow 6–24 hrs to generate; auto-updates while source updates AND lookalike is in use; recreate if size/updates look wrong

## Benchmarks & numbers

| Metric | Value / threshold | Context |
|---|---|---|
| Customer-list match rate | ~50% | Share of an uploaded phone/email list Facebook recognizes |
| Lookalike source — Facebook recommended | 1,000–50,000 people | Ideal source audience size |
| Lookalike works from (observed) | ~1,000 data points | Agency has seen good results at this low end |
| Lookalike "fully dialed in" | 60,000–100,000 data points | Per Facebook reps (≠ 100K customers — video views build this fast) |
| Lookalike source minimum | ≥100 same-country people | Hard minimum to create one |
| Lookalike size selection | 1–10% of population | 1% most similar/smallest, 10% broadest |
| Lookalikes per source | up to 500 | Limit |
| Custom audiences per ad account | up to 500 | Limit |
| Potential reach — incl. U.S. | 400,000–2,000,000 | Recommended "sweet spot" |
| Potential reach — smaller-pop countries | 100,000–500,000 | When U.S. not included |
| Power Editor Suggestion Tool — record threshold | reach > 100,000 | Record suggested interests above this |
| "Large audience" trigger for Narrow feature | > 3,000,000 | Combine down into 400K–2M range |
| Large-audience algorithm play | 4–5M (best case 40–50M) | Needs ≥20–30 conversions/wk per ad set |
| Lift radius — "traveling in this location" | >125 miles from home | Definition of a traveler |
| Geo radius — city method | 10–50 miles | Radius range |
| Geo radius — drop-a-pin method | 1–50 miles | Finer minimum control |
| Audience Insights — demographics threshold | ≥1,000 | Min audience size to see demographics |
| Audience Insights — Page Likes threshold | ≥100,000 | Min size to see Page Likes |
| Lookback — video / canvas / page engagement | up to 365 days | Engagement window |
| Lookback — lead form engagement | up to 90 days | Shorter than other engagement types |
| Lookback — website custom audience | up to 180 days | Pixel-based |
| Lookback — app engagement | up to 180 days | App activity |
| Website custom audience rules | up to 5 (1 inclusive + up to 4 more) | Inclusive/exclusive rules per audience |
| App events | 14 pre-defined (or custom) | Trackable app events via Facebook SDK |
| Like campaign starter reach | ~1.5 million | With one or two related interests |
| BCOP starting interests | ~20 (large budget) / ~5 (small) | Number of interests to begin with |
| Lookalike processing time | 6–24 hours | Time to generate |
| Data Guru / Request Help turnaround | 24–48 hours | Facebook strategist recommendations |

## Copy/templates

Content-to-offer retargeting example articles (segment visitors by topic consumed):
```
Article 1 (tennis):    "Three Quick Tips to Easily Add 10 MPH to Your Tennis Serve"
Article 2 (basketball): "Try this In-Home Exercise That Can Quickly Add Up to Two
                         Inches or More to Your Vertical Leap, in Just Five Minutes a Day"
→ Tennis-article visitors see the "Special Edition Tennis Racquet" offer;
  vertical-leap visitors see the "Vertical Leap Explosion" basketball program.
```

Sub-avatar hook specificity (guitar niche):
```
Too broad:  "How to play guitar"
Better:     "Learn to Play Eddie Van Halen's Top 10 Guitar Licks"  (hard-rock sub-avatar)
```

Abandoned-cart custom audience (pixel events):
```
Audiences → Create Custom Audience → Website Traffic → Custom Combination
  → change dropdown from "URL" to "Event"
  → INCLUDE event: AddToCart
  → EXCLUDE event: Purchase
```

Like Campaign cold-audience ad set targeting (Ch. 11):
```
1. Choose the Facebook page to promote.
2. Target COLD audiences. Geo start: U.S., Canada, U.K., Australia, New Zealand.
   To reach English speakers elsewhere (e.g., Europe), set Languages = "English (All)".
3. Set Age & Gender (narrow if niche — e.g., women's sportswear, baldness cure).
4. Detailed Targeting: pick just ONE or TWO related interests → ~1.5M reach.
   (Separate interests into separate ad sets to compare response.)
5. Connections: "Exclude people who like your page."
```

## Pitfalls to avoid

- **Don't chase cheap/tricked likes.** Bait such as "Click Like if you love being in shape" or "Click Like if you Love Making Money" loads you with poor-quality leads. Warm-audience ROI only works with QUALITY fans who genuinely want to hear from you. (Ch. 11)
- **Never scrape data.** Always have permission to collect info before uploading — scraping violates Facebook Policy. (Ch. 24)
- **Saved audiences are limited:** only ONE usable at a time; edits must be made to the *original* saved audience (not inside the ad set); can't be combined (build a new saved audience to combine); connections must be set when the saved audience is *created*. (A.P.B. ch.)
- **OR-by-accident:** stacking interests in one "include" box is OR targeting — you'll reach people matching only one criterion. Use audience narrowing for AND. (A.P.B. ch.)
- **Don't pile all suggested interests into one ad set** — you lose the ability to compare per-interest performance. (Ch. 11)
- **Audience Insights ≠ targetable:** an interest shown in Audience Insights may not exist in Power Editor — always confirm in Power Editor (BCOP Step 2). (Ch. 23)
- **Large-audience strategy fails below the conversion floor** — needs ≥20–30 conversions/week per ad set; in small-population countries fall back to 100K–500K. (Five-Tier Scaling ch.)
- **Wrong audience for good content:** a near-"unicorn" post can flop because it was boosted to the wrong audience; the right audience differs per post. (More Boosted Posts ch.)
