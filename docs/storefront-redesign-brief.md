# Haukao Storefront Redesign: Design and Implementation Brief

Status: proposal, not yet checked against the live store.
Prepared for: the Haukao merchant and Shopify Sidekick.

---

## 1. Recommendation (summary)

**Refine Shopify's current free flagship theme rather than buying a theme or building a custom one.**
Use the theme that is already installed if it is a recent Online Store 2.0 theme from Shopify (Horizon family or Dawn). If not, install Horizon (or Dawn) as an **unpublished** copy and build it there.
Almost everything in this brief can be done with **theme settings, section ordering, and one small custom CSS layer**. No paid theme or paid app is needed.

Order of work:
1. Global styles (colours, type, buttons, cards).
2. Header and search.
3. Homepage.
4. Collection pages.
5. Product pages.
6. Cart.

Each phase is previewed on an unpublished theme copy and published only with merchant approval.

**Business reason.** Haukao has a broad, still-forming catalogue and is on the Basic plan. The biggest wins are:
- shoppers find products fast (search and categories),
- shoppers trust the store (clear prices, real delivery and returns information),
- the store is quick on mobile.

A free Shopify-maintained theme gets security, checkout compatibility and performance updates at no cost. A light custom layer gets the "premium" feel without taking on code you have to maintain.

### Verified facts vs assumptions vs recommendations

| Type | Item |
|---|---|
| **Verified (from merchant brief)** | Brand Haukao; domain haukao.com; UK-operated; GBP; Shopify Basic plan; planned categories: gadgets, home, kitchen, desk essentials, travel, accessories. |
| **Not verified, not inspected** | Current theme, theme version, installed apps, catalogue size, product imagery quality, existing navigation, analytics, shipping and returns policies. **Claude has not inspected the store, its code, its settings or its analytics.** |
| **Not confirmed (do not invent)** | Suppliers, stock ownership, fulfilment arrangements, delivery times, returns terms, target audience, reviews. |
| **Assumptions** | Most traffic will be mobile (normal for UK e-commerce, to be confirmed in analytics). The catalogue will grow to many products across the six categories. Product photos come from several sources and vary in style. |
| **Recommendations** | Everything in sections 2–9 below. |

---

## 2. Handoff for Sidekick

### Objective
Make Haukao feel calm, premium and trustworthy while making it **faster to find and buy products**, especially on mobile. Success means:
- more shoppers use search or category navigation,
- more product page visits turn into add-to-cart,
- fewer shoppers drop out between cart and checkout.

These business outcomes are measured after launch (see acceptance criteria).

### Scope

**In scope:**
- Theme colour schemes, typography and global style settings.
- Header: logo, search, menu, cart icon.
- Announcement bar (only with verified content).
- Homepage sections and their order.
- Collection page template: grid, filters, sorting, empty state.
- Product page template: gallery, purchase area, delivery and returns block.
- Cart (drawer and/or page).
- Footer: navigation and policies.
- Search results page.
- Main menu and footer menu structure.
- One custom CSS layer (see 2.4).

**Must remain unchanged unless the merchant explicitly approves:**
- The **live/published theme**. All work happens on a duplicate or new unpublished theme.
- Products, prices, inventory, variants, product descriptions and product media (except alt text, with approval).
- Checkout settings, payment providers, shipping rates, taxes, markets, domains.
- Existing apps and their app blocks/embeds. Do not remove them; report them.
- Store policies text. Link to the policies, don't rewrite them, unless the merchant supplies new text.
- Existing URLs and handles of products and collections. Changing them breaks links and SEO.

### Proposed changes

#### 2.1 Colour roles (final proposed values, contrast checked)

Contrast was calculated with the WCAG 2.x formula. AA requires 4.5:1 for normal text and 3:1 for large text and UI parts.

| Role | Value | Use | Contrast |
|---|---|---|---|
| Background | `#FAFAF9` | Page background | — |
| Surface | `#FFFFFF` | Cards, header, drawers, inputs | — |
| Text primary | `#171717` | Headings, body, prices | 17.2:1 on background ✅ |
| Text secondary | `#626262` | Meta text, captions, helper text | 5.8:1 on background, 6.1:1 on white ✅ |
| Border subtle | `#E7E5E4` | Card outlines, dividers (decorative only) | 1.3:1, **decorative only** |
| Border control | `#8A8580` | Input, select, checkbox and quantity-selector borders | 3.7:1 on white ✅ (meets the 3:1 rule for UI parts) |
| Accent | `#C2410C` | Primary buttons, links, active states | White text on it 5.2:1 ✅; as text on white 5.2:1 ✅ |
| Accent hover/pressed | `#9A3412` | Hover and pressed for primary buttons and links | White text on it 7.3:1 ✅ |
| Accent tint | `#FFF7ED` | Selected filter chip background, subtle highlight | Text primary on it 16.9:1 ✅ |
| Focus ring | `#C2410C` 2px solid, 2px offset | All focusable elements | ✅ against white and background |
| Error | `#B91C1C` + icon + text message | Form errors | 6.5:1 ✅ |
| Success | `#15803D` + icon + text message | Added to cart, form success | 5.0:1 ✅ |
| Decorative gradient | `#FFF7ED → #FCE7F3 → #EEF2FF` | Hero and one feature band only | Body text `#171717` and `#626262` stay ≥5.1:1 across it ✅ |

Rules:
- **Do not put orange accent text on the gradient.** `#C2410C` on `#FCE7F3` is 4.4:1, which fails for small text. Use `#171717` text on gradients. Solid orange buttons on the gradient are fine.
- Status (sale, sold out, error, success) always uses **text and/or an icon, never colour alone**.
- The primary purchase button is **always solid accent with white text**. Never a gradient, outline or ghost style.

#### 2.2 Typography

- **Typeface:** Inter, from the Shopify font library. It is crisp, very readable at small sizes and served by Shopify (no extra licence or request). Use it for both headings and body. Use the system font stack as a fallback.
  - Alternative if Inter is not available in the theme's font picker: **"Instrument Sans"** or **"DM Sans"**, if available, or the system sans-serif stack. *Sidekick: check which fonts the font picker offers.*
- **Weights:** 400 (body) and 600 (headings, prices, buttons). Do not use more than these two.

**Type scale (mobile → desktop):**

| Style | Size | Line height | Weight | Notes |
|---|---|---|---|---|
| Display (hero only) | 32px → 48px | 1.1 | 600 | Letter-spacing −0.02em |
| H1 (page title) | 26px → 36px | 1.15 | 600 | Letter-spacing −0.01em |
| H2 (section) | 22px → 28px | 1.2 | 600 | |
| H3 (card group / block title) | 18px → 20px | 1.3 | 600 | |
| Body | 16px | 1.55 | 400 | Never below 16px for body; this also stops iOS zooming into inputs |
| Small / meta | 14px | 1.45 | 400 | Secondary colour |
| Product card title | 14px → 15px | 1.35 | 400 | Up to 2 lines, then truncate with ellipsis |
| Price | 15px → 16px | 1.3 | 600 | Format £12.99. Sale: new price in text primary, old price struck through in secondary, plus visible text such as "Was £15.99" |
| Button / label | 15px | 1 | 600 | Sentence case, no all-caps |

#### 2.3 Spacing, radius, shadows, buttons, cards, gradients

- **Spacing scale (4px base):** 4, 8, 12, 16, 24, 32, 48, 64, 96.
  - Section vertical padding: 48px mobile / 80px desktop.
  - Page side gutter: 16px mobile / 32px desktop.
  - Max content width 1280px.
- **Corner radius:**
  - 8px for buttons, inputs and chips;
  - 12px for cards and images;
  - 16px for drawers and modals (top corners on mobile sheets).
  - Pill (999px) only for filter chips.
- **Shadows:** none on cards at rest. Use 1px `#E7E5E4` borders instead.
  - Hover (pointer devices only): `0 4px 16px rgba(23,23,23,0.06)`.
  - Drawers: `0 8px 32px rgba(23,23,23,0.10)`.
  - No other shadows.

**Buttons:**
- **Primary:** background `#C2410C`, white text, 8px radius, minimum height 48px, full width on mobile product page. Hover/pressed `#9A3412`. Disabled: `#E7E5E4` background, `#626262` text, and visible label text such as "Sold out".
- **Secondary:** white background, `#171717` text, 1px `#8A8580` border, same size.
- **Tertiary/link:** `#C2410C` text, underlined on hover and always underlined inside body text.
- Every tap target is at least 44×44px.

**Product card:**
- Image ratio **1:1 (square), cropped to fit, white background**. Use one ratio site-wide. Square suits mixed gadget, home and kitchen photography.
- Title: up to 2 lines.
- Price below the title.
- Optional vendor/brand line: off by default, because suppliers are unconfirmed.
- **Badges allowed:** "Sale" and "Sold out" only, as text. No "Hot", "Trending" or countdowns.
- Hover on desktop: card lifts by the hover shadow, and the second image shows if one exists. No scaling of text.
- **Quick add:** enable only if the theme supports it natively and products are mostly single-variant. Otherwise leave it off. *Merchant decision.*
- **Missing image:** the theme's neutral placeholder on `#FFFFFF` with the product title. Never a stock or fake image.

**Gradient rules:**
- Allowed in **two places only**: the homepage hero background and one optional homepage "brand promise" band.
- Direction 135°.
- Never behind product grids, product images, prices, forms or checkout.
- No glass/blur effects over text.

**Motion:**
- 150–200ms ease-out for hover, drawer open and accordion.
- No autoplay carousels.
- No parallax.
- No scroll-triggered reveal animations on product grids.
- Respect `prefers-reduced-motion: reduce` by turning off non-essential transitions.

#### 2.4 Custom CSS layer (small, optional)

Use the theme's built-in colour schemes, typography and spacing settings first. Use custom CSS only for what settings can't do: gradient hero, card hover, focus ring, reduced motion.

Reference CSS is in `docs/design/haukao-tokens.css` in the GitHub repository. Paste it into **Theme settings → Custom CSS**, or into a section's Custom CSS field. *Sidekick: check the theme's custom-CSS character limit and supported selectors. If it is too long, keep only the hero gradient, focus ring and reduced-motion rules.*

#### 2.5 Header and search

- **Desktop, one row:**
  - Logo left (wordmark "HAUKAO" or the existing logo, max height 32px).
  - **Search field centred and wide (min 480px)**, with placeholder **"Search Haukao"**.
  - Account icon and cart icon with item count on the right.
- **Desktop, second row:** the category menu (see menu below).
- **Mobile:**
  - Row 1: menu (hamburger) button, logo, cart.
  - Row 2: **full-width search field always visible**, not hidden behind an icon.
  - Header is sticky on scroll-up only, if the theme supports it, so it doesn't take up screen space while reading.
- **Predictive search:** turn on (built into Shopify's free themes). Show products, collections and pages. Search must cover product title, product type, tags and vendor. *Sidekick: check the search settings and Search & Discovery app settings.*
- **Search synonyms:** set up in the free **Shopify Search & Discovery** app (made by Shopify), for example:
  - "phone holder, phone stand, mobile stand"
  - "flask, bottle, water bottle"
  - "organiser, organizer"

  The last one handles UK vs US spelling, which matters for a UK store.
- **Main menu:** six top-level items, in this order: **Gadgets · Home · Kitchen · Desk · Travel · Accessories**, then **New in** if a "new arrivals" collection exists.
  - At most one level of sub-items per category.
  - **Hide or omit any category that has no products yet.** Do not link to empty collections.
- **Announcement bar:** turn on **only** with merchant-verified text, for example a real delivery or returns statement. Suggested *template* (merchant must fill in and confirm): "UK delivery from £[X] · [N]-day returns".
  - **Do not publish placeholder values.**
  - If nothing is confirmed, turn the announcement bar off.

#### 2.6 Homepage (section order)

1. **Header** (as above).
2. **Hero:**
   - Gradient background (`#FFF7ED → #FCE7F3 → #EEF2FF`, 135°), compact height (about 40% of the viewport on desktop, under 360px on mobile).
   - Content left-aligned:
     - Heading: **"Everyday finds, thoughtfully chosen."**
     - Subheading: **"Gadgets, home, kitchen and travel essentials, shipped from the UK."**
     - Primary button **"Shop new in"** → New in collection, or "Shop all" → /collections/all if there is no New in.
   - Optional: a single product or lifestyle photo on the right (desktop only). No carousel.
3. **Category tiles:**
   - Heading **"Shop by category"**.
   - Six tiles (square images, 12px radius, label below).
   - Mobile: 2-column grid of six, or a horizontal scroll row showing about 2.5 tiles with a visible scroll hint.
   - Hide tiles for empty categories.
4. **Featured collection: "New in"**:
   - 8 products, 4 columns on desktop, 2 columns on mobile.
   - "View all" link.
5. **Featured collection: one category** (merchant's choice, for example Desk essentials) with the same card layout. Leave out if there are fewer than 4 products.
6. **Brand promise band** (optional gradient band, or plain surface):
   - Three short columns with icons.
   - **Only use statements the merchant confirms are true.** Candidate copy:
     - "Shipped from the UK"
     - "Secure checkout"
     - "Help when you need it" → contact page
   - **No delivery times, returns windows or review claims until verified.**
7. **Featured collection: best sellers** — **only** once there is real sales data. Until then, leave it out (do not label products "best sellers" without evidence).
8. **Newsletter signup** (plain surface):
   - Heading "Get new arrivals first".
   - One email field and a "Sign up" button.
   - No promised discount unless the merchant confirms one.
9. **Footer:**
   - Columns: **Shop** (the categories), **Help** (Contact, Shipping, Returns, FAQ if it exists), **About** (About Haukao, policies).
   - Payment icons (theme setting, shows the payment methods actually enabled).
   - Country/currency selector only if more than one market is active.
   - Legal links: Privacy policy, Terms of service, Refund policy, Shipping policy (Shopify policy pages).

**Leave out:** testimonials/reviews (none verified), countdown timers, "only X left" messages, Instagram feeds, video autoplay.

#### 2.7 Collection pages

- Collection title (H1) and an optional one-line description. No large banner image, so products show above the fold.
- **Filters** from Search & Discovery: Availability, Price, Product type, plus any real product options (Colour, Size).
  - Desktop: left sidebar.
  - Mobile: a "Filter and sort" button that opens a bottom sheet, with active filters shown as removable chips above the grid.
- **Sort options:** Featured, Price low–high, Price high–low, Newest.
- **Grid:** 2 columns on mobile, 3 on tablet, 4 on desktop. 24 products per page, with paging or a "Load more" button, not infinite scroll (better for accessibility and the footer).
- Product count shown, for example "48 products".
- **Empty collection state:** heading "Nothing here yet", text "We're adding products to this category soon. Browse everything we have in the meantime.", button "Shop all" → /collections/all. No fake products.
- **No search results state:** "No results for "[query]"", suggestions "Check the spelling or try a broader term", links to the six categories.

#### 2.8 Product page

From top to bottom on mobile; two columns on desktop (gallery 55–60%, purchase area 40–45%, sticky purchase area on desktop):

1. **Gallery:**
   - Square main image, swipeable on mobile with dots plus "1 / 5" text, thumbnails on desktop.
   - Zoom on tap or click.
   - **Alt text required** for every image.
2. **Title (H1)**, then **price** (and sale formatting as in 2.2). Show "Tax included." if the theme setting applies. *Sidekick: check tax display settings.*
3. **Variant selectors:**
   - Use buttons (pills) for 6 or fewer options, a dropdown for more.
   - Sold-out variants are crossed out and labelled "Sold out" in text.
4. **Quantity selector.**
5. **Primary button "Add to cart"** (full width on mobile). Show dynamic checkout buttons (Shop Pay, Apple Pay and others) only if the merchant wants them. They speed up checkout but add visual weight. *Merchant decision. Recommended: on.*
6. **Delivery and returns block:** a short, collapsible row showing **only merchant-verified text**, linking to the Shipping and Refund policy pages. If unverified, show only links: "Delivery information" and "Returns". **Do not invent timescales.**
7. **Description**, then collapsible sections: "Details and specifications", "Delivery", "Returns". Use product metafields if the theme supports them; otherwise the description only.
8. **Complementary / related products:** "You may also like", 4 products, from Search & Discovery product recommendations.
9. **Reviews:** leave out until a real review source exists.
10. **Sticky add-to-cart bar on mobile:** use only if the theme supports it natively. Otherwise leave it off.

#### 2.9 Cart

- **Cart drawer** (slide-in from the right, full screen on mobile) after Add to cart, so shoppers can keep browsing. The drawer contains:
  - product image, title, variant, quantity controls and a "Remove" text button;
  - line price;
  - subtotal;
  - the note **"Shipping and taxes calculated at checkout."** (or the theme's standard equivalent);
  - primary button **"Check out"**;
  - secondary text link "Continue shopping".
- **Free-shipping progress bar:** only if a free-shipping threshold is confirmed and set up in shipping settings.
- **Empty cart:** "Your cart is empty", button "Start shopping" → /collections/all.
- No upsell pop-ups and no cart timers.

### Dependencies and verification

**Sidekick must inspect:**
1. The current published theme: name, version, Online Store 2.0 or not.
2. Unpublished themes.
3. Installed apps and app embeds.
4. The current main menu and footer menu.
5. Collections and their product counts (to find empty categories).
6. Whether Search & Discovery is installed.
7. Product image ratios and missing images or alt text.
8. Policy pages that exist.
9. Tax display settings.
10. Active markets and currencies.

**Platform features to verify** (behaviour differs between themes and changes over time):
- The theme's colour scheme system, the font picker's list of fonts, and the custom CSS field and its limits.
- Sticky header, predictive search, quick add, cart drawer and sticky add-to-cart support.
- Search & Discovery: filters, synonyms, recommendations.
- Sidekick's own ability to edit theme settings, templates and menus. **If Sidekick can't make an edit, it should list the exact manual steps for the merchant instead.**

**Merchant decisions needed (blocking specific items only):**
- Confirmed delivery cost/timescale and returns window, for the announcement bar, brand promise band and product page delivery block.
- Whether a free-shipping threshold exists.
- Quick add on or off; dynamic checkout buttons on or off.
- Which category to feature on the homepage.
- Logo file (SVG preferred).
- Hero image, if any.

**External development (not needed for phases 1–4):** a fully custom header or mega-menu beyond what the theme supports; custom product-card layouts. Avoid these unless phase 4 measurement shows a clear need.

**Authoritative references** (Sidekick should confirm current behaviour):
- Shopify themes (free themes, Horizon/Dawn): https://themes.shopify.com/themes?price=free
- Theme editor and theme settings: https://help.shopify.com/en/manual/online-store/themes/customizing-themes
- Adding custom CSS: https://help.shopify.com/en/manual/online-store/themes/customizing-themes/edit/add-css
- Duplicating and previewing themes: https://help.shopify.com/en/manual/online-store/themes/managing-themes/duplicating-themes
- Shopify Search & Discovery app: https://help.shopify.com/en/manual/online-store/search-and-discovery
- Navigation menus: https://help.shopify.com/en/manual/online-store/menus-and-links
- Shopify GitHub integration: https://shopify.dev/docs/storefronts/themes/tools/github
- Theme Check (linting): https://shopify.dev/docs/storefronts/themes/tools/theme-check
- Shopify Sidekick: https://help.shopify.com/en/manual/shopify-admin/productivity-tools/sidekick
- WCAG 2.2 quick reference: https://www.w3.org/WAI/WCAG22/quickref/

### Phased implementation plan

All phases run on an **unpublished duplicate theme** named `Haukao redesign [date]`. The merchant previews each phase before moving on.

| Phase | Work | Mostly theme settings? | Custom work? |
|---|---|---|---|
| **0. Audit and safety** | Inspect theme, apps, menus, collections, imagery. Duplicate the live theme. Record current settings. Note baseline metrics (conversion rate, add-to-cart rate, search usage, mobile share) from Analytics. | Yes | No |
| **1. Global styles** | Colour schemes (2.1), fonts and scale (2.2), button/input/card radius, spacing, product card settings (square images, 2-line titles, Sale/Sold-out badges only). Custom CSS for focus ring and reduced motion. | Yes | Small CSS |
| **2. Header and search** | Header layout, always-visible mobile search, predictive search, main menu restructure (hide empty categories), announcement bar (only with verified text), Search & Discovery synonyms. | Yes, plus free Shopify app | Possibly CSS for the mobile search row |
| **3. Homepage** | Sections in the 2.6 order, hero gradient (CSS), category tiles, featured collections, verified brand promise band, newsletter, footer. | Yes | Hero gradient CSS |
| **4. Collection and search pages** | Filters, sorting, grid columns, paging, empty states, no-results page copy. | Yes | Possibly empty-state copy in template |
| **5. Product page** | Gallery, purchase area order, delivery/returns block, collapsible tabs, recommendations, alt text pass. | Yes | Metafields optional |
| **6. Cart** | Cart drawer, empty state, checkout button, optional verified free-shipping bar. | Yes | No |
| **7. QA and publish** | Run the acceptance checks below, merchant approval, publish, keep the old theme unpublished as a rollback. | — | — |

### Acceptance criteria

**Implementation checks (before publish):**
- [ ] All work is on an unpublished theme; the live theme is untouched until merchant approval.
- [ ] Colours match 2.1. Text contrast ≥4.5:1, UI parts and focus rings ≥3:1. Check with a contrast tool or Lighthouse.
- [ ] Only one font family and only weights 400 and 600 are loaded.
- [ ] Every product card uses a 1:1 image ratio. Titles truncate after 2 lines. Prices show in £ GBP format.
- [ ] Search is visible without tapping on mobile (375px wide) and desktop; predictive search returns products for a known product title.
- [ ] The main menu has no links to empty collections.
- [ ] Gradients appear only in the hero (and the optional brand band).
- [ ] No fake reviews, stock counts, countdowns, unverified delivery times or "best seller" labels anywhere.
- [ ] Empty collection, no-results search and empty cart all show the defined messages.
- [ ] Keyboard only: you can tab through header, search, menu, filters, product options, add to cart, cart drawer and checkout button, in a logical order, with a visible focus ring. The cart drawer and menu trap focus while open and close with Esc.
- [ ] Screen reader smoke test (VoiceOver iOS or NVDA): images have alt text, buttons have names, and the cart count is announced.
- [ ] With `prefers-reduced-motion` set, there is no animation beyond instant state changes.
- [ ] Mobile (375px and 390px widths): no horizontal scroll, tap targets ≥44px, body text ≥16px, add-to-cart visible without zooming.
- [ ] Lighthouse mobile on the homepage, a collection and a product page: Performance ≥ the baseline from Phase 0 (target ≥70), Accessibility ≥95, Best practices ≥90. Shopify's own theme speed report does not drop compared with baseline.
- [ ] Theme Check passes with no errors (if code was edited through GitHub).
- [ ] All existing app embeds still work. Add to cart → checkout works end to end with a test order (Bogus Gateway or test mode, or a real order that is then refunded).

**Business outcomes (measure 4–8 weeks after publish, against the Phase 0 baseline):**
- Conversion rate and add-to-cart rate (Shopify Analytics).
- Search usage and "searches with no results" (Search & Discovery reports). Add synonyms for the top no-result terms.
- Cart-to-checkout and checkout completion rates.
- Mobile bounce rate.
- Treat changes as directional. Low traffic will make small differences unreliable.

### Risks and recovery

| Risk | Likelihood | Recovery |
|---|---|---|
| Publishing a broken design | Medium | Never edit the live theme. Keep the previous theme unpublished; re-publish it to roll back in one click. |
| Changing a theme loses app blocks or custom code | Medium | Inventory apps and app embeds in Phase 0. Re-add each block in the new theme and test before publish. |
| Menu restructure breaks links | Low–Medium | Don't change collection or product handles. If any handle must change, create URL redirects (Online Store → Navigation → URL redirects). |
| Unverified claims published (delivery, returns) | Medium | Only publish text the merchant confirms. If wrong text goes live, edit the theme setting immediately. Wrong policy statements can have consumer-law consequences in the UK. |
| Custom CSS breaks on theme update | Low | Keep CSS small, scoped and documented in `docs/design/haukao-tokens.css`. Re-test after theme updates. |
| Performance falls (fonts, large hero images) | Low | One font family, two weights. Hero image ≤200 KB, served by Shopify's image CDN with responsive sizes. Compare with the Lighthouse baseline. |
| Deleting themes, apps, products or redirects | — | **Irreversible. Do not delete anything without explicit merchant approval.** |

### Instruction to Sidekick

"Inspect the relevant store state and verify platform support before acting. Treat this brief as a proposal, not proof of current store facts. Implement the supported parts requested by the merchant, preserve unrelated work, and clearly report anything blocked, substituted, or still requiring review. Do not claim testing or completion without evidence."

---

## 3. Theme route: refine vs replace

| Route | When to choose | Trade-offs |
|---|---|---|
| **A. Refine the existing theme** (recommended if it is a current Shopify free theme, OS 2.0) | Current theme is Horizon, Dawn or another recent Shopify theme | Fastest; keeps app blocks and settings; free updates. Limited by that theme's options. |
| **B. Install Horizon (or Dawn) fresh, unpublished** | Current theme is old (vintage, not OS 2.0), heavily hacked, or third-party and unmaintained | Clean base, best speed and accessibility, free. You must rebuild homepage sections and re-add app blocks. |
| C. Buy a premium theme | Only if A/B can't do a clearly needed feature (for example a complex mega-menu) after Phase 4 | ~£250–£400 one-off cost (check current prices). Not needed for this brief. |
| D. Fully custom theme | Not recommended now | Highest cost and maintenance. Not justified while the catalogue is still forming. |

---

## 4. Open questions for the merchant (none block Phases 0–4)

1. What delivery cost and timescale and what returns window can you guarantee today?
2. Is there a free-shipping threshold?
3. Do you have an SVG logo? If not, use a text wordmark "HAUKAO" in Inter 600 with letter-spacing 0.08em.
4. Which category should be featured on the homepage?
5. Do you want Shop Pay / Apple Pay express buttons on product pages?
