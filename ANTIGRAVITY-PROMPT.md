# Antigravity Prompt — Sky Goodies Homepage Build (Tinker Theme)

## Context

You are working on the Sky Goodies Shopify store built on the **Tinker theme** at this repo. The goal is to ship a production homepage that matches the v5 wireframe exactly, then push to GitHub (master) which auto-syncs to Shopify.

**Visual spec (ground truth):** `Wireframe/homepage-wireframe-v5.html`
Open this file first and study every section. Your Liquid output must render visually identical to this wireframe — same spacing, same colors, same typography, same interactions.

**Brand voice & rules:**
- Warm, human, craft-forward. NOT corporate or salesy.
- NO black anywhere (not `#000`, not `#1E1B18` as a background).
- NO purple or shades of purple.
- NO emojis.
- Allowed colors:
  - Orange `#E8845A` (primary CTA, accents)
  - Orange soft `#F5A67A`
  - Cream `#FAF6F0` (section backgrounds, soft cards)
  - Warm white `#FDFCFA` (page base)
  - Dark brown `#3D3833` / deep `#1E1B18` (TEXT only, never section bg)
  - Muted `#7A7168`
  - Border `#EDE8E2`
  - Peach accent `#FCEEE6`
  - Lime green `#C8E616` — ONLY on the hero curvy blob
- Fonts: DM Sans (body) + DM Serif Display (headings)
- Mobile-first (80% traffic is phone)

**Already completed in this worktree (do not rebuild):**
- `sections/sg-hero.liquid` — slideshow with lime-green blob (review before editing)
- `sections/sg-shoppable-video.liquid` — new shoppable video section
- `sections/sg-categories.liquid` — horizontal scrolling circles
- `sections/sg-announcement.liquid` — auto-rotating messages
- `snippets/sg-product-card.liquid` — reusable product card with pills

**What you need to deliver:**

---

## 1. Rewrite `assets/sg-theme.css` to match v5 wireframe

Read `Wireframe/homepage-wireframe-v5.html` and extract every style. The current sg-theme.css is outdated.

Build a comprehensive stylesheet with:
- `:root { --sg-* }` custom properties for every color, font, radius, spacing value
- Typography utilities matching v5 (h1 clamp(40px, 8vw, 72px), serif italic, etc.)
- Button system: `.sg-btn-primary` (orange fill + white text, fully rounded pill), `.sg-btn-outline` (cream fill + brown text + brown border), `.sg-btn-atc` (for product cards)
- Section spacing: `.sg-section` with padding 40px mobile / 60px desktop
- All section-specific styles matching v5 exactly (hero with blob, categories circles, bestsellers with pills, shoppable video cards, kids grid, how-it-works with SVG curve + paper plane, adults banner, gifting 3-cards, press marquee, testimonials with top images, brand-story split, newsletter, mega menu, cart drawer with progress bar)
- Animations: fade-up scroll, marquee, announcement rotation, category nudge
- Mobile-first breakpoints at 750px and 1024px

All classes prefixed `sg-`. Preserve scoping so it doesn't conflict with Tinker theme base styles.

Target size: ~50KB.

---

## 2. Rewrite `sections/sg-process.liquid` (How It Works with paper plane)

Layout: 3 numbered step circles connected by an SVG dotted curve path with a paper plane at the end.

**Desktop:** zigzag layout — step 1 top-left, step 2 middle-bottom, step 3 top-right. SVG path with `stroke-dasharray: 2 10` curves through them. Paper plane SVG icon floats at the end of the path.

**Mobile:** vertical stack with dotted curve on the left connecting each step vertically.

Section schema:
- Settings: `heading`, `eyebrow`, `subheading`, `padding_top` (range 0-100), `padding_bottom`, `background_color` (color)
- Block type "step" (min 3, max 3): `step_number` (text, e.g. "01"), `title`, `description`

Default content (preset):
1. "Open the kit" — "Pre-cut, colour-coded pieces. No scissors, no tears, no hunting for glue that dried out in 2019."
2. "Fold, score, slot" — "Follow the illustrated guide. Most kits are done in an hour — slow down, enjoy the process, breathe."
3. "Display & glow" — "Your finished piece is keepsake-quality. Hang the lights, set up the decor, share the joy."

---

## 3. Rewrite `sections/sg-featured-products.liquid` (Bestsellers)

Already uses `sg-product-card` snippet. Make sure:
- Section has heading "Loved by thousands", eyebrow "BESTSELLERS", subheading
- Collection picker setting
- Max 6-8 products shown
- 3-column desktop / horizontal scroll mobile
- Full settings for padding, colors, column count
- Preset with reasonable defaults

The product card already shows pills + orange-outline ATC. Verify metafield pattern works (`product.metafields.custom.build_time`, `age`, `difficulty`) with graceful fallback to text like "1 hr", "All ages", "Easy".

---

## 4. Split `sections/sg-split-collection.liquid` into two sections

**a) `sections/sg-kids-collection.liquid`** — centered heading + 4-product grid

- Settings: `heading` (default "For little hands with big ideas"), `eyebrow` ("FOR LITTLE MAKERS"), `subheading`, `collection` picker, `product_count` (range 4-8), `link_text` (default "Shop all kids kits →"), `link_url`
- Centered header, then grid using `sg-product-card` snippet
- Bottom "Shop all" link
- Standard padding settings

**b) `sections/sg-adults-banner.liquid`** — banner with CTA + 4-product grid

- Section-level: `eyebrow` ("INTRODUCING"), `heading` ("Slow making for grown-ups"), `subheading`, `banner_image` (image_picker), `cta_text` ("Explore the collection"), `cta_url`, `collection` picker for products, `product_count`
- Banner: full-width image with overlay text and CTA pill (orange)
- Products below: 4 adult product cards using `sg-product-card`
- Standard padding settings

Delete or deprecate `sg-split-collection.liquid`.

---

## 5. Rewrite `sections/sg-gifting.liquid`

- Centered heading + subheading (flex column, align-items: center, max-width 680px)
- 3 cards in a row (stack mobile, max 6 blocks)
- Each card: image (square, 24px radius) + title + description + "Explore →" link
- Card internals left-aligned
- Block settings: `title`, `description`, `image`, `link_text`, `link_url`
- Section settings: heading "Made to be gifted", eyebrow "GIFTING", subheading, padding, background
- Preset with 3 default blocks: Kids' Return Gifts / Bulk & Party Orders / Corporate Gifts

---

## 6. Rewrite `sections/sg-press-logos.liquid` — Marquee

- Continuous scrolling marquee (CSS animation, no JS)
- Fade edges via `mask-image: linear-gradient(...)`
- Each block: `logo_image` (optional) OR `logo_text` (fallback styled text)
- Duplicate block list twice in markup for seamless loop
- Section settings: `eyebrow` (default "The good company we keep"), padding, speed
- Preset with 8 default text blocks (Nat Geo, Hot Wheels, CRED, Barbie, Discovery, UNESCO, Tata, NCPEDP)

---

## 7. Rewrite `sections/sg-testimonials.liquid` — User images at top

- Heading "Real people, real craft" (centered)
- Horizontal scrollable row of cards (snap points on mobile)
- Each card block:
  - `customer_image` (image at top, 100% width, square/portrait aspect)
  - `rating` (number, 1-5, default 5)
  - `review_text` (textarea)
  - `customer_name`
  - `verified` (checkbox, default true)
  - `date` (text)
- Card: 24px radius, cream border
- Stars in gold `#D4A853`
- Preset with 4 default blocks using real-sounding reviews

---

## 8. Rewrite `sections/sg-brand-story.liquid`

- Two-column layout (stack mobile)
- LEFT: image (image_picker setting)
- RIGHT: eyebrow, heading "Paper can spark something wonderful" (keep this heading), 2 paragraphs of story, "Read the full story →" link
- Settings: `eyebrow` (default "THE SKY GOODIES STORY"), `heading`, `story_para_1`, `story_para_2`, `link_text`, `link_url`, `image`, padding, background
- Default image: a Ganpati/pooja decor from Sky Goodies CDN (use `https://cdn.shopify.com/s/files/1/0428/5530/1271/collections/Sky-Goodies-DIY-Paper-Banana-Trees-06.jpg?v=1741609615`)

---

## 9. Create `snippets/sg-cart-drawer.liquid`

Included in `layout/theme.liquid` once, so cart drawer is available on every page.

Structure:
- Fixed overlay + slide-in drawer from right (400px desktop, 100% mobile)
- Header: "Your cart ({{ cart.item_count }})" + close X
- Free shipping progress bar: threshold `100000` cents (Rs.1000)
  - Fill percentage = `cart.total_price / 100000 * 100` capped at 100
  - Text: if under threshold: "You're Rs.X away from free shipping!"; if over: "Congratulations! You've unlocked free shipping!"
- Cart items list: loop `cart.items`, show image, title, variant, quantity (- 1 +), line price, remove link
- "You may also like" section: show 3 products from `collections.featured.products` or similar fallback
- Subtotal + full-width orange checkout button with price

Include inline JS for:
- Open/close handlers (listens for `click` on elements with `data-sg-cart-toggle`)
- Quantity update via fetch to `/cart/change.js`
- Remove via fetch to `/cart/change.js` with quantity 0
- Reload drawer content on cart update

Then in `layout/theme.liquid`:
- Include the snippet right before `</body>`: `{% render 'sg-cart-drawer' %}`
- Also include the CSS: `{{ 'sg-theme.css' | asset_url | stylesheet_tag }}` in `<head>` if not already present
- Add `data-sg-cart-toggle` attribute to the cart icon in the header

---

## 10. Add a mega menu snippet `snippets/sg-mega-menu.liquid`

Yourbasil-style mega menu to be included in the header. Structure:
- Triggered by "Shop" link click
- Full-width dropdown panel with:
  - 3 text-link columns (Shop by Product / Shop by Occasion / Shop by Age)
  - Divider line
  - 4 featured cream "pot" cards below with collection images
- Generous whitespace (56px top/bottom, 80px horizontal desktop)
- Click "Shop" button in header to toggle; click outside or Escape to close

Link data can be hardcoded to match v5 wireframe (Party Decor, Fairy Lights, Kids Kits, Home Decor, Calendars, Pooja Decor etc.). For the 4 featured cards, use collection handles: `new-arrivals`, `bestsellers`, `under-500`, `on-sale` (if these don't exist on the store, fall back to any collection).

Hook into the header — you'll need to either modify `sections/header.liquid` (or whichever header file the Tinker theme uses) to include `{% render 'sg-mega-menu' %}` and adapt the "Shop" link to toggle it.

---

## 11. Add wishlist icon to header

The header needs a heart/wishlist icon between search and account. If the Tinker theme doesn't natively support wishlist, just add a link to `/pages/wishlist` or `#` placeholder with a heart SVG.

Modify `sections/header.liquid` (or whichever header file Tinker uses) to add this icon.

---

## 12. Update `templates/index.json`

Update the homepage section order and content to match v5 wireframe. Target order:

1. `sg_announcement` (announcement bar)
2. `sg_hero` (slideshow)
3. `sg_categories` (circles)
4. `sg_featured_products` (bestsellers — "Loved by thousands")
5. `sg_shoppable_video`
6. `sg_kids_collection`
7. `sg_process` (how it works with paper plane)
8. `sg_adults_banner`
9. `sg_gifting`
10. `sg_press_logos` (marquee)
11. `sg_testimonials`
12. `sg_brand_story`
13. Newsletter (can use Tinker's native newsletter section OR create `sg-newsletter.liquid`)

Each section should have proper block configuration with default content matching v5 wireframe.

---

## 13. Commit & push

When everything is working:
1. Review all changes locally
2. `git status` + `git diff` to verify
3. Commit with message: `"feat: v5 homepage — yourbasil-style rework with slideshow, shoppable video, paper plane steps"`
4. Push to `master` branch (this triggers Shopify sync)

---

## Shopify section schema conventions (remind yourself)

Every section must have a schema with:
- `name` (user-visible in theme editor)
- `tag` (usually "section")
- `class` (for CSS hooks)
- `settings` array (all section-level settings)
- `blocks` array (if applicable, with type + settings)
- `presets` array (default configuration shown when adding section)

Every setting supporting the v5 design:
- `padding_top`, `padding_bottom` as range 0-100 step 4 default varies
- `background_color` as color type
- `heading`, `eyebrow`, `subheading` as text/textarea

Image settings use `image_picker` type. For hero slides, each block should have BOTH `image` (desktop) and `image_mobile` settings so editors can upload separate images per viewport.

For block "image_size" setting on hero slides:
```json
{
  "type": "select",
  "id": "image_size",
  "label": "Image size",
  "options": [
    {"value": "auto", "label": "Auto"},
    {"value": "small", "label": "Small"},
    {"value": "medium", "label": "Medium"},
    {"value": "large", "label": "Large"}
  ],
  "default": "auto"
}
```

## Final sanity checks before push
- [ ] All sections render without Liquid errors
- [ ] No black backgrounds anywhere (except announcement bar which uses `#3D3833` brown)
- [ ] Mobile responsive at 375px
- [ ] All images load (use correct CDN URLs)
- [ ] Cart drawer opens on cart icon click
- [ ] Mega menu opens on "Shop" click
- [ ] Hero slideshow auto-rotates every 5s
- [ ] Announcement bar rotates every 7s
- [ ] Paper plane path + dotted curve visible in How It Works
- [ ] Category circles scroll horizontally with fade+chevron hint
- [ ] All "Add to cart" buttons are cream-fill + brown-outline pills (NEVER black)
- [ ] Wishlist icon present in header
- [ ] Footer has NO payment icon strip
- [ ] Press logos scroll as marquee
- [ ] Testimonial cards show user image at top

Once pushed, the Shopify admin at `in.skygoodies.co/admin` should reflect the changes within ~60 seconds via the theme sync.
