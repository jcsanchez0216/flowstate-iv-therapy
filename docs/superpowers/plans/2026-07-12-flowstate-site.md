# Flowstate IV Therapy Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single self-contained `index.html` marketing/informational site for Flowstate IV Therapy, matching the approved design spec.

**Architecture:** One static HTML file with inline `<style>` and no JavaScript (smooth-scroll is CSS-only via `scroll-behavior`; there is no nav menu to toggle, so the JS mentioned in the spec turns out to be unnecessary — the header is a persistent logo + call button rather than a hamburger menu). Google Fonts loaded via CDN `<link>`. Icons are inline SVG `<symbol>` definitions reused via `<use>`. No build step, no backend, no dependencies.

**Tech Stack:** Plain HTML5 + CSS3. Google Fonts (Playfair Display, Dancing Script, Inter).

## Global Constraints

- Single file: everything lives in `index.html` at the repo root — no separate `.css`/`.js` files.
- Mobile-first CSS: unprefixed rules target mobile; `@media (min-width: ...)` rules layer on tablet/desktop.
- Colors: ink `#17171A`, cream `#F4EFE4`, accent `#7E97A3`, accent-dark `#5F7986`, gray `#6B6660` — defined once as CSS custom properties in Task 1 and reused everywhere.
- Fonts: Playfair Display (serif, headings), Dancing Script (script, wordmark only), Inter (sans, everything else).
- Phone number everywhere: `(505) 249-4350` displayed, `tel:+15052494350` / `sms:+15052494350` as link targets.
- No email address anywhere on the page.
- No live booking form and no payment processing anywhere on the page.
- Two images are not yet available (hero background, About portrait). Each is a CSS-only placeholder block with an HTML comment directly above it stating the exact replacement markup for later.

---

### Task 1: Scaffold — head, design tokens, icon sprite, header, footer, empty section stubs

**Files:**
- Create: `index.html`

**Interfaces:**
- Produces CSS custom properties: `--ink`, `--cream`, `--accent`, `--accent-dark`, `--gray`, `--font-serif`, `--font-script`, `--font-sans`, `--radius`
- Produces CSS classes: `.container`, `.btn`, `.btn-sm`, `.btn-primary`, `.btn-outline`, `.btn-on-dark`, `.btn-outline-on-dark`, `.icon-circle`, `.eyebrow`
- Produces SVG symbol ids (in a hidden sprite at top of `<body>`): `icon-drop`, `icon-cross`, `icon-sparkle`
- Produces empty section stubs with ids `#hero`, `#services`, `#about`, `#contact` inside `<main>`, each to be filled by a later task
- Consumes: nothing (first task)

- [ ] **Step 1: Write `index.html` with the full page shell**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Flowstate IV Therapy | Mobile IV Hydration in Albuquerque, NM</title>
<meta name="description" content="Mobile IV hydration, vitamin, and NAD+ therapy in Albuquerque, NM. Licensed RN comes to your home, gym, office, or hotel. Call or text to book.">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ctext y='.9em' font-size='90'%3E%F0%9F%92%A7%3C/text%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@500;700&family=Inter:wght@400;500;600;700&family=Playfair+Display:wght@500;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #17171A;
    --cream: #F4EFE4;
    --accent: #7E97A3;
    --accent-dark: #5F7986;
    --gray: #6B6660;
    --font-serif: 'Playfair Display', serif;
    --font-script: 'Dancing Script', cursive;
    --font-sans: 'Inter', sans-serif;
    --radius: 14px;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body {
    font-family: var(--font-sans);
    color: var(--ink);
    background: var(--cream);
    line-height: 1.55;
    -webkit-font-smoothing: antialiased;
  }
  h1, h2, h3 { font-family: var(--font-serif); font-weight: 600; line-height: 1.2; }
  .container { width: 100%; padding: 0 24px; margin: 0 auto; }
  @media (min-width: 768px) { .container { max-width: 720px; } }
  @media (min-width: 1100px) { .container { max-width: 1040px; } }
  section { padding: 64px 0; }
  .eyebrow {
    font-size: 13px;
    letter-spacing: .12em;
    text-transform: uppercase;
    color: var(--accent-dark);
    font-weight: 600;
    margin-bottom: 10px;
  }
  .btn {
    display: inline-block;
    font-family: var(--font-sans);
    font-weight: 600;
    font-size: 15px;
    padding: 14px 28px;
    border-radius: 999px;
    text-decoration: none;
    text-align: center;
    transition: transform .15s ease;
  }
  .btn:active { transform: scale(.97); }
  .btn-sm { padding: 8px 18px; font-size: 13px; }
  .btn-primary { background: var(--ink); color: var(--cream); }
  .btn-outline { background: transparent; color: var(--ink); border: 1.5px solid var(--ink); }
  .btn-on-dark { background: var(--cream); color: var(--ink); }
  .btn-outline-on-dark { background: transparent; color: var(--cream); border: 1.5px solid var(--cream); }
  .icon-circle {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    background: var(--accent);
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 12px;
  }
  .icon-circle svg { width: 26px; height: 26px; fill: none; stroke: var(--ink); stroke-width: 1.6; stroke-linecap: round; stroke-linejoin: round; }
  .site-header {
    position: sticky;
    top: 0;
    z-index: 50;
    background: var(--cream);
    border-bottom: 1px solid rgba(23,23,26,.08);
  }
  .site-header-inner { display: flex; align-items: center; justify-content: space-between; padding: 14px 0; }
  .wordmark { font-family: var(--font-script); font-size: 28px; color: var(--ink); text-decoration: none; }
  .wordmark.small { font-size: 22px; }
  .site-footer { background: var(--ink); color: var(--cream); padding: 40px 0; }
  .footer-content { display: flex; flex-direction: column; align-items: center; gap: 14px; text-align: center; }
  .footer-content a { color: var(--cream); }
  .disclaimer { font-size: 12px; color: rgba(244,239,228,.65); max-width: 480px; }
</style>
</head>
<body>

<svg style="display:none">
  <symbol id="icon-drop" viewBox="0 0 24 24">
    <path d="M12 2C12 2 5 11 5 15.5C5 19.09 8.13 22 12 22C15.87 22 19 19.09 19 15.5C19 11 12 2 12 2Z"/>
  </symbol>
  <symbol id="icon-cross" viewBox="0 0 24 24">
    <path d="M12 2L20 5V11C20 16 16.5 20.5 12 22C7.5 20.5 4 16 4 11V5L12 2Z"/>
    <path d="M12 8V16M8 12H16"/>
  </symbol>
  <symbol id="icon-sparkle" viewBox="0 0 24 24">
    <path d="M12 2L13.8 9.2L21 11L13.8 12.8L12 20L10.2 12.8L3 11L10.2 9.2L12 2Z"/>
  </symbol>
</svg>

<header class="site-header">
  <div class="container site-header-inner">
    <a class="wordmark" href="#hero">Flowstate</a>
    <a class="btn btn-primary btn-sm" href="tel:+15052494350">Call</a>
  </div>
</header>

<main>
  <section id="hero"><!-- filled in Task 2 --></section>
  <section id="services"><!-- filled in Task 3 --></section>
  <section id="about"><!-- filled in Task 4 --></section>
  <section id="contact"><!-- filled in Task 5 --></section>
</main>

<footer class="site-footer">
  <div class="container footer-content">
    <span class="wordmark small">Flowstate</span>
    <p class="disclaimer">IV therapy administered by a licensed RN. Not a substitute for emergency medical care.</p>
    <a href="https://instagram.com/flowstateivtherapy" target="_blank" rel="noopener">@flowstateivtherapy</a>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Verify the file is well-formed and contains the expected scaffold pieces**

Run: `grep -c "icon-drop\|icon-cross\|icon-sparkle" ~/flowstate-iv-therapy/index.html`
Expected: `3` (one line per symbol id match; if your grep counts differently, confirm all three ids are present with `grep -o` instead)

Run: `grep -c "tel:+15052494350" ~/flowstate-iv-therapy/index.html`
Expected: `1` (the header Call button)

Run: `grep -c "id=\"hero\"\|id=\"services\"\|id=\"about\"\|id=\"contact\"" ~/flowstate-iv-therapy/index.html`
Expected: `4`

- [ ] **Step 3: Commit**

```bash
cd ~/flowstate-iv-therapy
git add index.html
git commit -m "Scaffold Flowstate site: head, design tokens, icon sprite, header, footer"
```

---

### Task 2: Hero section

**Files:**
- Modify: `index.html` — replace the contents of `<section id="hero">` (currently `<!-- filled in Task 2 -->`)

**Interfaces:**
- Consumes: `--ink`, `--cream` custom properties; `.container`, `.btn`, `.btn-on-dark`, `.btn-outline-on-dark`, `.eyebrow` classes from Task 1
- Produces: `.hero`, `.hero-bg`, `.hero-content`, `.hero-logo`, `.hero-tagline`, `.hero-sub`, `.cta-row` classes (used only within this section)

- [ ] **Step 1: Add hero CSS to the `<style>` block, just before `</style>`**

```css
  .hero {
    position: relative;
    background: var(--ink);
    color: var(--cream);
    padding: 88px 0 72px;
    overflow: hidden;
  }
  .hero-bg {
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at 50% 20%, #23262b 0%, #17171A 70%);
    z-index: 0;
  }
  .hero-content { position: relative; z-index: 1; text-align: center; }
  .hero-logo { width: 160px; height: 160px; margin: 0 auto 28px; }
  .hero-logo svg { width: 100%; height: 100%; }
  .hero .eyebrow { color: var(--accent); }
  .hero-tagline { font-size: 34px; margin-bottom: 16px; }
  @media (min-width: 768px) { .hero-tagline { font-size: 46px; } }
  .hero-sub {
    font-size: 16px;
    color: rgba(244,239,228,.85);
    max-width: 460px;
    margin: 0 auto 32px;
  }
  .cta-row { display: flex; flex-direction: column; gap: 14px; align-items: center; }
  @media (min-width: 480px) { .cta-row { flex-direction: row; justify-content: center; } }
```

- [ ] **Step 2: Replace the hero section markup**

```html
  <section id="hero">
    <!-- PLACEHOLDER: replace the .hero-bg div below with
         <img class="hero-bg" src="hero-photo.jpg" alt="Laticia administering mobile IV therapy in Albuquerque">
         once real hero photography is available. Keep .hero-content's z-index: 1 unchanged so text stays readable over the photo. -->
    <div class="hero-bg" aria-hidden="true"></div>
    <div class="container hero-content">
      <div class="hero-logo" aria-hidden="true">
        <svg viewBox="0 0 220 220">
          <circle cx="110" cy="110" r="104" fill="none" stroke="#F4EFE4" stroke-width="1.5"/>
          <path id="ringPath" d="M 14,110 A 96,96 0 0 1 206,110" fill="none"/>
          <text font-family="Inter, sans-serif" font-size="13" letter-spacing="4" fill="#F4EFE4">
            <textPath href="#ringPath" startOffset="50%" text-anchor="middle">IV THERAPY</textPath>
          </text>
          <text x="110" y="118" font-family="'Dancing Script', cursive" font-size="46" fill="#F4EFE4" text-anchor="middle">Flowstate</text>
          <path d="M40,150 C40,158 33,164 33,172 a7,7 0 0 0 14,0 C47,164 40,158 40,150 Z" fill="#7E97A3"/>
          <path d="M180,150 C180,158 173,164 173,172 a7,7 0 0 0 14,0 C187,164 180,158 180,150 Z" fill="#7E97A3"/>
        </svg>
      </div>
      <p class="eyebrow">Mobile IV Hydration Therapy &middot; Albuquerque, NM</p>
      <h1 class="hero-tagline">Mobile wellness that fits your flow.</h1>
      <p class="hero-sub">Come to You &mdash; IV hydration, vitamin, and NAD+ infusions delivered by a licensed RN, wherever you are.</p>
      <div class="cta-row">
        <a class="btn btn-on-dark" href="tel:+15052494350">Call to Book</a>
        <a class="btn btn-outline-on-dark" href="sms:+15052494350">Text to Book</a>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Verify hero content is present**

Run: `grep -c "Mobile wellness that fits your flow" ~/flowstate-iv-therapy/index.html`
Expected: `1`

Run: `grep -c "sms:+15052494350" ~/flowstate-iv-therapy/index.html`
Expected: `1`

Run: `grep -c "PLACEHOLDER: replace the .hero-bg div" ~/flowstate-iv-therapy/index.html`
Expected: `1`

- [ ] **Step 4: Commit**

```bash
cd ~/flowstate-iv-therapy
git add index.html
git commit -m "Add hero section with inline SVG logo"
```

---

### Task 3: Services & Pricing section

**Files:**
- Modify: `index.html` — replace the contents of `<section id="services">` (currently `<!-- filled in Task 3 -->`)

**Interfaces:**
- Consumes: `--accent`, `--accent-dark`, `--gray` custom properties; `.container`, `.eyebrow`, `.icon-circle` classes; `icon-drop`, `icon-cross`, `icon-sparkle` SVG symbols from Task 1
- Produces: `.drip-grid`, `.drip-card`, `.price`, `.ingredients`, `.benefit`, `.addon-grid`, `.addon-card`, `.premium-grid`, `.premium-card`, `.tier-list`, `.section-note` classes (used only within this section)

- [ ] **Step 1: Add services/pricing CSS to the `<style>` block, just before `</style>`**

```css
  .section-heading { text-align: center; max-width: 560px; margin: 0 auto 40px; }
  .section-note { color: var(--gray); font-size: 14px; margin-top: 8px; }
  .drip-grid, .addon-grid, .premium-grid { display: grid; grid-template-columns: 1fr; gap: 20px; }
  @media (min-width: 640px) { .drip-grid, .addon-grid { grid-template-columns: repeat(2, 1fr); } }
  @media (min-width: 1000px) { .drip-grid { grid-template-columns: repeat(3, 1fr); } }
  @media (min-width: 640px) { .premium-grid { grid-template-columns: repeat(2, 1fr); } }
  .drip-card, .addon-card, .premium-card {
    background: #fff;
    border: 1px solid rgba(23,23,26,.08);
    border-radius: var(--radius);
    padding: 24px;
  }
  .price { font-family: var(--font-serif); font-size: 22px; color: var(--accent-dark); margin: 4px 0 10px; }
  .ingredients {
    font-size: 12px;
    letter-spacing: .04em;
    text-transform: uppercase;
    color: var(--gray);
    margin-bottom: 10px;
  }
  .benefit { font-size: 14px; opacity: .85; }
  .subgroup-heading { margin: 56px 0 20px; text-align: center; font-size: 24px; }
  .tier-list { list-style: none; margin-top: 12px; }
  .tier-list li {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    padding: 8px 0;
    border-top: 1px solid rgba(23,23,26,.08);
    font-size: 14px;
  }
  .tier-list li:first-child { border-top: none; }
  .tier-list .tier-price { font-family: var(--font-serif); color: var(--accent-dark); }
  .tier-list small { display: block; width: 100%; color: var(--gray); font-size: 12px; margin-top: 2px; }
```

- [ ] **Step 2: Replace the services section markup**

```html
  <section id="services">
    <div class="container">
      <div class="section-heading">
        <p class="eyebrow">Services &amp; Pricing</p>
        <h2>IV Drip Menu</h2>
        <p class="section-note">All prices include transportation and handling fees.</p>
      </div>

      <div class="drip-grid">
        <article class="drip-card">
          <div class="icon-circle"><svg><use href="#icon-drop"/></svg></div>
          <h3>Dehydration Drip</h3>
          <p class="price">$130</p>
          <p class="ingredients">Magnesium &middot; Calcium &middot; Zinc &middot; Vitamin B12</p>
          <p class="benefit">Supports proper muscle and nerve function. Reduces fatigue and low energy. Aids electrolyte balance and supports immune and metabolic health.</p>
        </article>
        <article class="drip-card">
          <div class="icon-circle"><svg><use href="#icon-drop"/></svg></div>
          <h3>Athlete Drip</h3>
          <p class="price">$180</p>
          <p class="ingredients">Magnesium &middot; Taurine &middot; B-Complex &middot; Vitamin B12 &middot; BCAA Blend</p>
          <p class="benefit">Supports muscle recovery, aids energy production, and reduces feelings of fatigue. Helps replenish nutrients and supports endurance and performance.</p>
        </article>
        <article class="drip-card">
          <div class="icon-circle"><svg><use href="#icon-drop"/></svg></div>
          <h3>Immunity Drip</h3>
          <p class="price">$180</p>
          <p class="ingredients">Vitamin C &middot; Zinc &middot; Vitamin B12</p>
          <p class="benefit">High-dose Vitamin C supports immune function and collagen production. Zinc helps the immune response and recovery. B12 supports energy levels and metabolic support.</p>
        </article>
        <article class="drip-card">
          <div class="icon-circle"><svg><use href="#icon-drop"/></svg></div>
          <h3>Beauty Drip</h3>
          <p class="price">$180</p>
          <p class="ingredients">Vitamin C &middot; Biotin &middot; Vitamin B12 &middot; B-Complex</p>
          <p class="benefit">Biotin supports collagen formation and skin brightness. Vitamin C and B-complex support energy levels and metabolism.</p>
        </article>
        <article class="drip-card">
          <div class="icon-circle"><svg><use href="#icon-drop"/></svg></div>
          <h3>Detox Drip</h3>
          <p class="price">$180</p>
          <p class="ingredients">Vitamin C &middot; Zinc &middot; Vitamin B12 &middot; B-Complex</p>
          <p class="benefit">Vitamin C supports immune function and helps protect cells from oxidative stress. Zinc supports immune balance. B12 and B-complex support energy production, metabolism, and overall wellness.</p>
        </article>
        <article class="drip-card">
          <div class="icon-circle"><svg><use href="#icon-drop"/></svg></div>
          <h3>Energy Boost Drip</h3>
          <p class="price">$150</p>
          <p class="ingredients">Vitamin B12 &middot; Taurine &middot; Magnesium &middot; B-Complex</p>
          <p class="benefit">B12 helps support energy production and reduces feelings of fatigue. B-complex assists with metabolism and nervous system function. Taurine and magnesium support cellular energy and nerve function.</p>
        </article>
      </div>

      <h3 class="subgroup-heading">Add-on Upgrades</h3>
      <div class="addon-grid">
        <article class="addon-card">
          <div class="icon-circle"><svg><use href="#icon-cross"/></svg></div>
          <h3>Migraine / Headache</h3>
          <p class="price">$40</p>
          <p class="benefit">30mg Toradol &middot; 25mg Benadryl &mdash; support for migraine or headache discomfort.</p>
        </article>
        <article class="addon-card">
          <div class="icon-circle"><svg><use href="#icon-cross"/></svg></div>
          <h3>Nausea</h3>
          <p class="price">$20</p>
          <p class="benefit">4mg Zofran &middot; 20mg Pepcid &mdash; support for nausea and stomach discomfort.</p>
        </article>
      </div>

      <h3 class="subgroup-heading">Premium Add-ons</h3>
      <div class="premium-grid">
        <article class="premium-card">
          <div class="icon-circle"><svg><use href="#icon-sparkle"/></svg></div>
          <h3>NAD+</h3>
          <p class="benefit">Supports cellular energy metabolism and overall wellness.</p>
          <ul class="tier-list">
            <li>
              <span>100mg</span>
              <span class="tier-price">$100</span>
              <small>1-hour infusion minimum</small>
            </li>
            <li>
              <span>250mg</span>
              <span class="tier-price">$250</span>
              <small>2.5-hour infusion minimum</small>
            </li>
          </ul>
        </article>
        <article class="premium-card">
          <div class="icon-circle"><svg><use href="#icon-sparkle"/></svg></div>
          <h3>Glutathione</h3>
          <p class="benefit">Powerful antioxidant support to reduce oxidative stress and support detoxification.</p>
          <ul class="tier-list">
            <li>
              <span>200mg</span>
              <span class="tier-price">$30</span>
            </li>
            <li>
              <span>400mg</span>
              <span class="tier-price">$40</span>
            </li>
          </ul>
        </article>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Verify all six drips, both add-ons, and both premium items are present with correct prices**

Run: `grep -oE "Dehydration Drip|Athlete Drip|Immunity Drip|Beauty Drip|Detox Drip|Energy Boost Drip" ~/flowstate-iv-therapy/index.html | sort -u | wc -l`
Expected: `6`

Run: `grep -c "\\$130\|\\$180\|\\$150\|\\$40\|\\$20\|\\$100\|\\$250\|\\$30" ~/flowstate-iv-therapy/index.html`
Expected: `12` (six drip price lines — note `$180` is the price on four of those six: Athlete, Immunity, Beauty, Detox — plus two add-on price lines and four premium tier price lines. If this count looks off, manually confirm each of $130, $150, $180 (x4), $40 (x2: Migraine and Glutathione 400mg), $20, $100, $250, $30 appears rather than trusting the raw count)

Run: `grep -c "NAD+\|Glutathione" ~/flowstate-iv-therapy/index.html`
Expected: `2` or more (each appears once as a heading; fine either way as long as both are present)

- [ ] **Step 4: Commit**

```bash
cd ~/flowstate-iv-therapy
git add index.html
git commit -m "Add services and pricing section"
```

---

### Task 4: About section

**Files:**
- Modify: `index.html` — replace the contents of `<section id="about">` (currently `<!-- filled in Task 4 -->`)

**Interfaces:**
- Consumes: `--accent`, `--cream` custom properties; `.container`, `.eyebrow` classes from Task 1
- Produces: `.about-grid`, `.about-photo`, `.about-copy`, `.credential` classes (used only within this section)

- [ ] **Step 1: Add About CSS to the `<style>` block, just before `</style>`**

```css
  .about-grid { display: grid; grid-template-columns: 1fr; gap: 32px; align-items: center; }
  @media (min-width: 768px) { .about-grid { grid-template-columns: 280px 1fr; gap: 48px; } }
  .about-photo {
    aspect-ratio: 4 / 5;
    width: 100%;
    max-width: 320px;
    margin: 0 auto;
    border-radius: var(--radius);
    background: radial-gradient(circle at 50% 30%, #e4ddc9 0%, #d8cfb6 100%);
  }
  @media (min-width: 768px) { .about-photo { margin: 0; } }
  .about-copy h2 { font-size: 28px; margin-bottom: 16px; }
  .credential { font-family: var(--font-sans); font-size: 16px; font-weight: 600; color: var(--accent-dark); }
  .about-copy p.bio { font-size: 16px; }
```

- [ ] **Step 2: Replace the About section markup**

```html
  <section id="about">
    <div class="container about-grid">
      <!-- PLACEHOLDER: replace the .about-photo div below with
           <img class="about-photo" src="laticia-portrait.jpg" alt="Laticia Sanchez, BSN, RN, founder of Flowstate IV Therapy">
           once a real portrait photo is available. -->
      <div class="about-photo" aria-hidden="true"></div>
      <div class="about-copy">
        <p class="eyebrow">Meet Your Nurse</p>
        <h2>Laticia Sanchez, <span class="credential">BSN, RN</span></h2>
        <p class="bio">Hello!! I'm Laticia! I am a registered nurse born and raised in New Mexico. I graduated from UNM Nursing school in 2023. I am doing IV therapy based out of ABQ and looking to help you feel your best &mdash; safely and comfortably!</p>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Verify About content is present**

Run: `grep -c "Laticia Sanchez" ~/flowstate-iv-therapy/index.html`
Expected: `1`

Run: `grep -c "UNM Nursing school in 2023" ~/flowstate-iv-therapy/index.html`
Expected: `1`

Run: `grep -c "PLACEHOLDER: replace the .about-photo div" ~/flowstate-iv-therapy/index.html`
Expected: `1`

- [ ] **Step 4: Commit**

```bash
cd ~/flowstate-iv-therapy
git add index.html
git commit -m "Add About section with Laticia's bio"
```

---

### Task 5: Contact section

**Files:**
- Modify: `index.html` — replace the contents of `<section id="contact">` (currently `<!-- filled in Task 5 -->`)

**Interfaces:**
- Consumes: `--ink`, `--accent` custom properties; `.container`, `.eyebrow`, `.btn`, `.btn-primary`, `.btn-outline` classes from Task 1
- Produces: `.contact-section`, `.contact-actions`, `.locations-list` classes (used only within this section)

- [ ] **Step 1: Add Contact CSS to the `<style>` block, just before `</style>`**

```css
  .contact-section { background: #fff; }
  .contact-section .container { text-align: center; }
  .contact-intro { max-width: 480px; margin: 0 auto 28px; color: var(--gray); }
  .contact-actions { display: flex; flex-direction: column; gap: 14px; align-items: center; margin-bottom: 40px; }
  @media (min-width: 480px) { .contact-actions { flex-direction: row; justify-content: center; } }
  .locations-list {
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
    max-width: 480px;
    margin: 0 auto;
  }
  .locations-list li {
    background: var(--cream);
    border: 1px solid rgba(23,23,26,.1);
    border-radius: 999px;
    padding: 8px 18px;
    font-size: 14px;
  }
```

- [ ] **Step 2: Replace the Contact section markup**

```html
  <section id="contact" class="contact-section">
    <div class="container">
      <p class="eyebrow">Get In Touch</p>
      <h2>Come to You</h2>
      <p class="contact-intro">Mobile IV hydration therapy anywhere in the Albuquerque area. Call, text, or DM to book &mdash; no forms, no hassle.</p>
      <div class="contact-actions">
        <a class="btn btn-primary" href="tel:+15052494350">(505) 249-4350</a>
        <a class="btn btn-outline" href="https://instagram.com/flowstateivtherapy" target="_blank" rel="noopener">DM on Instagram</a>
      </div>
      <ul class="locations-list">
        <li>Your Home</li>
        <li>The Gym</li>
        <li>Your Office</li>
        <li>Hotel Stays</li>
        <li>And More</li>
      </ul>
    </div>
  </section>
```

- [ ] **Step 3: Verify Contact content is present**

Run: `grep -c "(505) 249-4350" ~/flowstate-iv-therapy/index.html`
Expected: `1`

Run: `grep -c "@" ~/flowstate-iv-therapy/index.html`
Expected: `2` (one line: the Google Fonts `<link>` href, which contains `wght@...` three times but counts as one matching line; one line: the footer's `@flowstateivtherapy` text). If the count is higher, run `grep -n "@" ~/flowstate-iv-therapy/index.html` and confirm no `mailto:` or email address was introduced anywhere else

Run: `grep -c "Your Home\|The Gym\|Your Office\|Hotel Stays" ~/flowstate-iv-therapy/index.html`
Expected: `4`

- [ ] **Step 4: Commit**

```bash
cd ~/flowstate-iv-therapy
git add index.html
git commit -m "Add Contact section"
```

---

### Task 6: Final QA pass

**Files:**
- Modify: `index.html` only if QA finds a defect (no planned changes otherwise)

**Interfaces:**
- Consumes: the complete page produced by Tasks 1–5
- Produces: nothing new — this task is verification-only

- [ ] **Step 1: Full-content grep audit against the spec**

Run each of these from `~/flowstate-iv-therapy`:

```bash
grep -c "mailto:" index.html                    # Expected: 0
grep -c "<form" index.html                       # Expected: 0
grep -c "tel:+15052494350" index.html             # Expected: 3 (header + hero + contact section)
grep -c "sms:+15052494350" index.html             # Expected: 1 (hero)
grep -c "not a substitute for emergency" index.html -i   # Expected: 1
grep -c "viewport" index.html                     # Expected: 1
```

All must match the expected values. If any don't, find and fix the discrepancy in `index.html` before proceeding.

- [ ] **Step 2: Visual check across breakpoints in a real browser**

Get a tab and navigate to the file, then screenshot at mobile, tablet, and desktop widths:

```
mcp__claude-in-chrome__tabs_context_mcp (createIfEmpty: true)
mcp__claude-in-chrome__navigate  → url: "file:///Users/jaredsanchez/flowstate-iv-therapy/index.html"
mcp__claude-in-chrome__resize_window → width: 390, height: 844   (mobile)
mcp__claude-in-chrome__computer → action: "screenshot"
mcp__claude-in-chrome__resize_window → width: 820, height: 1180  (tablet)
mcp__claude-in-chrome__computer → action: "screenshot"
mcp__claude-in-chrome__resize_window → width: 1440, height: 900  (desktop)
mcp__claude-in-chrome__computer → action: "screenshot"
```

Confirm at every width: the hero logo and text are centered and readable, all six drip cards + two add-on cards + two premium cards are visible without overlapping, the About section stacks (mobile) or sits side-by-side (tablet/desktop) without the photo placeholder squashing, and the Contact buttons are full tap-target size (not cramped) on mobile.

- [ ] **Step 3: Click every link and confirm the target**

In the same browser tab, click each of: the header "Call" button, the hero "Call to Book" and "Text to Book" buttons, the Contact section phone button, the Contact "DM on Instagram" button, and the footer Instagram link. Confirm the header/hero/contact phone buttons all show `tel:+15052494350` or `sms:+15052494350` as their href (use `mcp__claude-in-chrome__read_page` with `filter: "interactive"` to list all links and their hrefs in one pass rather than clicking each individually), and both Instagram links point to `https://instagram.com/flowstateivtherapy`.

- [ ] **Step 4: Fix any defects found, then commit**

If Steps 1–3 found no defects, skip straight to the commit. Otherwise fix the issue in `index.html` first.

```bash
cd ~/flowstate-iv-therapy
git add index.html
git commit -m "Final QA pass on Flowstate site" --allow-empty
```
