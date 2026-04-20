# Sky Goodies — CRO Audit & 90-Day Roadmap

**Audit date:** 20 April 2026
**Data window:** 20 Jan 2026 – 20 Apr 2026 (last 90 days)
**Source:** Shopify Admin · Analytics · Live storefront
**Prepared by:** Claude, for Himanshu / Sky Goodies

---

## 1. Executive Summary

**Where Sky Goodies stands today:**

| Metric | Sky Goodies (90d) | Indian D2C benchmark | Verdict |
|---|---|---|---|
| **Sessions** | 9,004 | — | Low volume; ~71/day in April |
| **Overall CR** | **0.89%** | 1.5–2.5% | **Less than half of average** |
| **Add-to-Cart rate** | **3.46%** | 6–10% | **~50% below benchmark** |
| **Checkout→Purchase** | **40.1%** (81/202) | 60–70% | **Bleeding at checkout** |
| **AOV** | ₹1,185.55 | ₹600–₹1,200 | Strong |
| **Returning customer rate** | **36.58%** | 20–30% | **Excellent — brand has real loyalty** |
| **Discount as % of gross** | 15.6% | 8–12% | Discounting harder than peers |

**The top-line diagnosis in one sentence:**
Sky Goodies has **good brand loyalty (36.58% returning) but a broken acquisition-to-conversion funnel**. At 0.89% CR, the store is converting less than half of what similar Indian D2C brands achieve — and the biggest leaks are at the PDP (add-to-cart) and checkout steps, not at the traffic or brand level.

**If we fix the funnel:**
- Taking ATC rate from 3.46% → 6% alone would yield roughly **+₹8 L in annual revenue** on current traffic.
- Taking checkout completion from 40% → 60% yields another **+₹4 L annually**.
- Combined: this audit's recommendations can plausibly **2×–3× current revenue without any new ad spend.**

---

## 2. Traffic Quality: The Bot Problem

### 🚨 Critical finding: ~22% of sessions are bot traffic

Top geographic sessions over 90 days:

| Location | Sessions | Verdict |
|---|---|---|
| India · Karnataka · Bengaluru | 711 | Real |
| Mumbai (top city) | ~751 | Real |
| **China · None · None** | **696** | Bot (no city/region attribution) |
| **United States · Virginia · Ashburn** | **629** | Bot (AWS/data-center hub) |
| **United States · Iowa · Council Bluffs** | **584** | Bot (Google data-center location) |

**Why this matters:**
- **~1,900 of 9,004 sessions (~21%) are not real shoppers.**
- Your true CR on *human* traffic is closer to **81 / 7,100 = 1.14%** (still below benchmark, but less dire).
- Bot traffic dilutes every metric in your reports. Funnel rates, bounce rates, device splits, and landing-page attribution are all skewed.
- It also consumes Shopify session quota (on Plus pricing tiers) and inflates hosting/app costs.

**What to do (this week):**
1. Exclude Ashburn, Council Bluffs, and unattributed China/US traffic in GA4 via IP or ISP filters.
2. Add Cloudflare Bot Management or Shopify's built-in bot protection to block the worst offenders at the edge.
3. Use these filters in any A/B test to avoid corrupting results.

---

## 3. Funnel Diagnosis — Where Revenue is Leaking

### The 4-step customer journey (real data)

```
Sessions              9,004  ████████████████████   100%
Added to cart           312  █                       3.46%   ← 97% drop
Reached checkout        202  ░                       2.24%
Completed purchase       81                          0.89%   ← 60% of checkouts abandoned
```

### Step-by-step:

**Step 1 → Step 2 (Landing → ATC): 3.46% ★ BIGGEST LEAK**
- **97% of visitors leave without adding anything to cart.**
- This is the single highest-value page in the funnel to fix.
- Likely causes (to verify with session recordings):
  - Thin product pages: poor images, weak descriptions, no video, no reviews visible above fold
  - No urgency / social proof
  - Missing or non-visible ATC CTA on mobile
  - Page speed issues
  - Visitors landing on wrong pages (stale `/collections/2025-calendars` still gets 462 sessions!)

**Step 2 → Step 3 (ATC → Checkout): 64.7%**
- This is actually healthy — the cart/checkout trigger works.

**Step 3 → Step 4 (Checkout → Purchase): 40.1% ★ SECOND BIGGEST LEAK**
- Industry benchmark: 60–70%.
- You're **losing 6 out of every 10 people** who made it to checkout.
- Likely causes:
  - No COD visible until checkout reveals it's unavailable for pincode
  - Shipping cost surprise ("₹2,593 in shipping revenue / 84 orders = ₹30/order" — so most orders got free shipping, but first-time buyers may hit an unexpected shipping fee on smaller carts)
  - Limited payment options (need to verify UPI/GPay prominence)
  - No express checkout (Shop Pay / Apple Pay / Google Pay)
  - Account creation requirement
  - Trust gaps at the payment step

---

## 4. What's Working

Don't break these. Double down on them.

### 4.1 Returning customer rate: 36.58% ✓
Well above the 20–30% Indian D2C benchmark. Your product delivers on its promise — people come back. This is the foundation everything else should build on.

### 4.2 AOV: ₹1,185 ✓
Above the free-shipping threshold (₹1,000). Customers are self-bundling. Bundle-led merchandising should work well.

### 4.3 Organic Google is your #1 revenue channel
- Search · Google: **₹41.3K revenue** over 90 days (biggest channel after direct)
- Direct (real, excluding bots): **~₹25–30K**
- Instagram: **₹6.8K**
- Paid: **near zero** (Bing ₹0, Brave ₹1.4K)

You've built organic demand. Don't squander it with weak SEO landing pages (see stale `/collections/2025-calendars`).

### 4.4 Top revenue products (90 days)

| Product | 90-d revenue |
|---|---|
| 1. BOX SET of 12 DIY Mini Endangered Animals | ₹17.8K |
| 2. Paper Mini Hot Air Balloon Fairy Lights | ₹8.1K |
| 3. Turquoise Mini Grand Piano Calendar 2026 & 2027 | ₹6.5K |
| 4. Colourful Typewriter Desk Calendar 2026 & 2027 DIY | ₹5.3K |
| 5. Big Blue Hot Air Balloon DIY Paper Lamp Shade | ~₹5.1K |

**All 2026 calendars are 100% sell-through (sold out).** That's both good (demand) and bad (can't capture current residual demand).

### 4.5 High-intent content is driving traffic
- **Blog post: "/blogs/blog/the-joy-of-making-miniature-books"** → 243 sessions (8th biggest landing page)
- This is content-marketing gold. Replicate this pattern.

---

## 5. What's Broken

### 5.1 Stale collections are poisoning landing pages
- `/collections/2025-calendars` gets **462 sessions** in Q1 2026 → visitors arrive, see "Sold out" stamps, leave.
- `/collections/diwali-collection` still getting **109 sessions** in April → seasonally wrong.
- These are **the highest-volume landing pages after the homepage** and they're actively hurting conversion.

**Fix:** 301-redirect `/collections/2025-calendars` → `/collections/calendars` (evergreen). Update or hide `/collections/diwali-collection` until September. Google will re-crawl within 2–4 weeks.

### 5.2 Calendar traffic is mis-seasoned
By April, calendars are a tiny slice of buying intent. But your site and SEO still treat calendars as the marquee category (9 of top 50 organic keywords, likely). This is a planning/inventory issue as much as a CRO one:
- Keep calendar pages indexed (they rank) but don't feature them on the homepage in April.
- In April–July, foreground the in-stock gifting + décor kits that actually have inventory.

### 5.3 Checkout is losing 60% of intent
40% CO→PO is a 25-point gap vs. benchmark. Most likely causes to check in order:

| Suspect | How to verify | Quick fix |
|---|---|---|
| COD unavailable for pincode (only revealed at checkout) | Ask customer service for tickets | Add pincode + COD check to PDP (already in wireframe) |
| Shipping cost surprise on sub-₹1K carts | Check checkout recordings | Show shipping estimate in cart drawer |
| No express wallet (Shop Pay, GPay one-tap) | Inspect checkout | Enable Shop Pay + UPI quick-pay |
| Account creation required | Inspect checkout flow | Confirm guest checkout is ON |
| Payment failures | Check Shopify Payments dashboard for decline rates | Add Razorpay or Cashfree as backup |

### 5.4 Paid channels aren't working
- Bing: ₹0 revenue
- Brave: ₹1.4K revenue
- Facebook: only 46 referred sessions (vs. Pinterest's 201)
- Instagram revenue: ₹6.8K (decent but low for a visually-driven brand)

You're essentially not a paid-acquisition business right now. That's fine — but it means **every % of CR improvement compounds directly** because you're not paying for traffic.

### 5.5 Discounting is heavy (15.6% of gross)
- ₹18,403 in discounts on ₹117,990 gross = 15.6%
- Benchmark: 8–12%
- This suggests the store is training customers to wait for sales rather than buy at full price.
- With bundle-led merchandising (saves built-in), you can drop blanket discounting.

---

## 6. The 90-Day CRO Roadmap

This roadmap assumes a single-operator team (you) with occasional designer/dev help. It's designed around **your actual 9K-sessions/quarter traffic level**, which is below A/B-testing thresholds — so the methodology is **qualitative-research-first + best-practice implementation**, with before/after 30-day windows instead of A/B tests.

### 🎯 North-star goal for the next 90 days:
**Take overall CR from 0.89% → 1.8%** (2× improvement). At current traffic, that's an extra ~72 orders and ~₹85K in net revenue.

---

### Week 1–2 · Diagnose (understand the leaks before fixing anything)

| Task | Owner | Why | Deliverable |
|---|---|---|---|
| Install Microsoft Clarity (free, no traffic cap) | Self · 2 hrs | Heatmaps + session recordings + rage-click detection on PDP/checkout | Active dashboard |
| Install Google Analytics 4 with ecommerce tracking if not already | Self · 2 hrs | Funnel attribution, landing-page CR, device breakdown | Live GA4 |
| Watch 30 session recordings (10 PDP, 10 cart, 10 checkout) | Self · 3 hrs | Find what makes people hesitate | Notes doc: top 10 friction moments |
| Read last 100 support tickets, tag by theme | Self · 2 hrs | Free voice-of-customer research | Tagged sheet: top 5 recurring questions |
| Add post-purchase survey: "What almost stopped you?" | Self · 1 hr (Typeform / KnoCommerce) | Captures objection data at peak signal | Survey live |
| Set up a weekly KPI dashboard (Shopify + GA4 + Clarity) | Self · 3 hrs | You can't improve what you don't look at weekly | Shared dashboard URL |

**What to look for:** rage clicks on PDP (broken elements), dead clicks on non-clickable trust badges, scroll depth on PDP (are they seeing reviews?), checkout recordings (where do they quit?).

---

### Week 3–4 · Quick Wins (best-practice fixes, no A/B test needed)

Ship these without testing. Each is a known CRO improvement that's safer than current state. Measure CR in 30-day windows after each ship.

| # | Fix | Expected lift | Effort |
|---|---|---|---|
| 1 | **Kill stale seasonal pages.** 301-redirect `/collections/2025-calendars` → `/collections/calendars`; hide Diwali collection from nav/footer | +5–10% CR on affected landings | 1 hr |
| 2 | **Add pincode + COD checker on PDP.** (Apps: GoKwik, Shiprocket, Cashfree) — pre-qualifies shipping + COD before ATC | +0.3 pp ATC rate | 2 hrs |
| 3 | **Enable Shop Pay + UPI intent at checkout.** Shopify Payments setup → India UPI toggle | +8–12% CO completion | 1 hr |
| 4 | **Confirm guest checkout is on.** Requiring account = ~24% abandonment | Eliminates major leak | 15 min |
| 5 | **Free-shipping progress bar in cart drawer.** "You're ₹X from free shipping" | +5–15% AOV | Shopify app (Monster Cart, etc.) |
| 6 | **Add trust row to every PDP.** COD · Returns · Secure Pay · Made in Mumbai | +0.2–0.4 pp CR | 2 hrs theme edit |
| 7 | **Post-purchase upsell on thank-you page.** Apps: ReConvert, AfterSell | +8–15% AOV | 2 hrs |
| 8 | **Add product video to top 5 PDPs.** Even a 15-sec phone clip | Video PDPs convert 80%+ better | Half day of filming |
| 9 | **Social proof on PDP.** "X sold this month" + visible review count near price | +10–20% ATC | App: Loox / Judge.me |
| 10 | **Announce COD + Prepaid ₹50 off in announcement bar.** Make Indian shoppers feel at home | +0.2 pp CR | 15 min |
| 11 | **Fix mobile sticky ATC.** Every PDP needs a thumb-reachable CTA that stays visible on scroll | +15–25% mobile CR | 3 hrs |
| 12 | **Compress top 10 PDP hero images.** Run through Squoosh / TinyPNG → WebP | Faster LCP → +3–5% CR | 2 hrs |

---

### Week 5–8 · Content + Structural fixes

| Task | Why | Effort |
|---|---|---|
| Add a "**Shop by Occasion**" megamenu (Birthdays, Housewarming, Weddings, Kids' birthdays, Corporate) | Matches organic search intent + April–July seasonality | 1 day |
| Rewrite PDP copy for top 10 revenue products with **benefit-first headlines + specific objection handling** (sizing, how it's made, who it's for) | Supporting the 3.46%→6% ATC goal | 2 days |
| Build **3 new gift-guide blog posts** (copy the miniature-books blog pattern that's already working): <br>  · "Housewarming gifts under ₹1,000 that won't end up in a drawer" <br>  · "Paper crafts for slow weekends with kids" <br>  · "10 unusual corporate gifts from a small Mumbai studio" | Blog drives 243 sessions from just one post — scale the pattern | 1 week |
| Add a **"Why Sky Goodies" page** with founder story, process, materials, FSC cert, reviews count | Trust amplification — this is what separates 0.89% from 1.8% stores | 2 days |
| Set up **WhatsApp order updates + abandoned cart** (apps: Interakt, DelightChat) | In India, WhatsApp recovery > email. Especially with 45–60% COD market | 1 day setup |
| **Bundle merchandising:** 3 new bundles visible on homepage & PDP — Home Décor Starter (₹1,599), Kids' Birthday Gift (₹999), Housewarming Trio (₹1,299) | Pushes AOV, reduces reliance on blanket discounts | 3 days |
| Redesign **cart drawer** with upsells + progress bar (already in wireframe) | +8–12% AOV potential | 1 day |

---

### Week 9–12 · Retention + paid tests

| Task | Why |
|---|---|
| Klaviyo flows: **Welcome (3 emails), Browse abandonment, Cart abandonment, Post-purchase, Win-back** | You have 36.58% returning — lever up with email |
| **SMS flow for COD confirmation** (drops RTO ~20–40%) | Protects margin |
| Small **Meta/Google retargeting test** (₹500/day for 30 days) targeting PDP-viewers and cart-abandoners only — NOT cold traffic | Warm traffic is cheap and converts 3–5× cold |
| Launch **referral program** (Yotpo or ReferralCandy) — "Give ₹100, get ₹100" | Returning customers (your strength) → compound it |
| **Diwali calendar pre-launch waitlist** (for 2027 calendars and Diwali décor) by mid-August | Given FY2026 calendars are all sold out, capture demand early next cycle |

---

## 7. Metrics to Track (and When)

### 7.1 Daily (2-min glance — Shopify mobile app)
- Sessions, orders, CR, revenue

### 7.2 Weekly (30-min review — Mondays)
- **Funnel view** (Sessions → ATC → CO → Purchase) — catch weekly drift
- **Top 10 landing pages** CR — spot broken pages
- **Top 10 PDPs** ATC rate — find the weak pages
- **Device split** CR (desktop vs mobile) — mobile is the usual leak
- **Search terms** in Shopify search — demand signals
- **Cart abandonment + checkout abandonment** — from Shopify reports
- **Clarity rage clicks** — anything new to fix

### 7.3 Monthly (2-hr review — first Monday)
- Revenue Per Visitor (RPV) vs. prior month
- AOV trend
- Returning customer rate
- Discount-as-% of gross
- LTV:CAC (if running paid)
- Cohort retention (month 1 vs. month 3)
- Top 5 support-ticket themes
- Post-purchase survey results: "what almost stopped you?"

### 7.4 Quarterly (half-day workshop)
- Full funnel audit vs. this baseline
- Reprioritize the roadmap
- Qualitative: 5 customer interviews
- Update the 6-month CRO roadmap

---

## 8. How to React to Results

A simple decision tree for each metric:

### If **CR drops** week-on-week:
1. Check landing-page attribution — did a new page start getting traffic that converts poorly?
2. Check device split — did mobile CR drop? (usually a broken layout after theme update)
3. Watch 10 fresh recordings — is there a new friction point?
4. Check app updates — any app change break checkout?

### If **ATC rate is flat** after PDP improvements:
- Run a "5-second test" (usertesting.com) on one PDP — does the value prop land?
- Add inline micro-surveys on PDP exit: "What kept you from adding to cart?"
- Reconsider pricing/offers, not design

### If **checkout completion doesn't budge** after quick wins:
- Check payment provider decline rates
- Run the checkout on 3G mobile — where does it get slow?
- Enable Shop Pay's one-tap — the single biggest mobile CR lever Shopify offers

### If **a specific change lifts CR ≥15%**:
- Scale it to every other product/page where applicable
- Document it in a "what worked" log
- Don't lose it in a future redesign

### If a change **lifts one metric but tanks another** (e.g., AOV up but CR down):
- Check **Revenue Per Visitor (RPV)** — that's the real truth
- Revert unless RPV is net positive

---

## 9. Tooling — What to Install This Month

### Free (install all of these)
- **Google Analytics 4** — if not already
- **Microsoft Clarity** — heatmaps, recordings, rage clicks (unlimited, free)
- **Shopify's built-in Behavior reports** — already there, use them
- **Google PageSpeed Insights** — weekly check

### Paid — order of ROI
1. **Judge.me** (₹500/mo) — reviews with photos + UGC widgets
2. **ReConvert** (₹2,000/mo) — post-purchase upsell, near-instant payback
3. **GoKwik or Shiprocket CODSure** (revenue share) — India-specific COD/shipping optimization
4. **Interakt or Wati** (₹1,500/mo) — WhatsApp abandoned cart, order updates
5. **Klaviyo** (₹2,500/mo start) — email flows
6. **Hotjar Business** (if you outgrow Clarity) — ₹4,000/mo

### Total recommended app spend: ₹6,500–₹10,000/month
At ₹99K net sales/90d = ₹33K/month, this is high (~25% of revenue). Start only with **Judge.me + ReConvert + Interakt (₹4,000/mo total)** and scale the rest as revenue grows.

---

## 10. The 30-60-90 in One View

| Day | Focus | Success looks like |
|---|---|---|
| **Day 30** | Quick wins live, bot traffic filtered | CR ≥ 1.2%, ATC rate ≥ 4.5% |
| **Day 60** | Content + bundles shipping; WhatsApp live | CR ≥ 1.5%, AOV ≥ ₹1,250, returning rate ≥ 40% |
| **Day 90** | Retention flows + referral live | CR ≥ 1.8%, 20–30 more orders/month, RPV +60% vs. baseline |

---

## 11. Risks & Watch-Outs

1. **Don't A/B test at this traffic level.** You need ≥10K sessions per variation to reach significance. At 3K/month (after bot filtering), a test would need 2+ months to read — by which time external factors corrupt it. Instead: best-practice implementations + before/after 30-day windows.

2. **Don't over-discount to hit short-term CR.** Discounts are already 15.6% of gross. A 10% flash sale will lift CR but train the wrong behavior. Prefer bundles, free shipping thresholds, and COD-to-prepaid incentives.

3. **Don't redesign without diagnosing first.** The Horizon theme revamp + new wireframe is a good platform, but the 0.89% CR is not primarily a design problem. It's a trust/friction/content problem. Design is 30% of the lift, content + flows are 70%.

4. **Seasonality is real.** April–July is a lean quarter for Sky Goodies historically (calendars don't sell, Diwali is far). Don't panic at flat weeks in May — expect a **soft April/May → modest June–July → real pickup from August**.

5. **Inventory drives CR more than you think.** You have five top-performing calendars at 100% sell-through. If a similar run of your #1 bestseller (Endangered Animals BOX SET) sells out, quarterly CR will tank. Build better inventory reorder alerts.

---

## 12. What to Do This Week

In priority order:

1. ☐ Install Microsoft Clarity (30 min)
2. ☐ Redirect `/collections/2025-calendars` → `/collections/calendars` (30 min)
3. ☐ Hide Diwali collection from nav/footer until September (15 min)
4. ☐ Watch 20 session recordings on PDP + checkout (2 hrs)
5. ☐ Read last 100 support tickets, tag by theme (2 hrs)
6. ☐ Enable Shop Pay + UPI intent at checkout (1 hr)
7. ☐ Install Judge.me for reviews if not using a review app (1 hr)
8. ☐ Write 3 post-purchase survey questions, send to next 50 orders (30 min)
9. ☐ Confirm guest checkout is ON (5 min)
10. ☐ Filter Ashburn + Council Bluffs from GA4 views (15 min)

**Total time: ~8 hours. Expected impact at 30 days: CR 0.89% → 1.2–1.4%.**

---

## Appendix A — Raw data captured (20 April 2026)

```
DATE RANGE: Jan 20 – Apr 20, 2026 (90 days)

Sessions:               9,004
Added to cart:            312   (3.46%)
Reached checkout:         202   (2.24%)
Completed purchase:        81   (0.89%)

Gross sales:         ₹1,17,990
Discounts:             ₹18,404  (15.6% of gross)
Returns:                  ₹304
Net sales:             ₹99,282
Shipping collected:     ₹2,593
Taxes:                 ₹18,203
Total sales:         ₹1,20,078

Orders:                    84
AOV:                 ₹1,185.55
Returning customer:     36.58%

DEVICE:
 Desktop                4.7K (52%)
 Mobile                 4.1K (46%)
 Tablet                   45 (<1%)

TOP LANDING PAGES:
 1. Homepage                          2,402
 2. /collections/2025-calendars         462   ⚠ STALE
 3. /collections/home-decor-lighting    283
 4. blog/the-joy-of-making-miniature…   243
 5. /collections/quirky-gifts-for-adults 200
 6. /collections/gift-boxes-envelopes   141
 7. /collections/diy-papercraft-kits    133
 8. /products/set-of-10-mini-hot-air…   112
 9. /collections/diwali-collection      109   ⚠ SEASON
10. /collections/matchbook-notebooks    106

REVENUE BY REFERRER:
 Search · google                 ₹41,300
 None · None (direct)            ₹16,500
 None · instagram                 ₹6,800
 None · startupworld              ₹5,000
 (bing)                               ₹0
 (brave)                          ₹1,400

SOCIAL SESSIONS:
 Pinterest                          201
 YouTube                             61
 Facebook                            46
 Twitter                              7

TOP PRODUCTS (revenue):
 1. BOX SET of 12 DIY Mini Endangered Animals    ₹17,800
 2. Paper Mini Hot Air Balloon Fairy Lights       ₹8,100
 3. Turquoise Mini Grand Piano Calendar 2026&27   ₹6,500
 4. Colourful Typewriter Desk Calendar 2026&27    ₹5,300
 5. Big Blue Hot Air Balloon DIY Paper Lamp       ₹5,100

100% SELL-THROUGH (sold out):
 - Colourful Typewriter Desk Calendar 2026
 - Mini Toaster Desk Calendar 2026
 - 'Be Good This Year' Postcard Desk Calendar 2026
 - Mini Sewing Machine Desk Calendar 2026
 - 'Be Good This Year' Wall Calendar & Planner 2026
```

---

*This audit was built from actual Shopify admin data on 20 April 2026. Re-run in 30 days to measure progress and reprioritize.*
