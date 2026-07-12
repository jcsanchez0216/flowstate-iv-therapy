# Flowstate IV Therapy — Website Design

## Purpose

A single-file, mobile-first informational website for Flowstate IV Therapy, a
mobile IV hydration business in Albuquerque, NM run by Laticia Sanchez, BSN,
RN. Primary traffic source is the Instagram bio link, viewed on phones. The
site is informational only — no live payments, no interactive booking form.
Visitors book by calling, texting, or DMing Instagram, matching how the
business already operates.

## Branding source

Pulled directly from @flowstateivtherapy on Instagram (profile, grid posts,
and highlights: Process, Drips, Prices, Add-ons, RN, Where):

- **Logo**: circular badge — hand-lettered script "Flowstate," ring text "IV
  THERAPY," thin line-art IV bag icon, two water-droplet accents. Monochrome
  ink linework on cream.
- **Two visual modes observed**: feed posts (marketing graphics) use black
  backgrounds with white script/serif type; highlight covers (informational
  content — prices, credentials, service area) use cream/parchment
  backgrounds with dusty slate-blue accent icon circles. This site follows
  the highlight mode as its base, since it's built for the same
  purpose — communicating real information, not a social post.
- **Caption tone**: warm, educational, science-lite ("Did you know even mild
  dehydration can affect concentration..."), light emoji use, soft CTAs.

## Visual direction: "Cream & Ink"

- **Colors**: ink `#17171A` (hero, headlines), cream `#F4EFE4` (page base),
  dusty slate-blue `#7E97A3` (accent — icon circles, dividers, links), warm
  gray `#6B6660` (secondary text)
- **Type**: Playfair Display (serif headlines), a script face matching her
  hand-lettered logo for the "Flowstate" wordmark accent, Inter (sans) for
  body copy, labels, and prices. Loaded via Google Fonts `<link>`.
- **Icons**: thin line-art in dusty-blue-filled circles with ink strokes
  (droplet, IV bag, stethoscope, home, dumbbell), echoing her highlight-cover
  icon style.
- One full-bleed ink-black hero section provides brand punch and ties back
  to her feed aesthetic; the rest of the page stays cream for readability of
  pricing lists and body text on mobile.

## Technical approach

- Single self-contained `index.html`: inline `<style>`, minimal vanilla JS
  (mobile nav toggle, smooth-scroll to in-page anchors), fonts via Google
  Fonts CDN link. No build step, no framework, no backend.
- Deployable as a static file to any host (Netlify, GitHub Pages, cheap
  shared hosting) and linkable directly from the Instagram bio.
- Logo recreated as inline SVG (script wordmark + ring text + droplet + IV
  bag icon) rather than a raster image, so it stays crisp at any size with
  no image asset to manage.
- Hero and About photos are not yet available. Both use elegant CSS
  placeholder blocks (soft gradient + line-art watermark icon, sized to the
  final image's aspect ratio) with an HTML comment marking exactly where to
  swap in a real `<img>` tag later. No layout rework needed when photos
  arrive.
- Mobile-first CSS: single-column layouts, large tap targets for call/text
  buttons, breakpoints added upward for tablet/desktop rather than designed
  desktop-first.

## Sections

### 1. Hero
Full-bleed ink-black section. Inline-SVG logo mark, tagline "Mobile wellness
that fits your flow," subhead "Come to You — IV Hydration Therapy in
Albuquerque," primary CTA "Call to Book" (`tel:5052494350` link) and
secondary "Text to Book" (`sms:5052494350` link). Placeholder background
graphic behind the logo, ready to swap for a real photo.

### 2. Services & Pricing
Cream section, card grid. All prices include transportation and handling
fees (stated once, not repeated per card).

**Drips:**
| Drip | Price | Ingredients | Benefit |
|---|---|---|---|
| Dehydration | $130 | Magnesium, Calcium, Zinc, Vitamin B12 | Supports proper muscle and nerve function; reduces fatigue and low energy; aids electrolyte balance and immune/metabolic health |
| Athlete | $180 | Magnesium, Taurine, B-Complex, Vitamin B12, BCAA Blend | Supports muscle recovery, aids energy production, reduces fatigue; replenishes nutrients for endurance and performance |
| Immunity | $180 | Vitamin C, Zinc, Vitamin B12 | High-dose Vitamin C supports immune function/collagen; Zinc supports immune response and recovery; B12 for energy and metabolic support |
| Beauty | $180 | Vitamin C, Biotin, Vitamin B12, B-Complex | Biotin supports hair/skin/nails; Vitamin C supports collagen formation; B12 and B-Complex support energy and metabolism |
| Detox | $180 | Vitamin C, Zinc, Vitamin B12, B-Complex | Vitamin C helps protect cells from oxidative stress; Zinc for immune balance; B12/B-Complex support energy production and metabolism |
| Energy Boost | $150 | Vitamin B12, Taurine, Magnesium, B-Complex | B12 supports energy production and reduces fatigue; B-Complex assists metabolism and nervous system function; Taurine/Magnesium support cellular energy and nerve function |

**Add-on Upgrades:**
| Add-on | Price | Detail |
|---|---|---|
| Migraine/Headache | $40 | 30mg Toradol, 25mg Benadryl — support for migraine or headache discomfort |
| Nausea | $20 | 4mg Zofran, 20mg Pepcid — support for nausea and stomach discomfort |

**Premium Add-ons:**
| Add-on | Price | Detail |
|---|---|---|
| NAD+ | $100 (100mg, 1-hour infusion minimum) / $250 (250mg, 2.5-hour infusion minimum) | Supports cellular energy metabolism and overall wellness |
| Glutathione | $30 (200mg) / $40 (400mg) | Powerful antioxidant support to reduce oxidative stress, support detoxification |

### 3. About
Photo placeholder + bio, using Laticia's own highlight copy:

> "Hello!! I'm Laticia! I am a registered nurse born and raised in New
> Mexico. I graduated from UNM Nursing school in 2023. I am doing IV therapy
> based out of ABQ and looking to help you feel your best — safely and
> comfortably!"

Credential badge: **Laticia Sanchez, BSN, RN**.

### 4. Contact
- Tap-to-call button: `(505) 249-4350`
- "Come to You" service locations: Your Home, The Gym, Your Office, Hotel
  Stays, and More
- Service area: Albuquerque, NM
- Instagram link/handle (@flowstateivtherapy) as the DM-to-book channel
- No email displayed (per business owner's request)

### 5. Footer
Small disclaimer line: "IV therapy administered by a licensed RN. Not a
substitute for emergency medical care." Business name/logo mark repeated
small, Instagram link repeated.

## Explicitly out of scope

- No live booking form, no payment processing
- No email contact method
- No "How It Works" process section (not requested; can be added later)
- No real photography yet — placeholders only, swapped in a follow-up pass
- No CMS/backend — content changes require editing the HTML file directly
