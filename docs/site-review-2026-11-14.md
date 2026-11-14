# Haukao site review (2026-11-14)

Read-only review of the public site by three specialist passes: SEO; design and accessibility; UK compliance and trust. Not legal advice.

## Scores
| Area | Score |
|---|---|
| Overall | **5/10**: good foundation, not launch-ready |
| Visual design | 6 |
| Typography | 6 |
| Colour | 5 |
| Layout | 6 |
| Mobile UX | 5 |
| Accessibility | 6 |
| Navigation / search | 7 |
| SEO | 5 |
| UK compliance | 3 |
| Trust / conversion | 4 |

## Blockers before launch
1. **Fake "Deal of the day":** countdown, "Today only", and a was-price of £34.99 / -26% that was never charged. Remove it (DMCCA 2024, CMA pricing guidance).
2. **Placeholder products:** 18 are published, appear in the sitemap and show "Add to Basket". Set them to Draft until real stock exists. Hide "New this week" and the Deals collection.
3. **No trader identity:** legal name, geographic address, company number and VAT number are all missing. Add them to the footer and a Contact Information policy (CCR 2013, E-Commerce Regs 2002).
4. **Personal email address in the policies.** Use an email on the haukao.com domain.
5. **Policies are generic templates:** the refund policy needs UK 14-day cancellation and CRA 2015 rights; the terms contain US wording.
6. **Cookie banner:** not seen from a US test address. Turn on the UK banner with an equally easy "Reject all" option, write the cookie policy, and test from the UK.
7. **Unverified claims:** "Easy returns", "Free UK delivery over £50" (needs the matching shipping rule), "UK-based support", "Run from the UK", "Thousands of everyday finds".

## High
- Accent `#E5342A` with white text is 4.32:1 and fails AA. Use `#C2410C` (5.18:1), with `#9A3412` for hover.
- Search input has no visible focus. Skip link is broken (no `#MainContent` target).
- Homepage title is just "Haukao". `lang` should be en-GB. The same meta description appears on every page.
- `/pages/coming-soon` is indexable, and 7 footer links point to it.
- Electrical products need UKCA/CE marking, a UK importer's name and address, and safety documents before listing.

## Medium
- Visual direction is busy, warm and dark: purple/orange hero, maroon and brown blocks. It drifts from the calm, bright brief. Keep at most 6–7 homepage sections and one product rail.
- Guide cards have blank image areas. The desktop footer is a near-empty dark block.
- Mobile homepage is about 9,800px tall. The category bar is cut off, and the Help pill dominates the header.
- No breadcrumb schema. og:image is the logo. `/favicon.ico` returns 404. `/pages/about` returns 404.
- Collections (home-kitchen, tech-desk, travel-carry, garden-outdoor, wellness, gifts, deals) don't match the brief, and category links go to /collections/all. Any handle change needs merchant approval and 301 redirects.

## Strengths
- Prominent search and a clear desktop header.
- Good discovery modules: shop by budget, shop by room, category tiles.
- Stable layout (CLS ≈ 0), no mobile overflow, alt attributes on all images.
- Technical SEO basics: HTTPS/www redirects, canonical, sitemaps, Organization and WebSite JSON-LD, noindex on cart/search/404.

## Suggested homepage meta
- **Title:** Haukao | Gadgets, Home & Kitchen, Desk and Travel UK
- **Description:** Shop gadgets, home and kitchen essentials, desk accessories and travel gear at Haukao. Prices in GBP, with delivery across the UK.
