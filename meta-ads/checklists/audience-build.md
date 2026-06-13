# Audience Build Checklist

> Define, build, research, and scale Meta (Facebook/Instagram) ad audiences — warm vs. cold, custom audiences, lookalikes, interest research (BCOP), and ad-set structure. Source: *Ultimate Guide to Facebook Advertising (3rd ed.)*, Ch. 23 / Ch. 24 / A.P.B.

---

## 1. The Four Ad Set Groups — sequenced rollout (Ch. 24)

Structure campaigns to fire "on all four cylinders." Roll out in order:

- [ ] Start with **Ad Set #4 — Interests & Behaviors (cold)** — recommended starting point: 5–20 interests
- [ ] As you build audiences, add **#1 — Your Fans (warm)**
- [ ] As you build audiences, add **#2 — Your Custom Audiences (warm)**
- [ ] As you see conversions from #1 and #2, add **#3 — 1% Lookalike Audiences (cold)**

## 2. BCOP — Audience Research Process (Ch. 23)

> For ecommerce, digital, and information products (NOT local businesses — they use geo targeting).
> Start with ~20 interests for larger budgets, ~5 for small budgets.

**Step 1 — Brainstorm.** Prerequisites first:
- [ ] Know your avatar
- [ ] Have a great hook and offer
- [ ] Know which UPSYD segment you're targeting
- [ ] Use the Interest Research Template spreadsheet; capture as many ideas as possible
- [ ] Apply the Six Brainstorming Triggers (below)
- [ ] Analyze warm-audience assets in Audience Insights (Page Likes)

**Step 2 — Confirm.**
- [ ] Verify each interest is an *actual targetable interest* in Power Editor (some show in Audience Insights but not Power Editor)
- [ ] Record each interest's potential reach

**Step 3 — Organize & Combine.**
- [ ] Sort interests into categories/sub-categories by theme; order largest reach → smallest
- [ ] Any interest with reach **> 3 million** → "Large Audiences" column
- [ ] Use the **Narrow** feature to combine into the **400K–2M** sweet spot → record in "Combined Interests"

**Step 4 — Prioritize by Avatar Match.** For each interest ask:
- [ ] Does this interest sound like my avatar, *including where they are on UPSYD*?
- [ ] Does a **LARGE PERCENTAGE** of this interest sound like my avatar?
- [ ] Prioritize interests that pass both

## 3. The Six Brainstorming Triggers (Ch. 23)

- [ ] Competitors
- [ ] Leaders and gurus in your market
- [ ] Tools / Equipment / Services
- [ ] Publications (blogs, TV shows, books, magazines, podcasts)
- [ ] Organizations your avatar might belong to
- [ ] Other Behavior (ideas that fit no category)

## 4. Build a Lookalike Audience (Ch. 24)

- [ ] Ads Manager → Audiences → Create Audience → Lookalike Audience
- [ ] Choose Source → Select Country/Countries → Select Size (1–10%) → Create
- [ ] Allow **6–24 hrs** to generate; auto-updates while source updates AND lookalike is in use; recreate if size/updates look wrong

**Lookalike rules & limits (Ch. 24):**
- [ ] Country-specific — must name the country/countries
- [ ] Source must contain ≥100 people from the SAME country
- [ ] Size = 1–10% of population (1% = most similar/smallest, 10% = broadest)
- [ ] Up to 500 lookalikes per single source audience
- [ ] Source members are excluded from the lookalike UNLESS the source is a pixel

## 5. Contact-list custom audience — uploadable fields (Ch. 24)

> More data fields = better match rate. Don't upload email alone. Facebook recognizes ~50% of an uploaded list.

- [ ] email, phone, first name, last name, city, state/province, country
- [ ] date of birth, year of birth, age, zip/postal code, gender
- [ ] mobile advertiser ID, Facebook ID
- [ ] Confirm you have **permission** to collect the data (scraping violates Policy)

## 6. Website Custom Audience — Rule Selection options (Ch. 24)

Standard Rules:
- [ ] All Website Visitors (everyone in last ≤180 days)
- [ ] URL Contains / URL Doesn't Contain / URL Equals
- [ ] Frequency (visited a particular number of times)
- [ ] Device (visited using a specific device)
- [ ] Visitors by Time Spent (those who spent the most time)

Pixel Event Rules:
- [ ] URL (specific URL) · Frequency · Device

## 7. Abandoned-cart custom audience (Ch. 25)

- [ ] Audiences → Create Custom Audience → Website Traffic → Custom Combination
- [ ] Change dropdown from "URL" to **Event**
- [ ] INCLUDE event: `AddToCart`
- [ ] EXCLUDE event: `Purchase`

## 8. Detailed targeting & exclusion logic (A.P.B.)

- [ ] Keep **one (or two related) interests per ad set** so you can compare per-interest performance
- [ ] Stacking interests in one "include" box = **OR** targeting (broad); use **audience narrowing** for **AND** targeting
- [ ] Don't pile all suggested interests into one ad set
- [ ] Exclude existing leads/customers on conversion campaigns
- [ ] Exclude your **fans** to reach a truly cold audience

---

## Key numbers / thresholds

| Metric | Value / threshold |
|---|---|
| Custom-list match rate | ~50% |
| Lookalike source — Facebook recommended | 1,000–50,000 people |
| Lookalike source minimum | ≥100 same-country people |
| Lookalike size | 1–10% of population |
| Lookalikes per source / Custom audiences per ad account | up to 500 each |
| Lookalike processing time | 6–24 hours |
| Potential reach sweet spot (incl. U.S.) | 400,000–2,000,000 |
| Potential reach (smaller-pop countries) | 100,000–500,000 |
| "Large audience" trigger for Narrow feature | > 3,000,000 |
| Large-audience algorithm play | 4–5M (best case 40–50M) |
| Min conversions for large audiences | 20–30/week per ad set (ideally 10–20+/day) |
| BCOP starting interests | ~20 (large budget) / ~5 (small budget) |
| Recommended interest range | 5–20 interests |
| Reach target per interest ad set | ~1.5 million |
| Lookback — video/canvas/page engagement | up to 365 days |
| Lookback — lead form engagement | up to 90 days |
| Lookback — website custom audience | up to 180 days |
| Lookback — app engagement | up to 180 days |
| Website custom audience rules | up to 5 (1 inclusive + up to 4 more) |
| Geo radius — city method | 10–50 miles |
| Geo radius — drop-a-pin method | 1–50 miles |
| "Traveling in this location" definition | >125 miles from home |
