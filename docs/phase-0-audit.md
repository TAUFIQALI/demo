# Phase 0 audit: public storefront (2026-11-11)

Method: read-only requests to the public site (`https://www.haukao.com`, `/products.json`, `/collections.json`).
No admin, theme code, settings or analytics were accessed. Sidekick should confirm each point in the admin.

## Verified from the public site

| Area | Finding |
|---|---|
| Live theme | Name "Bright Marketplace", schema "Base" 1.0.0, not from the Theme Store (`theme_store_id: null`), theme slot `t/4`. It looks like a generated/custom theme with its own components (`s-cart`, `s-predictive-search`, `s-mobile-nav`, `view-transition`). |
| Fonts | DM Sans and Space Grotesk (two families). |
| Colours in use | `#CC4000` accent, `#141414` text, `#FCFCFA` / `#F0F2F0` backgrounds. Already close to the brief's palette. |
| Header | Logo, menu (Home, Catalog, Contact), search ("Search thousands of everyday finds"), cart. Predictive search component present. |
| Homepage | Category list → hero "Everything you need, one place" → two promo tiles → "Shop by category" → "Picked for you" (8 products) → brand band → three promise columns → closing band → footer with the four policy links. |
| **Products** | **`/products.json` returns 0 published products. `/collections.json` shows only `frontpage` with 0 products.** |
| **Homepage products** | The 8 "Picked for you" products (e.g. "4K Resolution Projector £399.99") **don't link to product pages**. They appear to be **theme placeholder/sample content, not real stock**. |
| Category links | All category tiles and menu category links go to `/collections` or `/collections/all`, not real category collections. |

## Problems this creates (fix before any styling work)

1. **Fake products with prices are shown to shoppers.** This breaks the "no fictional products" rule and could mislead customers. Remove or hide the "Picked for you" section until real products exist.
2. **Unverified claims in copy:**
   - "Thousands of everyday finds" (search placeholder and hero) — the store has 0 published products.
   - "Orders are packed and sent from our UK base" — depends on the unconfirmed fulfilment set-up.
   - "Pay safely with the methods you already use" — fine only once payments are set up.

   Replace with the brief's neutral copy until verified.
3. **Categories lead nowhere useful.** Create the six collections (empty is fine, hidden from navigation until stocked), or point tiles at `/collections/all` only.
4. **Two display fonts.** The brief recommends one family (Inter, or keep **DM Sans** alone, which also fits the brief). Dropping Space Grotesk saves a font download.

## Decision: theme route

The live theme is **custom, not Horizon/Dawn**. It is already light, orange-accented and marketplace-shaped, so **Route A (refine it) is still recommended**. Rebuilding on Horizon would throw away work that already matches the brief.

The catch: custom theme code is only editable through the admin code editor, or after connecting the theme to this repo. Sidekick may not be able to change the components.

## Blocking next step (merchant)

Connect the theme to this repo so code changes can be made and reviewed:

1. Admin → **Online Store → Themes**.
2. Find "Bright Marketplace" → **⋯ → Duplicate** (keep the live one untouched).
3. Connect the duplicate to GitHub: Add theme → **Connect from GitHub** → repo `taufiqali/demo`, new branch `theme-redesign`.

   If your admin offers no way to connect an existing theme, download the duplicate instead (⋯ → Download theme file) and add its contents to this repo.
4. Then Phase 1 (global styles) and the homepage clean-up can be implemented in code here.

Product and collection set-up (adding real products, creating the six collections) is merchant/Sidekick admin work, not theme code.
