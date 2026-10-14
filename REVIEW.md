# PureTalk Business — Website Review & Redesign Notes

Reviewed: https://puretalkbusiness.com/ (redirects to `/landing-page-702448`) on 2026-10-12.
Redesign: [index.html](index.html) — single static file, no build step.

## What the current page does well
- Clear price-led value prop ("without the big-carrier bill", lines from $15).
- Strong differentiators: veteran-led, 100% U.S. support, no contracts, dedicated account manager.
- Plan disclosures in the footer are thorough.

## Problems found

### Conversion
| # | Issue | Impact |
|---|---|---|
| 1 | **Hero lead form is clipped.** The HubSpot iframe renders 507px wide inside a narrower card, so the heading ("Get your free sa…"), the fields and the right edge are cut off at desktop widths. | High: the main conversion point looks broken. |
| 2 | **Hero headline breaks mid-word** at tablet/narrow-desktop widths ("team' / s", "wirel / ess"). | High: first impression looks unfinished. |
| 3 | **50% off first bill is buried** below the fold under the hero. This is the strongest offer on the page. | High |
| 4 | **The final CTA promises "Takes 30 seconds" but has no form**, just a large empty-looking video block with a small play button. | Medium–high: dead end at the bottom of the funnel. |
| 5 | **No phone number in the header**, and no click-to-call on mobile. Telecom B2B buyers call a lot. | Medium |
| 6 | No savings calculator. The page says "most teams cut their bill by half" but gives visitors nothing to check it with. | Medium |
| 7 | No social proof (testimonials, customer count, reviews, logos). | Medium |
| 8 | No FAQ to handle objections (network, contracts, data throttling, porting numbers). | Medium |
| 9 | No "how switching works" section. Switching cost is the #1 objection in telecom. | Medium |
| 10 | Plan cards have no recommended tier and no plan names, which makes them harder to compare. | Low–medium |

### SEO / technical
| # | Issue |
|---|---|
| 11 | **Empty `<title>`** and **no meta description**. Google gets no title and no snippet to show. |
| 12 | **Wrong H1.** The H1 is "Straight forward plans. Real savings." The real headline isn't a heading, while "$15.00" and "PER LINE, PER MONTH" are H2s. |
| 13 | Typo: "Straight forward" should be "Straightforward". |
| 14 | Images have empty `alt` text, including the logo. |
| 15 | No `og:title`, `og:description` or `og:image`, so shared links have no preview. |
| 16 | Homepage 302s to `/landing-page-702448`. The root domain should serve the canonical page. |
| 17 | 38 scripts and about 10 tracking iframes (Flashtalking, Trade Desk, DoubleClick, Bing, reCAPTCHA) slow the first paint. |
| 18 | The YouTube embed loads eagerly. |

## What the redesign does (and why)

**Above the fold:** promo bar with the 50% offer → sticky header with phone and CTA → H1 value prop, $15 price anchor, 4 trust checks → **short, fully visible lead form** (4 fields plus a one-tap line-count picker) with a "50% off" ribbon.

**Page flow (a standard telecom B2B funnel):**
1. Trust strip: veteran-led, 5G, no contracts, U.S. support
2. Plans: named tiers (Field / Pro / Data Only), "Most popular" on $30, first-month price shown with 50% off
3. **Interactive savings calculator** with a compliant "illustrative estimate" disclaimer
4. Comparison table against a typical big carrier, plus 6 benefit cards
5. "How switching works" in 3 steps
6. Video (lazy-loaded, privacy-enhanced) + testimonial slots
7. FAQ (also marked up as FAQPage schema for rich results)
8. Final CTA band → footer with full legal disclosures
9. **Sticky mobile bar** with Call and Get quote buttons

**Technical:** proper title and meta description, OG tags, one H1, Organization + Product/Offer + FAQPage JSON-LD, accessible labels, focus states and `aria-live` regions, reduced-motion support, no horizontal scroll at 375px, `data-track` attributes and `dataLayer` pushes (`generate_lead`, `select_plan`, `cta_click`) ready for GTM.

## Brand guideline alignment (PT Business Brand Guidelines, March 2021)
| Guideline | How the page applies it |
|---|---|
| **Logo:** horizontal 3-color is primary, white field preferred, min 1" wide, clear space, no recoloring or effects | `assets/ptb-logo-3color.svg`, converted straight from `PT-BUSINESS logo-HORZ-PMS-3color.ai` with no color changes. Used in the white header (≈150px wide) and the white footer, with padding for clear space. |
| **Typography:** Montserrat only | Montserrat 400–800 plus italic. Inter and Plus Jakarta Sans removed. |
| **Sentence case** for all copy | Removed every uppercase transform ("MOST POPULAR", eyebrows, ribbon). Headlines end with a period, as in the guideline examples. |
| **Superscript $** ("Plans start at ˢ20 a month") | Used for prices in the hero, plan circles, calculator, table and FAQ. |
| **Palette:** primary #2574BB, #75787B, #003A70, #3CB4E5; secondary #76BC43, #FF671D; neutrals #53565A, #C8C7C7, #FFF | All colors are CSS tokens taken from the palette. Off-palette yellow and dark navy removed. Body text is #53565A; section titles are #2574BB under a #75787B label, mirroring the guideline page headers. Only light tints of brand colors are added, for backgrounds. |
| **Business pattern** on navy | Hero, values panel, calculator result and final CTA use navy with the rounded-triangle pattern. Light sections use a faint version. |
| **Blue + green bottom stripe** | Added to the bottom of the footer. |
| **Website mock** (photo + navy "values" panel, "Inquiries." form, circular "Plan cost per line." prices) | Added the "Doing business with a company that shares your values." split section. Plan prices are now circular badges. |
| **Tagline** "Simply. Smarter. Wireless." | Added to the footer in blue / green / blue. |
| **Photography:** small-business people in business attire, light and airy | Photo slot in the values section, waiting for a licensed photo. |

**Contrast notes:**
- Green buttons use navy text (#003A70 on #76BC43, 4.9:1, passes AA).
- Orange #FF671D fails AA with white text (about 3:1), so it is used only as a non-text accent: the placeholder outlines and the form error border.

## Before launch: things to verify or replace
- [x] **Logo:** official 3-color horizontal logo is in place (`assets/ptb-logo-3color.svg`). The 2-color and white SVGs are also in `assets/` for dark backgrounds.
- [x] **Visual QA:** full-page check in headless Chromium at 1440, 820 and 390px. Fixed horizontal scroll on tablet/phone (hidden line-picker radios inherited `width:100%`) and the missing side gutter in the mobile footer. Re-check on real iOS/Android devices before launch.
- [ ] **Brand pattern:** `assets/pattern-*.svg` is redrawn to approximate the guideline pattern. Swap in the official pattern file if design has one.
- [ ] **Values photo:** add a licensed, on-brand photo at `assets/values.jpg` and uncomment the `<img>` in the values section.
- [ ] **HubSpot field names:** the form posts to portal `50596285` / form `76b117d4-…` (taken from the live embed). Confirm the internal names `company`, `firstname`, `email`, `phone`, `lines` match, or add the missing properties. Submission only fires on the production domain.
- [ ] **Testimonials:** the two quote cards are marked placeholders (dashed outline). Replace them with real, approved quotes.
- [ ] **Comparison table:** legal should review the "Typical big carrier" column ("Often 2–3× more", "Large accounts only", etc.). These are general claims and need substantiation.
- [ ] **Step 2 copy:** "We'll help you move your existing numbers over" assumes number porting and BYOD are supported. Confirm with ops.
- [ ] **FAQ:** "no termination fees" and "no surprise overage charges" are inferred from "no contracts" and the reduced-speed policy. Confirm both.
- [ ] Privacy policy and Terms links currently point to `#`.
- [ ] Add an `og:image` (1200×630).
- [ ] Re-add only the tracking pixels that are still in active use, through GTM.

## Suggested A/B tests
1. Form in hero vs. a two-step form ("How many lines?" first, then contact details).
2. Price-led headline vs. savings-led headline ("Cut your team's wireless bill in half").
3. Calculator placed directly under the hero vs. after the plans.
