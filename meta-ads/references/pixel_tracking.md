# pixel_tracking

> How to install, configure, and use the Facebook (Meta) Pixel for conversion tracking, audience building, and AI delivery optimization.

## Core frameworks

### Three Super Powers of the Facebook Pixel
The pixel is far more than a tracking tag. A common misconception is that it is ONLY for tracking and measuring. It serves three core jobs, and every pixel decision should be made in service of leveraging them (Ch. "Power of the Pixel"; Ch. 25):

1. **Audience Building** — "Reach the right people." Build advertising audiences from on-site behavior and make sure ads are shown to the right people.
2. **Optimization** — "Drive more sales." Unlock additional Facebook advertising tools and let the algorithm find more people likely to convert.
3. **Tracking & Measurement** — "Measure the results of your ads." Understand the actions people take on your website.

Facebook's official definition: the pixel is "an analytics tool that allows you to measure the effectiveness of your advertising by understanding the actions people take on your website." Guiding quote, Claude Hopkins (*Scientific Advertising*): "Never be guided in any way by ads that are untracked."

### Three Ways Standard Events Are Used
Standard Events feed all three pixel super powers (Ch. 25):

1. **Tracking & Measurement** — Standard Events align with the columns/metrics available in Ads Manager for reporting on results.
2. **Audience Construction** — In **Audiences**, create a new **Custom Audience** based on **Website Traffic**, choose **Custom Combination**, then change the dropdown from **URL** to **Event**, and specify which events include/exclude people. Example: people who fired AddToCart but did not Purchase.
3. **Optimization** — When setting up a website conversion campaign at the **ad set level**, designate an **Optimization Event** from the dropdown (usually a Standard Event). You are telling Facebook: "look for people who do this event, then find more people similar to them to prioritize my ad's delivery." Facebook's Machine Learning then determines who the similar people are and raises the odds your ad reaches them.

## Tactics & best practices

**Installation & placement**
- Install the pixel on **every single page** of your site — home page, blog/article pages, sales pages, add-to-cart pages, checkout pages, and everything in between. Track that activity to build custom audiences for retargeting/remarketing (later or simultaneously). Website visitor activity is the most common audience-building behavior. (Ch. "Power of the Pixel")
- Fire the **Base Pixel Code on ALL pages, on page load.** Place it in the `<head>...</head>` so it runs completely before any event code executes. (Ch. 25)
- **Event code must come AFTER the Base Pixel Code** in top-to-bottom page-source order, so `fbq` is loaded before the event fires. Typical pattern: Base Pixel in `<head>`, event code in `<body>`. Events can also fire on a button click or form submission. (Ch. 25)
- Event code does **not** need to live inside the Base Pixel block — it can fire almost anywhere on the page (after the base code). (Ch. 25)

**Events & conversions**
- Place the pixel on any page you want to measure results from. Trackable actions: number of leads, cost per lead, purchase data, shopping cart and checkout activity, visitor engagement, and visitor events (e.g., button clicks). After receiving pixel data, Facebook attributes each measurable action to the ad that triggered it. (Ch. "Power of the Pixel")
- **Off-objective conversions still track.** A conversion different from your chosen optimization event is still recorded in reporting — as long as you created a Standard Event or a Custom Conversion. (setup in Ch. 27)
- Fire each Standard Event with the **right contextual meaning** in the right circumstances to avoid confusing yourself or your team during reporting. (Ch. 25)
- **Parameters** add descriptors (a payload) to an event. They are open-ended — add as many as you want and name them whatever you like — and can be used in Business Manager to build highly granular Custom Audiences or Custom Conversions (e.g., AddToCart where `product_name` contains "Shoes"). Only parameters that have already had traffic on your site appear in the pre-populated dropdowns. (Ch. 25)

**Like campaigns**
- At the bottom of a Like ad, choose to track **"All conversions from my Facebook pixel."** Worth doing because someone might click Like and then opt in to a lead gen ad a week later — your Like campaign will get credit for that conversion. (Ch. 11)

**Verification**
- Use the **Facebook Pixel Helper** (Chrome extension) to confirm the pixel is present and correct on every URL in the funnel. (Troubleshooting)

## Checklists

**Most common Standard Events** (Ch. 25)
- [ ] **Lead** — someone opts in to your email list / follow-up channel
- [ ] **Purchase** — fired when a purchase occurs (the only event with mandatory parameters)
- [ ] **Complete Registration** — webinar registrations, event registrations, etc.
- [ ] **Add To Cart** (`AddToCart`) — visitor adds a product to the cart
- [ ] **Initiate Checkout** (`InitiateCheckout`) — visitor reaches the checkout form before purchasing

**Key rules about parameters** (Ch. 25)
- [ ] Parameters are **mandatory only on the Purchase event** (`currency` and `value`); optional for all other events
- [ ] Parameters are completely open-ended — add and name as many as you want
- [ ] Use parameters in Business Manager to build granular Custom Audiences / Custom Conversions
- [ ] Only parameters that have already had site activity appear in the pre-populated dropdowns
- [ ] Consult Facebook's Advertising Help section for the full list of events and their commonly used / mandatory parameters

**Locate your Base Pixel Code in Business Manager** (Ch. 25)
- [ ] Go to Business Manager → main menu (top-left) → **Pixels** under the **Assets** submenu
- [ ] **New ad account:** follow the setup wizard prompts; the Base Pixel Code is provided at the end (do this ASAP after creating the account)
- [ ] **Existing ad account:** on the Pixels screen click **Actions → View Pixel Code**, then read it under **"1 Install Pixel Base Code"**

**Pixel verification with the Pixel Helper** (Troubleshooting)
- [ ] Install the Facebook Pixel Helper on Chrome
- [ ] Click each ad's URL and confirm the pixel fires on every page of the funnel
- [ ] Cross-reference the reported Pixel ID against your Ad Account Pixel ID in Ads Manager → All Tools → Pixels
- [ ] Confirm the IDs match on every page of the funnel

## Copy/templates

**Base Pixel Code** — replace `{{YourFBPIXELID}}` with your actual numeric Pixel ID (Ch. 25):

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

**Standard Event (Lead example)** — swap `'Lead'` for any other Standard Event name (Ch. 25):

```html
<script>
fbq('track', 'Lead');
</script>
```

**Purchase event with parameters** — `value` and `currency` are mandatory on Purchase (Ch. 25):

```html
<script>
fbq('track', 'Purchase', {
value: 54.00,
currency: 'USD'
});
</script>
```

**Parameter payload (JavaScript object) syntax pattern** (Ch. 25):
1. Open bracket `{`
2. Parameter name followed by a colon — e.g. `value:`
3. Parameter value followed by a comma — e.g. `54.00,`
4. Repeat steps 2–3 for all parameters
5. Closed bracket `}`, then close the function call with `);`

## How the pixel works (reference concepts)

**The Base Pixel Code.** When people say "Facebook Pixel" they mean a JavaScript block placed on your site. The block is identical for all advertisers; the only unique part is the **Facebook Pixel ID** — a number unique to your ad account that tells Facebook which account the activity belongs to. This common block is the **Base Pixel / Base Pixel Code** and is the foundation of all data you send to Facebook. (Ch. 25)

**What the base code does, step by step** (Ch. 25):
1. Notifies Facebook's Ad Tracking servers that there's an active visitor and requests the functions needed to send data.
2. Facebook responds with a set of functions — most importantly **`fbq`**, used to send data in a language Facebook understands.
3. `fbq('init', '{{YourFBPIXELID}}');` initializes the pixel, associating all page activity with your Pixel ID (correct attribution to your ad account).
4. `fbq('track', 'PageView');` registers the first **event**. Data sent behind the scenes includes the current page URL, the visitor's unique Facebook User ID, a timestamp, and helper data. Afterward Facebook knows WHO is on the site, WHAT page they view, the Pixel ID, and the related ad account(s). Once `fbq` is available you can send additional events.

**Events & Standard Events.** An **Event** is an on-site action you want Facebook to know about (PageView is one), used to build audiences, track conversions, and help Facebook learn WHO takes desired actions so it can target similar people. The pixel works with a predefined set of common actions called **Standard Events** (full list in Facebook's Advertising Help section). (Ch. 25)

**Parameters.** A third section of the `fbq` call carrying a payload of descriptors that tell Facebook more about an event. The Purchase event is unique because Facebook wants to know how much the purchase was worth, so it requires `value` and `currency`. (Ch. 25)

## Benchmarks & numbers

| Metric | Value/threshold | Context |
|---|---|---|
| Purchase example `value` | 54.00 | Sample value parameter in the verbatim Purchase event code (Ch. 25) |
| Purchase example `currency` | USD | Sample currency parameter in the verbatim Purchase event code (Ch. 25) |
| Mandatory Purchase parameters | 2 (`value`, `currency`) | Only event type with required parameters (Ch. 25) |
| Pages with pixel installed | Every page (100%) | Base Pixel must fire on all pages, on page load (Ch. "Power of the Pixel"; Ch. 25) |

## Pitfalls to avoid

- **Flying blind without a configured pixel.** Without the pixel set for proper conversion tracking you won't know what's working. Facebook's algorithms only do the heavy lifting if the pixel is set up and configured properly. (Ch. "Power of the Pixel")
- **Assuming Facebook enforces event names.** Aside from Purchase, Facebook doesn't know or care when/how you fire events — the names carry no special meaning. Firing `AddToCart` on a "Contact Us" page won't be flagged, but it will confuse your reporting. Always fire events with correct context. (Ch. 25)
- **Putting event code inside the Base Pixel block.** A common misconception; it's unnecessary and often makes implementation harder. Event code can fire almost anywhere on the page — as long as it's after the base code. (Ch. 25)
- **Placing event code before the Base Pixel Code.** If an event runs before `fbq` is loaded it won't fire properly. Keep event code after the base code in source order. (Ch. 25)
- **Treating the pixel as tracking-only.** This underuses two of its three super powers (audience building and optimization). (Ch. "Power of the Pixel")
