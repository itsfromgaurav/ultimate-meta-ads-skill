# Pixel & Tracking Setup Checklist

> Install, configure, and verify the Facebook (Meta) Pixel for conversion tracking, audience building, and AI delivery optimization. Source: *Ultimate Guide to Facebook Advertising (3rd ed.)*, Ch. 25 / "Power of the Pixel".

---

## 1. Locate your Base Pixel Code in Business Manager (Ch. 25)

- [ ] Go to Business Manager → main menu (top-left) → **Pixels** under the **Assets** submenu
- [ ] **New ad account:** follow the setup wizard prompts; the Base Pixel Code is provided at the end (do this ASAP after creating the account)
- [ ] **Existing ad account:** on the Pixels screen click **Actions → View Pixel Code**, then read it under **"1 Install Pixel Base Code"**

## 2. Install & place the pixel (Ch. 25 / Power of the Pixel)

- [ ] Install the pixel on **every single page** of the site (home, blog/article, sales, add-to-cart, checkout — 100% of pages)
- [ ] Fire the **Base Pixel Code on ALL pages, on page load**
- [ ] Place the Base Pixel Code in the `<head>...</head>` so it runs before any event code
- [ ] Ensure **event code comes AFTER the Base Pixel Code** in top-to-bottom source order (so `fbq` is loaded first)
- [ ] Replace `{{YourFBPIXELID}}` with your actual numeric Pixel ID

> Pitfall: Don't put event code inside the Base Pixel block — unnecessary; event code can fire almost anywhere after the base code.
> Pitfall: Don't place event code before the Base Pixel Code — it won't fire properly.

## 3. Configure Standard Events — most common (Ch. 25)

- [ ] **Lead** — someone opts in to your email list / follow-up channel
- [ ] **Purchase** — fired when a purchase occurs (the only event with mandatory parameters)
- [ ] **Complete Registration** — webinar registrations, event registrations, etc.
- [ ] **Add To Cart** (`AddToCart`) — visitor adds a product to the cart
- [ ] **Initiate Checkout** (`InitiateCheckout`) — visitor reaches the checkout form before purchasing
- [ ] Fire each Standard Event with the **right contextual meaning** in the right circumstances (avoid confusing reporting)

## 4. Parameters — key rules (Ch. 25)

- [ ] Parameters are **mandatory only on the Purchase event** (`currency` and `value`); optional for all other events
- [ ] Parameters are completely open-ended — add and name as many as you want
- [ ] Use parameters in Business Manager to build granular Custom Audiences / Custom Conversions
- [ ] Only parameters that have already had site activity appear in the pre-populated dropdowns
- [ ] Consult Facebook's Advertising Help section for the full list of events and their commonly used / mandatory parameters

## 5. Leverage the Three Super Powers of the Pixel (Ch. 25)

- [ ] **Audience Building** — build advertising audiences from on-site behavior ("reach the right people")
- [ ] **Optimization** — at the ad set level, designate an **Optimization Event** (usually a Standard Event) so Facebook finds more people likely to convert
- [ ] **Tracking & Measurement** — align Standard Events with the columns/metrics in Ads Manager for reporting

## 6. Verify with the Facebook Pixel Helper (Troubleshooting)

- [ ] Install the Facebook Pixel Helper on Chrome
- [ ] Click each ad's URL and confirm the pixel fires on every page of the funnel
- [ ] Cross-reference the reported Pixel ID against your Ad Account Pixel ID in Ads Manager → All Tools → Pixels
- [ ] Confirm the IDs match on every page of the funnel

---

## Copy/templates

**Base Pixel Code** — replace `{{YourFBPIXELID}}` with your actual numeric Pixel ID:

```html
<!-- Facebook Pixel Code -->
<script>
!function(f,b,e,v,n,t,s){if(f.fbq)return;n=f.fbq=function(){n.callMethod?
n.callMethod.apply(n,arguments):n.queue.push(arguments)};if(!f._fbq)f._fbq=n;
n.push=n;n.loaded=!0;n.version='2.0';n.queue=[];t=b.createElement(e);t.async=!0;
t.src=v;s=b.getElementsByTagName(e)[0];s.parentNode.insertBefore(t,s)}(window,
document,'script','https://connect.facebook.net/en_US/fbevents.js');
fbq('init', '{{YourFBPIXELID}}'); // Insert your pixel ID here.
fbq('track', 'PageView');
</script>
<noscript><img height="1" width="1" style="display:none"
src="https://www.facebook.com/tr?id={{YourFBPIXELID}}&ev=PageView&noscript=1"
/></noscript>
<!-- DO NOT MODIFY -->
<!-- End Facebook Pixel Code -->
```

**Standard Event (Lead example):**

```html
<script>
fbq('track', 'Lead');
</script>
```

**Purchase event with parameters** (`value` and `currency` mandatory on Purchase):

```html
<script>
fbq('track', 'Purchase', {
value: 54.00,
currency: 'USD'
});
</script>
```

---

## Key numbers / thresholds

| Item | Value |
|---|---|
| Pages with pixel installed | Every page (100%), on page load |
| Mandatory Purchase parameters | 2 (`value`, `currency`) |
| Purchase example `value` / `currency` | 54.00 / USD |
| Custom conversions per ad account | up to 40 |
| Standard website events | 9 |
