# DS Brand Guide — Website Implementation Reference

**Companion to:** `brand-guide.md` (master brand guide)
**Purpose:** HTML templates, Tailwind classes, CSS overrides, JS configuration, and deployment details for building DS web pages. Read the master brand guide first for brand context, then use this file for implementation.

**Gold Standard Reference:** `public/healthcare/index.html` — the SOLE authoritative reference for styling decisions.

**Critical Rule:** NEVER reference the WordPress production site (digitalscientists.com) for styling. The WP site uses different colors (#f1f2ea beige), typography, spacing, and component patterns. `healthcare/index.html` defines the standard.

---

## Table of Contents

1. [Page Architecture](#1-page-architecture)
2. [Tailwind Configuration](#2-tailwind-configuration)
3. [Section & Layout Patterns](#3-section--layout-patterns)
4. [Button System](#4-button-system)
5. [Card Patterns](#5-card-patterns)
6. [Component HTML Templates](#6-component-html-templates)
7. [Spacing Constants](#7-spacing-constants)
8. [Image Treatment Classes](#8-image-treatment-classes)
9. [Dark Section Implementation](#9-dark-section-implementation)
10. [Interactive Components](#10-interactive-components)
11. [Animation](#11-animation)
12. [Responsive Breakpoints](#12-responsive-breakpoints)
13. [Deployment & Path Conventions](#13-deployment--path-conventions)
14. [Case Study Page Patterns](#14-case-study-page-patterns)
15. [SEO Implementation](#15-seo-implementation)
16. [CSP & Security Headers](#16-csp--security-headers)

---

## 1. Page Architecture

### 1.1 Required Files

Every restyled page MUST include these files in the `<head>`:

```html
<script src="https://cdn.tailwindcss.com"></script>
<script>tailwind.config = { theme: { extend: { colors: {
    dsBlue: '#304FFF', dsBlack: '#050505', dsGray: '#F5F5F5',
    dsTeal: '#26D9C4', dsLime: '#D1F259',
}, fontFamily: {
    sans: ['Inter', 'system-ui', 'sans-serif'],
    mono: ['Roboto Mono', 'monospace'],
}}}}</script>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Roboto+Mono:wght@400;500&display=swap" rel="stylesheet">
<link rel="stylesheet" href="../ds-nav.css">
<link rel="stylesheet" href="../ds-wp-layout.css">
<script src="../ds-includes.js" defer></script>
```

And before `</body>`:
```html
<script src="../ds-wp-interactivity.js" defer></script>
```

Pages with carousels also need:
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css">
<script src="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js" defer></script>
```

Adjust `../` prefix per directory depth (e.g., `../../` for 2-deep, `../../../` for 3-deep).

### 1.2 HTML Structure (WP-Restyled Pages)

```html
<body class="bg-white text-dsBlack antialiased">
<div id="ds-nav-slot"></div>

<div class="wp-content-legacy pt-32">
  <div class="page-container page-container--outer">
    <div class="page-container page-container--content">
      <!-- guttenberg-block sections here -->
    </div>
  </div>
</div>

<div id="ds-footer-slot"></div>
<script src="../ds-wp-interactivity.js" defer></script>
</body>
```

### 1.3 CSS Override Chain

The outer `.page-container` wrappers have inline `max-width: 1200px` from the WP theme. `ds-wp-layout.css` Section 0 overrides these with `max-width: none !important` so section backgrounds extend edge-to-edge. Inner `__container` classes (Section 2) constrain content to `max-width: 1280px`.

### 1.4 Key CSS/JS Files

| File | Purpose | Lines |
|------|---------|-------|
| `ds-wp-layout.css` | Maps WP block classes to DS design system | ~2200 |
| `ds-nav.css` | Nav + footer styles | ~280 |
| `ds-includes.js` | Auto-loads nav/footer, detects base path | ~40 |
| `ds-wp-interactivity.js` | Swiper init, FAQ accordion, tab switching, alternating backgrounds | ~190 |

### 1.5 Two Page Paradigms

The site has two types of pages. Both use the same design system (colors, fonts, spacing, components) but differ in how sections are structured.

**WP-restyled pages** — Migrated from WordPress, wrapped in `.wp-content-legacy`:
- Sections use `.guttenberg-block` class with `data-bg` attributes
- Background alternation is handled by `ds-wp-interactivity.js` (automatic even/odd)
- Content containers use `.columns-content__container` or `.text-block__container`
- FAQ accordion uses `.faq-new__item` classes + JS event listeners
- Examples: `ai-machine-learning/`, `ux-design/`, most `blog/` posts

**Hand-crafted pages** — Written directly in Tailwind, no WP wrapper:
- Sections are bare `<section>` tags with explicit Tailwind classes (`py-20 px-6 bg-dsGray`)
- Background alternation is manual (author alternates `bg-white` / `bg-dsGray`)
- Content containers use `max-w-screen-xl mx-auto` directly
- FAQ accordion uses inline `onclick` handlers + CSS (see Section 6.16)
- Examples: `healthcare/index.html`, `services/blueprint/`, `healthcare/ai-agents/*`

**Which to use for new pages:** Always hand-crafted. The WP wrapper exists only for migrated content that hasn't been rewritten. When rewriting a WP-restyled page, strip the `.wp-content-legacy` wrapper and write direct Tailwind.

**How to tell which type a page is:** Check for `<div class="wp-content-legacy">` near the top. If present, it's WP-restyled. If the body starts with `<div id="ds-nav-slot">` followed by bare `<section>` tags, it's hand-crafted.

---

## 2. Tailwind Configuration

The full Tailwind config object (included inline in every page via `<script>`):

```js
tailwind.config = {
  theme: {
    extend: {
      colors: {
        dsBlue: '#304FFF',
        dsBlack: '#050505',
        dsGray: '#F5F5F5',
        dsTeal: '#26D9C4',
        dsLime: '#D1F259',
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['Roboto Mono', 'monospace'],
      }
    }
  }
}
```

See `brand-guide.md` Section 4 for the full color system rationale and usage rules.

### Typography Scale

| Element | Size | Weight | Other |
|---------|------|--------|-------|
| h1 | 3.5rem (56px) | 800 | Hero titles |
| h2 | 2.5rem (40px) | 700 | Section headings |
| h3 | 1.5rem (24px) | 600 | Subsection / card headings |
| h4 | 1.25rem (20px) | 600 | Card titles (alt) |
| h5 / label | 0.875rem (14px) | 600 | Section labels — dsBlue, uppercase, tracking 0.05em |
| body | 1.125rem (18px) | 400 | Paragraphs |
| small / caption | 0.875rem (14px) | 400 | Metadata, captions |

All headings: `letter-spacing: -0.02em`
Body text: `font-size: 1.125rem` (18px), `line-height: 1.6`

### Responsive Typography

| Element | Desktop | Mobile (< 768px) |
|---------|---------|-------------------|
| h1 | 3.5rem -> text-4xl md:text-5xl lg:text-6xl | 2.25rem |
| h2 | 2.5rem -> text-3xl md:text-4xl | 1.75rem |

---

## 3. Section & Layout Patterns

### 3.1 Background Alternation

**How it works:** `ds-wp-interactivity.js` runs on DOMContentLoaded and applies alternating white (#FFFFFF) / dsGray (#F5F5F5) backgrounds to all `.guttenberg-block` sections. Spacer blocks (`.spacer-new`) are excluded from the count so they don't disrupt the even/odd pattern.

**Sections that are SKIPPED** (their original background is preserved):

| `data-bg` Value | Rendered Color | Usage |
|-----------------|----------------|-------|
| `#333` / `#333333` | Dark (#333333) | Dark content sections |
| `#304fff` | dsBlue (#304FFF) | Blue CTA / feature sections |
| `#26d9c4` | dsTeal (#26D9C4) | Teal accent sections |
| `#d1f259` | dsLime (#D1F259) | Lime CTA banners |

**All other sections** (including `#ffffff` and `#f1f2ea`) receive alternating treatment.

**CSS provides fallback** alternation for pages where JS may not load, targeting `[data-bg="#f1f2ea"]` with nth-of-type rules.

### 3.2 Section Dimensions

- **Backgrounds:** Full viewport width (edge-to-edge)
- **Content:** `max-width: 1280px` (max-w-screen-xl), centered with `margin: 0 auto`
- **Vertical padding:** `padding: 5rem 0` (80px) per section
- **Horizontal padding:** `padding: 0 1.5rem` (24px) on inner containers
- **Spacer blocks:** `padding: 0` (height only, no visible spacing)

### 3.3 healthcare.html Section Pattern

In healthcare.html, each section is a direct child of `<body>` with explicit Tailwind backgrounds:

```html
<header class="pt-32 pb-16 px-6">             <!-- white (default) -->
<section class="bg-white border-t border-gray-100 py-12">  <!-- logo ribbon -->
<section class="py-20 px-6 bg-dsGray">         <!-- dsGray -->
<section class="py-20 px-6">                    <!-- white -->
<section class="py-20 px-6 bg-dsGray">         <!-- dsGray -->
...
```

Content is always constrained: `<div class="max-w-screen-xl mx-auto">`.

---

## 4. Button System

See `brand-guide.md` Section 6 for brand-level CTA tier definitions.

### 4.1 Three CTA Tiers

**Tier 1 — Primary Filled Button** (most prominent)
```
inline-flex items-center gap-2
bg-dsBlue text-white
px-6 py-3
text-sm font-medium (500)
rounded-full
hover:bg-dsBlack transition
Normal case (NOT uppercase)
Arrow: SVG icon (w-4 h-4) or -> character
```
Example from healthcare.html: "Discuss Your AI Opportunity ->"

**Tier 2 — Outline Button** (secondary)
```
inline-flex items-center gap-3
border-2 border-dsBlack text-dsBlack
px-6 py-3
rounded-full font-medium (500)
hover:bg-dsBlack hover:text-white transition-all
Text content is UPPERCASE
Arrow: SVG icon (w-5 h-5)
```
Example from healthcare.html: "VIEW CASE STUDY ->"

**Tier 3 — Text Link CTA** (tertiary / inline)
```
inline-flex items-center gap-2
text-dsBlue font-semibold (600) text-sm
uppercase tracking-wider
hover:gap-3 transition-all
Arrow: -> character or SVG
```
Example from healthcare.html: "View All ->"

### 4.2 WP Button Class Mapping

| WP Class | DS Pattern | Notes |
|----------|-----------|-------|
| `btn--main-blue` | Tier 1 (filled) | bg-dsBlue, normal case |
| `btn--main-blue-reverse` | Tier 2 (outline) | border-dsBlue instead of dsBlack |
| `btn--main-blue-arrow-white` | Tier 1 (filled) | Same as btn--main-blue, border: none |
| `btn--dark` | Tier 1 variant | bg-dsBlack, hover: bg-dsBlue |
| `btn--light` | Tier 1 variant | bg-white text-dsBlack, hover: bg-dsGray |
| `btn--outline` | Tier 2 (outline) | border-dsBlack |
| `btn--accent` | Tier 1 variant | bg-dsTeal text-dsBlack |
| `c-btn` | Tier 3 (text link) | text-dsBlue, -> arrow |
| `btn-light` | Tier 3 (text link) | Alias for text link pattern |

### 4.3 `.dec` Arrow Element

The WP theme uses `<span class="dec"></span>` inside buttons. In DS:

```css
.dec::before { content: '\2192'; font-size: 1rem; color: currentColor; }
```

The `.dec` element itself has NO visible styling (no width, height, or background). The arrow is rendered purely via the `::before` pseudo-element.

### 4.4 Base `.btn` Properties

```css
display: inline-flex;
align-items: center;
gap: 0.5rem;
padding: 0.75rem 1.5rem;
font-weight: 500;       /* NOT 600 */
font-size: 0.875rem;
border-radius: 9999px;  /* rounded-full */
text-decoration: none;
transition: all 0.2s ease;
cursor: pointer;
border: none;
/* NO text-transform */
/* NO letter-spacing */
```

### 4.5 Arrow Buttons

| Class | DS Pattern |
|-------|-----------|
| `arrow-btn--dark` | NOT used as dark circles. FAQ arrows: `background: none; color: #999; hover: color dsBlue` |
| `arrow-btn--light` | w-12 h-12 bg-white text-dsBlack rounded-full, centered arrow |
| `arrow-btn--main-blue` | Hidden (`display: none`) on product cards |

---

## 5. Card Patterns

### 5.1 Standard Card (stats, features)
```
border border-gray-200 rounded-xl (12px) p-6
hover: border-dsBlue shadow-sm
Equal height: display flex, flex-direction column
```

### 5.2 Image Card (case studies, blog)
```
bg-white rounded-xl (12px) overflow-hidden
border border-gray-200
Image: aspect-video (16/9) object-cover
       group-hover: scale-105 transition
Body: p-6
hover: border-dsBlue shadow-lg
```

### 5.3 Stat Card
```
border border-gray-200 rounded-xl p-6
Stat number: text-3xl md:text-4xl font-bold (dsBlack or dsBlue)
Label: text-gray-500 text-sm mt-1
```

### 5.4 Testimonial Card
```
border border-gray-200 rounded-xl p-8
Quote: text-gray-600 italic mb-6
Author row: flex items-center gap-4
Avatar: w-12 h-12 rounded-full object-cover
Name: font-semibold text-dsBlack
Title: text-gray-500 text-sm
```

### 5.5 Feature/Comparison Card
```
bg-white rounded-2xl (16px) p-8
border-2 border-gray-200
Used for side-by-side comparisons (Generic vs Custom)
```

### 5.6 Equal-Height Rule

Cards in grids MUST have equal heights. Apply to card wrappers:
```css
display: flex;
flex-direction: column;
```
Card inner content uses `flex: 1` to fill available space. CTA buttons use `margin-top: auto` to align at bottom.

### 5.7 Border Radius Rules

| Context | Radius | Tailwind |
|---------|--------|----------|
| Cards (standard, image, stat) | 12px | rounded-xl |
| Hero images, large feature images | 16px | rounded-2xl |
| Overlays, comparison cards | 16px | rounded-2xl |
| Buttons | 9999px | rounded-full |
| Avatars | 50% | rounded-full |
| Framework icons | 12px | rounded-xl |
| WP block images | 16px | rounded-2xl |

---

## 6. Component HTML Templates

This section contains the full HTML template and class reference for every DS web component. When creating a new page, read the "Best Example Page" from the reference table (Section 6.24) first, copy its structure, then modify content. Never build from memory alone.

### 6.1 Hero Headers

**WP Classes:** `landing-page-header`, `services-header`, `capabilities-header`, `industry-header`

**Live example:** `public/healthcare/index.html` lines 142-195

```html
<!-- Hero Section -->
<header class="pt-32 pb-16 px-6 bg-dsBlack">
    <div class="max-w-screen-xl mx-auto">
        <div class="grid lg:grid-cols-2 gap-12 items-center mb-12">
            <!-- Left Content -->
            <div>
                <div class="inline-flex items-center gap-2 text-sm text-dsBlue font-medium mb-6">
                    <span class="w-1.5 h-1.5 bg-dsBlue rounded-full"></span>
                    Healthcare & Life Sciences
                </div>

                <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-6 leading-[1.1]">
                    Healthcare software that reduces clinician burden and recovers lost revenue.
                </h1>

                <p class="text-xl text-gray-500 leading-relaxed mb-8">
                    Description text here. One or two paragraphs max.
                </p>

                <a href="#contact" class="inline-flex items-center gap-2 bg-dsBlue text-white px-6 py-3 text-sm font-medium rounded-full hover:bg-white hover:text-dsBlack transition">
                    CTA Text
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
                </a>
            </div>

            <!-- Right Image -->
            <div class="relative">
                <img src="../images/hero-healthcare.webp" alt="Healthcare AI Platform" class="rounded-2xl shadow-xl w-full">
            </div>
        </div>

        <!-- Optional: Stats Row (dark hero only) -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
            <div class="border border-gray-700 rounded-xl p-6">
                <span class="text-3xl md:text-4xl font-bold text-white">$10M+</span>
                <p class="text-gray-500 text-sm mt-1">PDPM Revenue Recovered</p>
            </div>
            <!-- repeat for each stat -->
        </div>
    </div>
</header>
```

**Key details:**
- Label uses dot indicator (`w-1.5 h-1.5 bg-dsBlue rounded-full`) not `<h5>`
- Dark heroes (`bg-dsBlack`): white text, `text-gray-500` descriptions, `border-gray-700` stat cards
- Light heroes (`bg-white`): `text-dsBlack` headings, `text-gray-600` descriptions
- Mobile: stacks vertically, image below text

### 6.2 Content + Image Sections

**WP Class:** `section-content`

**Image-right (text left, image right) — natural DOM order:**

Live example: `public/case-studies/custom-ehr-development/index.html` lines 278-330

```html
<section class="py-20 px-6 bg-white fade-up">
    <div class="max-w-screen-xl mx-auto">
        <div class="max-w-3xl mb-12">
            <span class="text-xs font-medium text-dsBlue uppercase tracking-wider">Section Label</span>
            <h2 class="text-3xl md:text-4xl font-bold text-dsBlack mt-3 mb-6">
                Section heading here
            </h2>
        </div>
        <div class="grid lg:grid-cols-2 gap-12 items-start">
            <!-- Text column (left) -->
            <div>
                <p class="text-gray-600 mb-6">Body text here.</p>
            </div>
            <!-- Image column (right) -->
            <div>
                <div class="rounded-xl overflow-hidden bg-white border border-gray-200">
                    <img loading="lazy" src="path/to/image.webp" alt="Description" class="w-full h-auto">
                </div>
            </div>
        </div>
    </div>
</section>
```

**Image-left (image left, text right) — two techniques:**

Technique 1: DOM order (image div first). Used when mobile order should be image-first.
```html
<div class="grid lg:grid-cols-2 gap-12 items-start">
    <div><!-- Image first in DOM = left on desktop --></div>
    <div><!-- Text second in DOM = right on desktop --></div>
</div>
```

Technique 2: `lg:order-*` classes. Used when mobile order should be text-first but desktop should be image-left. Live example: `public/case-studies/guardian-app/index.html` lines 203-214
```html
<div class="grid lg:grid-cols-2 gap-12 items-start">
    <div class="lg:order-2"><!-- Text: first on mobile, right on desktop --></div>
    <div class="lg:order-1"><!-- Image: second on mobile, left on desktop --></div>
</div>
```

**Mobile:** Always stacks vertically. Choose the technique based on desired mobile stacking order.

### 6.3 Client Logo Ribbon

**Standard across all pages:**

```
Section: bg-white border-t border-gray-100 py-12
Container: max-w-screen-xl mx-auto px-6
Layout: flex flex-wrap justify-center items-center
No label (no "clients we serve" text)
Each logo wrapper: px-6 md:px-8 py-4, border-r border-gray-200 (except last)
Logo images: grayscale(100%), object-contain, per-logo max-w-[...] and responsive h-
No opacity reduction (always 1.0)
```

**Why white background:** Provides highest contrast for grayscale logos and prevents white-cutout artifacts around transparent PNGs that appear on gray backgrounds.

**Logo Content Rule:** Each page's logo ribbon MUST show the same logos as the corresponding production page on digitalscientists.com. Do NOT substitute generic logos. Download logo images from WP if they're missing locally.

**Image Quality Rules:**
- Prefer SVG logos (infinite resolution)
- For raster logos, verify native pixel height >= display height (2.5rem = 40px)
- If native height < 40px, cap the display height to avoid upscale blur (e.g., HD Supply at 18px native -> height: 1.125rem)
- All logos: `object-contain` with per-logo `max-w-[...]` to prevent stretching
- NO `opacity` reduction — use only `grayscale(100%)`

**WP Block Variants (handled via ds-wp-layout.css):**
- `client-logos-new` with `.swiper .swiper-wrapper`: CSS overrides Swiper's `width: 100%` on slides with `width: auto !important; flex: 0 0 auto`
- `client-logos-new` with `.grid.centered`: CSS overrides grid with `display: flex`
- `client-logos` (older block): Simpler flex layout, same ribbon pattern
- `logos-and-list`: Logo row + optional text list below
- All variants: grayscale enforced via CSS, no opacity

### 6.4 Case Study Cards / Featured CS

**WP Class:** `featured-cs`

```
Header: label + title + optional CTA (left-aligned)
Cards: Swiper carousel (js-fcs-slider)
Card (cs-card):
  rounded-xl overflow-hidden border border-gray-200
  Image: aspect-video object-cover
  Body: p-6
    - Category tags: text-sm text-gray-500
    - Title: h3 font-bold
    - Description: text-gray-600
    - CTA: Tier 3 text link (margin-top: auto)
  Hover: shadow-lg border-dsBlue
```

### 6.5 Case Study Lists

**WP Class:** `case-study-lists`

```
Grid: grid md:grid-cols-2 lg:grid-cols-3 gap-6
Cards: same pattern as cs-card above
Equal heights enforced via flexbox
```

### 6.6 Capabilities / Feature Grid

**WP Class:** `capabilities`

```
Grid: grid md:grid-cols-2 lg:grid-cols-3 gap-6
Card: bg-white rounded-xl p-6 border border-gray-200
  Icon: 48px mb-4 (wp-theme SVG icons)
  Title: h3 font-bold mb-2
  Description: text-gray-500 text-sm
  Hover: border-dsBlue shadow-sm
```

### 6.7 Horizontal Boxes

**WP Class:** `horizontal-boxes`

```
Grid: grid md:grid-cols-3 lg:grid-cols-5 gap-6 (modifier: "five")
Card: bg-white rounded-xl p-6 border border-gray-200
  Icon: centered 48px
  Title: h3 centered
  Text: text-sm gray-500
  Arrow buttons: hidden (display: none)
  Hover: border-dsBlue shadow-sm
```

### 6.8 Three-Column Cards with Logos

**WP Class:** `three-cols-cards-with-logos`

```
Grid: grid md:grid-cols-2 lg:grid-cols-3 gap-6
Card: border border-gray-200 rounded-xl overflow-hidden
  Image: aspect-video (16/9) object-cover
  Body: p-6
  Logo: max-height 2rem
  Arrow buttons: hidden (display: none)
  Equal heights via flexbox
  Hover: border-dsBlue shadow-sm
```

### 6.9 C13 List (Image Cards)

**WP Class:** `c13-list`

```
Grid: grid md:grid-cols-2 lg:grid-cols-3 gap-6
Card: border border-gray-200 rounded-xl overflow-hidden
  Image: aspect-video (16/9) object-cover
  Body: p-6
  Equal heights via flexbox
  Hover: border-dsBlue shadow-sm
```

### 6.10 Plans / Pricing Cards

**WP Class:** `plans`

```
Container: max-width 1280px
Plans grid: depends on card count
Card (plans-info__item):
  rounded-xl border border-gray-200 p-6
  Title: h3 font-bold
  Feature list: text-sm
  CTA: Tier 1 or 2 button
```

### 6.11 Cards 1-3 Width

**WP Class:** `cards-1-3-width`

```
Grid: grid md:grid-cols-3 gap-6
Card: rounded-xl border border-gray-200 p-6
  Icon/number: styled per context
  Title: h3
  Description: text-sm text-gray-600
```

### 6.12 Process Line / Timeline

**WP Class:** `process-line`

```
Container: max-w-screen-xl
Title + description above
Steps: grid md:grid-cols-4 gap-6
Each step:
  Number circle: w-12 h-12 bg-dsBlue text-white rounded-full
  Title: h3 font-bold
  Description: text-gray-600
```

### 6.13 Framework Lists

**WP Classes:** `framework-half-width`, `framework-1-2-width`, `framework-full-width`

```
Grid: grid md:grid-cols-2 gap-8
Each item: flex gap-4
  Icon: w-12 h-12 bg-dsGray rounded-xl flex items-center justify-center
  Body: h3 title + p description + optional CTA
```

### 6.14 Testimonial Quote (single)

**WP Class:** `featured-testimonial-quote`

```
Container: max-w-3xl mx-auto text-center
Quote: text-xl italic text-gray-600 leading-relaxed
Attribution: mt-6 flex items-center gap-4 (centered)
  Avatar: w-12 h-12 rounded-full
  Name: font-semibold
  Title: text-gray-500 text-sm
```

### 6.15 Testimonial Carousel

**WP Class:** `client-quotes-carousel` (cqc-swiper)

```
Swiper: slidesPerView 1, autoplay 6s, loop true
Card: border border-gray-200 rounded-xl p-8
  Quote: text-gray-600 italic
  Author: flex items-center gap-4
Pagination: clickable dots
Nav: prev/next buttons
```

### 6.16 FAQ Accordion

**WP Class:** `faq-new` (WP-migrated pages use `ds-wp-interactivity.js`)
**Hand-crafted pages** use inline onclick + CSS (no JS file required).

**Live example (hand-crafted):** `public/healthcare/index.html` lines 1245-1325

```html
<section class="py-20 px-6 bg-dsGray">
    <div class="max-w-screen-xl mx-auto">
        <div class="max-w-3xl mx-auto">
            <div class="text-center mb-12 fade-up">
                <span class="text-xs font-medium text-dsBlue uppercase tracking-wider font-mono">FAQ</span>
                <h2 class="text-3xl md:text-4xl font-bold text-dsBlack mt-3 mb-4">Frequently Asked Questions</h2>
                <p class="text-gray-600">Subtitle text here.</p>
            </div>

            <div class="space-y-4 fade-up" id="faq-accordion">
                <div class="border border-gray-200 rounded-xl overflow-hidden">
                    <button class="w-full flex items-center justify-between px-6 py-5 text-left hover:bg-gray-50 transition" onclick="this.parentElement.classList.toggle('faq-open')">
                        <span class="font-semibold text-dsBlack pr-4">Question text here?</span>
                        <svg class="w-5 h-5 text-gray-500 flex-shrink-0 faq-icon transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/></svg>
                    </button>
                    <div class="faq-body px-6 pb-5 hidden">
                        <p class="text-gray-600 leading-relaxed">Answer text here.</p>
                    </div>
                </div>
                <!-- repeat for each Q&A -->
            </div>
        </div>
    </div>
</section>

<style>
    .faq-open .faq-icon { transform: rotate(180deg); }
    .faq-open .faq-body { display: block !important; }
</style>
```

**Key mechanics:**
- Toggle: `onclick="this.parentElement.classList.toggle('faq-open')"`
- Chevron rotates via `.faq-open .faq-icon { transform: rotate(180deg); }`
- Answer shows via `.faq-open .faq-body { display: block !important; }` overriding `hidden`
- Arrow is a minimal gray chevron — NO dark circle background, NO number prefix on hand-crafted pages

**WP-migrated FAQ** (`faq-new` class) uses different mechanics:
- `ds-wp-interactivity.js` handles toggle via `max-height` animation (0.35s ease)
- Number prefix: `text-dsBlue font-bold text-lg`
- Border: `border-top 1px solid gray-200` between items

### 6.17 Services List / Tabbed Accordion

**WP Class:** `services-overview` containing `services-list`

```
Section: typically dark (#333) with white text
Layout (desktop): flex, nav 35% + body 65%
Layout (mobile): stacked accordion

Nav tabs: count number + title (h2)
  Active: color white
  Inactive: color #CBCBCB
  Borders: border-top 1px solid #4d4d4d

Content panels: only isActive visible
  Icon (80px) + description + feature cards grid
  Feature cards: border 1px solid #4d4d4d, rounded-xl p-6
    Hover: border-dsBlue

JS required: ds-wp-interactivity.js handles tab switching
```

### 6.18 Condensed Content / Tabs

**WP Class:** `condensed-content`

```
Layout: grid lg:grid-cols-3 (nav 1col, content 2col)
Nav: border-l-2 border-gray-200, active: border-dsBlue
Content: p-8, title + description + optional button
```

### 6.19 CTA Banners

**WP Class:** `featured-cta`

```
Section: py-20 px-6, background from data-bg
Container: max-w-screen-xl mx-auto text-center
Title: text-3xl font-bold
Button: centered below, mt-8
```

**Hand-crafted HTML template** (from `services/blueprint/index.html`):

```html
<!-- CTA Banner — Blue background with inverted button -->
<section class="py-20 px-6 bg-dsBlue">
    <div class="max-w-screen-xl mx-auto text-center fade-up">
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-4">Ready to define what to build?</h2>
        <p class="text-blue-100 text-lg mb-8 max-w-2xl mx-auto">30 minutes. No pitch. We'll help you determine
            if a Blueprint is the right starting point&mdash;or recommend a
            <a href="../diagnostic/" class="text-white font-semibold underline hover:no-underline">Diagnostic</a>
            to identify the opportunity first.</p>
        <a href="../../start/" class="inline-flex items-center gap-2 bg-white text-dsBlue px-8 py-4 rounded-full font-medium hover:bg-dsBlack hover:text-white transition text-lg">
            Start a Blueprint &rarr;
        </a>
    </div>
</section>
```

**CTA color variants:**

| Background | Text | Button | Inline Links |
|------------|------|--------|-------------|
| `bg-dsBlue` | `text-white` / `text-blue-100` | `bg-white text-dsBlue hover:bg-dsBlack hover:text-white` | `text-white underline hover:no-underline` |
| `bg-[#333333]` | `text-white` / `text-gray-300` | `bg-white text-dsBlack hover:bg-dsBlue hover:text-white` | `text-white underline` |
| `bg-dsTeal` | `text-dsBlack` | `bg-dsBlack text-white hover:bg-dsBlue` | `text-dsBlack underline` |
| `bg-dsLime` | `text-dsBlack` | `bg-dsBlack text-white hover:bg-dsBlue` | `text-dsBlack underline` |

**Simple CTA (no body text):**
```html
<section class="py-20 px-6 bg-dsBlue">
    <div class="max-w-screen-xl mx-auto text-center fade-up">
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-8">Let's talk about your challenge</h2>
        <a href="../../start/" class="inline-flex items-center gap-2 bg-white text-dsBlue px-8 py-4 rounded-full font-medium hover:bg-dsBlack hover:text-white transition text-lg">
            Start a Conversation &rarr;
        </a>
    </div>
</section>
```

### 6.20 Next Page Navigation

**WP Class:** `next-page`

```
Section: bg-dsBlue text-white py-20 px-6
Container: max-w-screen-xl mx-auto flex justify-between items-center
Title: text-3xl font-bold text-white
Arrow: white circle button
```

**Hand-crafted "What's Next" pattern** (from `healthcare/ai-agents/intelligent-scheduling/index.html`):

The modern pattern replaces the WP single-link nav with a 3-card grid pointing to related pages. Each card has a colored label indicating value type.

```html
<!-- What's Next — Related pages navigation -->
<section class="py-20 px-6">
    <div class="max-w-screen-xl mx-auto">
        <div class="fade-up max-w-2xl mb-12">
            <span class="text-xs font-medium text-dsBlue uppercase tracking-wider">What's Next</span>
            <h2 class="text-3xl md:text-4xl font-bold text-dsBlack mt-3">
                After scheduling, where do you go?
            </h2>
        </div>

        <div class="grid md:grid-cols-3 gap-6">
            <a href="../documentation-automation/" class="group border border-gray-200 rounded-xl p-6 hover:border-dsBlue transition">
                <span class="text-xs text-green-600 font-medium uppercase tracking-wider">Fastest Payback</span>
                <h3 class="font-bold text-dsBlack mt-2 mb-2 group-hover:text-dsBlue transition">AI Documentation Automation</h3>
                <p class="text-gray-500 text-sm">Now that you have more visits, reduce documentation burden. 45->5 min per visit.</p>
            </a>

            <a href="../back-office-agents/" class="group border border-gray-200 rounded-xl p-6 hover:border-dsBlue transition">
                <span class="text-xs text-dsBlue font-medium uppercase tracking-wider">Highest ROI</span>
                <h3 class="font-bold text-dsBlack mt-2 mb-2 group-hover:text-dsBlue transition">Intelligent Back-Office Agents</h3>
                <p class="text-gray-500 text-sm">Scheduling proven? Apply AI to revenue cycle. 200-300 bps EBITDA improvement.</p>
            </a>

            <a href="../virtual-care-assistants/" class="group border border-gray-200 rounded-xl p-6 hover:border-dsBlue transition">
                <span class="text-xs text-purple-600 font-medium uppercase tracking-wider">Proven at Scale</span>
                <h3 class="font-bold text-dsBlack mt-2 mb-2 group-hover:text-dsBlue transition">Virtual Care Assistants</h3>
                <p class="text-gray-500 text-sm">Extend clinical capacity without more headcount. 3x patients per nurse.</p>
            </a>
        </div>
    </div>
</section>
```

**Label color conventions for navigation cards:**

| Label | Color | When to use |
|-------|-------|------------|
| Fastest Payback | `text-green-600` | Quick-win, low-effort recommendation |
| Highest ROI | `text-dsBlue` | Revenue/savings-focused recommendation |
| Proven at Scale | `text-purple-600` | Mature solution with validated results |
| Most Popular | `text-amber-600` | Highest traffic/engagement recommendation |

**Rules:**
- Always use `<a>` wrapping the entire card (not a button inside a card)
- `group` class on card + `group-hover:text-dsBlue` on title creates linked hover
- Labels are optional — use when cards need differentiation beyond title
- Paths must be relative (depth-appropriate `../` prefixes)

### 6.21 Benefits & Images

**WP Class:** `benefits-and-images`

```
Layout: grid lg:grid-cols-2 gap-12
Left: two stacked images, rounded-2xl, gap-6
Right: numbered items (01, 02, 03...)
  Each: border-top border-gray-200 pt-6
  Number: text-dsBlue font-bold
  Title: h3 font-bold
  Description: text-gray-600
```

**Hand-crafted icon-card grid** (from `services/blueprint/index.html` — "What You Get"):

```html
<section class="py-20 px-6">
    <div class="max-w-screen-xl mx-auto">
        <div class="max-w-3xl mb-12 fade-up">
            <span class="text-xs font-medium text-dsBlue uppercase tracking-wider">What You Get</span>
            <h2 class="text-3xl md:text-4xl font-bold text-dsBlack mt-3 mb-4">Five deliverables. A complete product plan.</h2>
            <p class="text-gray-600">Everything an engineering team needs to start building with confidence.</p>
        </div>
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6 fade-up">
            <div class="border border-gray-200 rounded-xl p-6 hover:border-dsBlue hover:shadow-sm transition flex flex-col">
                <div class="w-12 h-12 bg-dsBlue text-white rounded-xl flex items-center justify-center mb-4">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>
                    </svg>
                </div>
                <h3 class="font-bold text-dsBlack mb-2">Card Title</h3>
                <p class="text-gray-500 text-sm flex-1">Card description. The flex-1 class pushes all
                    cards to equal height regardless of content length.</p>
            </div>
            <!-- repeat for each card -->
        </div>
    </div>
</section>
```

**Grid column counts:** Use `md:grid-cols-2 lg:grid-cols-3` for 3+ items, `md:grid-cols-2` for exactly 4, `md:grid-cols-3` for exactly 3. Never exceed 3 columns for card-with-text layouts.

### 6.22 Dividers

**WP Class:** `divider`

```
max-width: 1280px, mx-auto
height: 1px (NOT WP 2px)
Light sections: #e5e7eb (gray-200)
Dark sections: #4d4d4d (preserve inline)
```

### 6.23 Process Timeline

A horizontal numbered-phase pattern used on service pages. Each phase gets a numbered circle badge connected by a horizontal line.

**Hand-crafted template** (from `services/blueprint/index.html` — "How It Works"):

```html
<section class="py-20 px-6 bg-dsGray">
    <div class="max-w-screen-xl mx-auto">
        <div class="text-center max-w-3xl mx-auto mb-16 fade-up">
            <span class="text-xs font-medium text-dsBlue uppercase tracking-wider">How It Works</span>
            <h2 class="text-3xl md:text-4xl font-bold text-dsBlack mt-3 mb-4">Four phases. Eight weeks. A complete plan.</h2>
            <p class="text-gray-600">Each phase builds on the last, with regular checkpoints.</p>
        </div>
        <div class="relative fade-up">
            <!-- Horizontal connector line (hidden on mobile) -->
            <div class="hidden md:block absolute top-8 left-[12.5%] right-[12.5%] h-0.5 bg-dsBlue/20"></div>
            <div class="grid md:grid-cols-4 gap-8">
                <div class="text-center relative">
                    <div class="w-16 h-16 bg-dsBlue text-white rounded-full flex items-center justify-center mx-auto mb-4 text-sm font-bold font-mono relative z-10">1-2</div>
                    <h3 class="text-lg font-bold text-dsBlack mb-2">Research &amp; Discovery</h3>
                    <p class="text-dsBlue font-semibold text-sm mb-2">Weeks 1&ndash;2</p>
                    <p class="text-gray-500 text-sm">User interviews, stakeholder workshops, competitive analysis.</p>
                </div>
                <!-- repeat for each phase -->
            </div>
        </div>
    </div>
</section>
```

**Key elements:**
- Circle badge: `w-16 h-16 bg-dsBlue text-white rounded-full` with `font-mono` for numbers
- Connector line: `hidden md:block absolute top-8` positioned to align with circle centers
- `relative z-10` on circles so they appear above the connector line
- Phase label (e.g., "Weeks 1-2"): `text-dsBlue font-semibold text-sm`

### 6.24 Reference Pages

Each component pattern maps to specific live pages. Use these as copy-from sources when building new pages.

| Pattern | Best Example Page | Page Type |
|---------|------------------|-----------|
| Dark hero (Section 6.1) | `healthcare/index.html` | Hand-crafted |
| Content + Image right (Section 6.2) | `healthcare/index.html` | Hand-crafted |
| Content + Image left (Section 6.2) | `healthcare/index.html` | Hand-crafted |
| Stats row (Section 6.3) | `healthcare/index.html` | Hand-crafted |
| Icon card grid (Section 6.4) | `services/blueprint/index.html` | Hand-crafted |
| Case study cards (Section 6.7) | `healthcare/index.html` | Hand-crafted |
| Testimonial carousel (Section 6.8) | `healthcare/index.html` | Hand-crafted |
| Logo ribbon (Section 6.9) | `healthcare/index.html` | Hand-crafted |
| Blog card grid (Section 6.12) | `blog/index.html` | Hand-crafted |
| FAQ accordion — hand-crafted (Section 6.16) | `healthcare/ai-agents/intelligent-scheduling/index.html` | Hand-crafted |
| FAQ accordion — WP (Section 6.16) | `ai-machine-learning/index.html` | WP-restyled |
| CTA banner — dsBlue (Section 6.19) | `services/blueprint/index.html` | Hand-crafted |
| What's Next navigation (Section 6.20) | `healthcare/ai-agents/intelligent-scheduling/index.html` | Hand-crafted |
| Benefits & deliverables (Section 6.21) | `services/blueprint/index.html` | Hand-crafted |
| Process timeline (Section 6.23) | `services/blueprint/index.html` | Hand-crafted |
| Dark section #333 (Section 9) | `services/blueprint/index.html` | Hand-crafted |
| Related Work cards | `case-studies/custom-ehr-development/index.html` | Hand-crafted |
| Tab switching (Section 10.3) | `healthcare/capabilities/ai-integration/index.html` | WP-restyled |

**Rule:** When creating a new page, read the "Best Example Page" first. Copy its structure, then modify content. Never build from memory alone.

---

## 7. Spacing Constants

| Context | Value | Notes |
|---------|-------|-------|
| Section vertical padding | `5rem` (80px) | py-20 |
| Section horizontal padding | `1.5rem` (24px) | px-6 |
| Hero top padding | `pt-32` (128px) | Accounts for fixed nav |
| Content max-width | `1280px` | max-w-screen-xl |
| Grid gap (cards) | `1.5rem` (24px) | gap-6 |
| Grid gap (layout columns) | `3rem` (48px) | gap-12 |
| Card internal padding | `1.5rem` (24px) | p-6 |
| Testimonial card padding | `2rem` (32px) | p-8 |
| Label to heading | `0.75rem` (12px) | mt-3 or mb-3 |
| Heading to text | `0.75rem-1.5rem` | mb-3 to mb-6 |
| Content to CTA | `2rem` (32px) | mb-8 or mt-8 |

---

## 8. Image Treatment Classes

| Context | Border Radius | Shadow | Other |
|---------|--------------|--------|-------|
| Hero image | rounded-2xl (16px) | shadow-xl | w-full |
| Section content image | rounded-2xl (16px) | shadow-xl | w-full h-auto |
| Card image | none (card has rounded-xl) | none | aspect-video object-cover |
| WP block image | rounded-2xl (16px) | none | max-width 100% |
| Avatar | rounded-full (50%) | none | w-12 h-12 object-cover |
| Logo (ribbon) | none | none | grayscale(100%), height 1.5-3rem |
| Gallery image | rounded-xl (12px) | none | object-cover |

### 8.1 Image Layout Rules

**No stacked images.** Never place two or more images vertically stacked within the same column or content area. Each section should use a single image to support its content. If multiple visuals are needed, place them side-by-side in a grid (e.g., `grid md:grid-cols-2 gap-6`) rather than stacking them vertically. Stacked images create excessive scroll depth and dilute visual impact.

### 8.2 Image Sizing Rules

Not every image should be `w-full`. Size images according to their content type to avoid oversized visuals that dominate the page.

| Content Type | Max Width | Tailwind Classes | Notes |
|---|---|---|---|
| Hero image (landscape screenshot, mockup) | Full column | `w-full h-auto` | Fills the hero column in a 2-col grid |
| Section content image (landscape) | Full column | `w-full h-auto` | Inside a 2-col grid, image fills one column |
| Mobile app screenshot (portrait) | 320-384px | `max-w-xs md:max-w-sm`, centered with `flex items-center justify-center` | Portrait app screens should never stretch to full width |
| Technical diagram / architecture | 768px | `max-w-3xl mx-auto` | Constrain and center within the section |
| Full-width collage / separator | Content width | `max-w-screen-xl mx-auto rounded-2xl` | Never full-bleed; constrain to content width |
| Client logo (sidebar/card) | Auto height | `h-16 w-auto` | Let width scale naturally from fixed height |
| Inline icon / small graphic | 48-64px | `w-12 h-12` or `w-16 h-16` | Fixed dimensions |

**General rules:**
1. **Match size to content.** A phone screenshot at `w-full` in a 640px column looks absurd. Constrain it.
2. **Center undersized images.** When an image is constrained smaller than its container, wrap it in `flex items-center justify-center`.
3. **Always include `h-auto`** with width constraints to maintain aspect ratio.
4. **Portrait vs landscape matters.** Landscape images can fill their column; portrait images (app screenshots, phone mockups) must be constrained.

---

## 9. Dark Section Implementation

See `brand-guide.md` for brand-level color pairing rules.

### When `data-bg="#333"` or `bg-[#333333]`:

- Background: `#333333`
- Text color: `#ffffff`
- Heading color: `#ffffff`
- Body text: `rgba(255,255,255,0.8)`
- Borders: `rgba(255,255,255,0.2)` or `#4d4d4d` (NOT gray-200)
- Buttons: `btn--light` (white bg, dark text) or white outline
- Links: `#ffffff` with underline on hover
- Dividers: preserve inline `#4d4d4d` color

**Hand-crafted dark section template** (from `services/blueprint/index.html` — "Who It's For"):

```html
<section class="py-20 px-6 bg-[#333333]">
    <div class="max-w-screen-xl mx-auto">
        <div class="text-center max-w-3xl mx-auto mb-12 fade-up">
            <span class="text-xs font-medium text-dsTeal uppercase tracking-wider">Who It's For</span>
            <h2 class="text-3xl md:text-4xl font-bold text-white mt-3 mb-4">This is right for you if&hellip;</h2>
            <p class="text-gray-300">The Blueprint is designed for organizations that need a complete,
                defensible plan before committing to a production build.</p>
        </div>
        <div class="grid md:grid-cols-3 gap-6 fade-up">
            <div class="bg-white/10 backdrop-blur rounded-xl p-8 border border-white/10 hover:border-dsTeal transition">
                <div class="w-12 h-12 bg-dsTeal/20 rounded-xl flex items-center justify-center mb-5">
                    <svg class="w-6 h-6 text-dsTeal" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4"/>
                    </svg>
                </div>
                <h3 class="font-bold text-white text-lg mb-3">Card title here</h3>
                <p class="text-gray-300 text-sm leading-relaxed">Card body text. Note text-gray-300 (not gray-500/600
                    which are too dark on #333 backgrounds).</p>
            </div>
            <!-- repeat card pattern for each item -->
        </div>
    </div>
</section>
```

**Dark section card pattern — key differences from light sections:**

| Element | Light Section | Dark Section (#333) |
|---------|--------------|-------------------|
| Card background | `bg-white` or none | `bg-white/10 backdrop-blur` |
| Card border | `border-gray-200` | `border-white/10` |
| Card hover | `hover:border-dsBlue` | `hover:border-dsTeal` |
| Icon badge bg | `bg-dsBlue` | `bg-dsTeal/20` |
| Icon color | `text-white` | `text-dsTeal` |
| Heading | `text-dsBlack` | `text-white` |
| Body text | `text-gray-600` | `text-gray-300` |
| Label | `text-dsBlue` | `text-dsTeal` |

### When `data-bg="#304fff"` (dsBlue):
- Text: `#ffffff`
- Buttons: white bg or white border
- Links: `#ffffff`
- See Section 6.19 CTA Banners for the full dsBlue section template

### When `data-bg="#26d9c4"` (dsTeal):
- Text: `#050505` (dsBlack)
- Buttons: dark variants

### When `data-bg="#d1f259"` (dsLime):
- Text: `#050505` (dsBlack)
- Buttons: dark variants

---

## 10. Interactive Components

### 10.1 Swiper Carousels

Managed by `ds-wp-interactivity.js`. Three carousel types:

| Type | Selector | Slides | Breakpoints |
|------|----------|--------|-------------|
| Service cards | `.sc-slider` | 1->2->3 | 768: 2, 1024: 3 |
| Case studies | `.js-fcs-slider` | 1->2->3 | 640: 2, 1024: 3 |
| Quote carousel | `.cqc-swiper` | 1 | Loop, autoplay 6s |

All carousels: `spaceBetween: 24`, navigation via prev/next buttons scoped to parent section.

### 10.2 FAQ Accordion

Selector: `.faq-new__item`
- Title (`.faq-new__item-title`): click toggles `.is-open` class
- Body (`.faq-new__item-text`): `max-height` animation (0 <-> scrollHeight)
- Arrow (`.faq-new__item-arrow`): rotates 0 deg <-> 180 deg
- Transition: 0.35s ease

### 10.3 Tab Switching

Selector: `.js-tab-item-nav` (data-tab attribute)
- Click activates matching `.js-tab-item-body[data-tab]`
- Deactivates all other tabs/bodies in same section
- Active class: `.isActive`

### 10.4 Alternating Backgrounds

Selector: `.guttenberg-block:not(.spacer-new)` inside `.wp-content-legacy`
- Skips dark (#333), dsBlue, dsTeal, dsLime sections
- Even index -> white (#FFFFFF)
- Odd index -> dsGray (#F5F5F5)
- Sets both inline `backgroundColor` and `data-bg` attribute

---

## 11. Animation

### Fade-Up

```css
.fade-up {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.6s ease, transform 0.6s ease;
}

.fade-up.visible {
    opacity: 1;
    transform: translateY(0);
}
```

### IntersectionObserver Configuration

- **Threshold:** 0.1
- **Root margin:** `0px 0px -50px 0px`
- **Duration:** 0.6s ease
- **WP elements:** `.inview` and `[data-aos]` classes get same treatment
- **Applied to:** `.fade-up`, `.inview`, `[data-aos]`

---

## 12. Responsive Breakpoints

| Breakpoint | Tailwind | Grid Behavior |
|------------|----------|---------------|
| < 640px | (mobile) | 1 column, reduced typography |
| 640px | sm: | Minor adjustments |
| 768px | md: | 2-3 column grids, tablet typography |
| 1024px | lg: | Full grid layouts (2-5 cols) |
| 1280px | xl: | Content max-width reached |

### Mobile-Specific Rules
- Hero grids: stack to single column
- Card grids: 1 column (2 at md:)
- Nav: hamburger menu
- Section padding: reduced (py-12 vs py-20)
- h1: 2.25rem, h2: 1.75rem

---

## 13. Deployment & Path Conventions

### Site Root & Hosting

- **Host:** Netlify via Cloudflare
- **Domain:** digitalscientists.com
- **Publish directory:** `public/` (configured in `netlify.toml` at repo root: `publish = "public"`)
- **Build command:** None — site is pre-built static HTML
- **Deploy trigger:** Push to `main` branch on GitHub

### Path Conventions

- All paths MUST be relative (depth-appropriate `../` prefix)
- Root-relative paths break in certain deployment contexts
- `ds-includes.js` auto-detects `basePath` from its own `src` URL
- On Netlify, basePath returns `/` (no subdirectory prefix needed)
- `.nojekyll` file required in repo root for subdirectory `index.html` serving
- Nav/footer links use bare-relative paths resolved by `ds-includes.js`

### Netlify Configuration Reference (from `netlify.toml`)

```toml
[build]
  command = ""
  publish = "public"

[functions]
  directory = "netlify/functions"

# Custom 404
[[redirects]]
  from = "/*"
  to = "/404.html"
  status = 404
```

Security headers and cache policy are also defined in `netlify.toml` — see Section 16 for details.

---

## 14. Case Study Page Patterns

### 14.1 JTBD Section

**Purpose:** A standardized component for displaying the user's "Jobs To Be Done" in case studies. Use when the original WP case study or engagement materials include JTBD content. Placed as a sub-section within the Challenge section (after challenge cards), preserving alternating backgrounds.

**Pattern:**
```
Location: Inside the Challenge section, after challenge cards
Wrapper: mt-16 fade-up
Label: text-xs font-medium text-dsBlue uppercase tracking-wider — "Jobs To Be Done"
Heading: h3 text-2xl md:text-3xl font-bold text-dsBlack mt-3 mb-8
Grid: grid md:grid-cols-2 gap-4

Each JTBD item:
  Container: flex items-start gap-3 border-l-4 border-dsBlue bg-dsGray rounded-r-xl pl-4 pr-5 py-4
  Icon: w-5 h-5 text-dsBlue mt-0.5 flex-shrink-0 (checkmark SVG)
  Text: text-gray-700 text-sm
```

**HTML Template:**

```html
<!-- Jobs To Be Done -->
<div class="mt-16 fade-up">
    <span class="text-xs font-medium text-dsBlue uppercase tracking-wider">Jobs To Be Done</span>
    <h3 class="text-2xl md:text-3xl font-bold text-dsBlack mt-3 mb-8">
        What [user role] needed to accomplish
    </h3>
    <div class="grid md:grid-cols-2 gap-4">
        <div class="flex items-start gap-3 border-l-4 border-dsBlue bg-dsGray rounded-r-xl pl-4 pr-5 py-4">
            <svg class="w-5 h-5 text-dsBlue mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4"/></svg>
            <p class="text-gray-700 text-sm">JTBD statement here</p>
        </div>
        <!-- Repeat for each JTBD item -->
    </div>
</div>
```

**Rules:**
1. **Heading format:** "What [user role] needed to accomplish" — adapt the user role per case study (e.g., "drivers", "clinicians", "coordinators")
2. **Item count:** Typically 4-8 items. Combine related items if the original has more than 8.
3. **Item voice:** Action-oriented, starting with a verb (e.g., "Submit service requests...", "Track the ETA..."). Rewrite from the user's perspective if the original is written from the builder's perspective.
4. **Visual distinction:** The `border-l-4 border-dsBlue` left accent + `bg-dsGray` background distinguishes JTBD items from Challenge cards (which use `border border-gray-200` full borders).
5. **Placement:** Always inside the Challenge section, after challenge cards. This maintains alternating section backgrounds.
6. **When to include:** Include when the case study has explicit JTBD content from the original WP page or engagement materials. Do NOT fabricate JTBD items.

### 14.2 Hero Section

**Purpose:** Standardized hero pattern for all hand-crafted case study pages. Distinct from the healthcare.html hero (which includes CTA buttons and a stats row).

**Layout:**
```
Background: bg-white (always)
Wrapper: <header class="pt-32 pb-16 px-6">
Container: max-w-screen-xl mx-auto
Grid: grid lg:grid-cols-2 gap-12 items-center
Mobile: stacks to single column (content above, image below)
```

**Left Column — Content:**
```
1. Label: inline-flex items-center gap-2 text-sm text-dsBlue font-medium mb-6
   - Blue dot: <span class="w-1.5 h-1.5 bg-dsBlue rounded-full"></span>
   - Text: "Case Study" (always)

2. Heading (h1): text-4xl md:text-5xl lg:text-6xl font-bold text-dsBlack mb-4 leading-tight
   - MUST be outcome-focused (describes the project result)
   - NOT the client name — the client name belongs in the Overview sidebar

3. Subtitle: text-xl text-gray-600 mb-6
   - Single paragraph, 1-2 sentences
   - Provides context: who the client is and what the engagement delivered

4. Tech Tags: flex flex-wrap gap-2
   - Each tag: text-xs font-medium text-dsBlue bg-blue-50 px-3 py-1 rounded-full
   - 3-5 tags typical (technologies, platforms, or service areas)
   - NO CTA buttons in the hero
```

**Right Column — Image sizing by content type:**

| Content Type | Classes | Notes |
|---|---|---|
| Landscape screenshot / dashboard | `rounded-2xl shadow-xl w-full` | Fills the column |
| Portrait app mockup / phone | `max-w-xs md:max-w-sm h-auto rounded-2xl shadow-xl` | Centered with `flex items-center justify-center` on wrapper |
| Product photo / composite | `w-full h-auto rounded-2xl shadow-xl` | Let natural aspect ratio dictate |
| Transparent PNG (app icon, device) | `max-w-xs md:max-w-sm h-auto` | No shadow, no background wrapper |

**General image wrapper:** `<div class="relative flex justify-center">`

**What NOT to include in the hero:**
- **No CTA buttons** — CTAs go in the final section (bg-dsBlue)
- **No stats row** — Impact stats get their own section (bg-dsBlue, after Overview)
- **No client logo** — Logo goes in the Overview sidebar card

**HTML Template:**

```html
<header class="pt-32 pb-16 px-6">
    <div class="max-w-screen-xl mx-auto">
        <div class="grid lg:grid-cols-2 gap-12 items-center">
            <div>
                <div class="inline-flex items-center gap-2 text-sm text-dsBlue font-medium mb-6">
                    <span class="w-1.5 h-1.5 bg-dsBlue rounded-full"></span>
                    Case Study
                </div>
                <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-dsBlack mb-4 leading-tight">
                    Outcome-focused title here
                </h1>
                <p class="text-xl text-gray-600 mb-6">
                    Brief context about the client and what was delivered.
                </p>
                <div class="flex flex-wrap gap-2">
                    <span class="text-xs font-medium text-dsBlue bg-blue-50 px-3 py-1 rounded-full">Tech 1</span>
                    <span class="text-xs font-medium text-dsBlue bg-blue-50 px-3 py-1 rounded-full">Tech 2</span>
                    <span class="text-xs font-medium text-dsBlue bg-blue-50 px-3 py-1 rounded-full">Tech 3</span>
                </div>
            </div>
            <div class="relative flex justify-center">
                <!-- Landscape screenshot -->
                <img src="..." alt="..." class="rounded-2xl shadow-xl w-full">
                <!-- OR portrait app mockup -->
                <img src="..." alt="..." class="max-w-xs md:max-w-sm h-auto rounded-2xl shadow-xl">
            </div>
        </div>
    </div>
</header>
```

### 14.3 Overview + Sidebar

Every case study page MUST include an Overview + Sidebar section immediately after the hero (or after the impact stats bar if present). This section identifies the client and provides engagement context.

**Layout:**
```
grid lg:grid-cols-3 gap-12
  lg:col-span-2  -> Overview text (h2 + body paragraphs)
  1 col           -> Sidebar card (client details)
```

Background: `bg-dsGray` (or `bg-white` if preceding section is already dsGray).

**Sidebar Card — Required Fields:**

Every sidebar card MUST include these five fields in this order:

| Field | Description |
|-------|-------------|
| **Logo** | Client logo, `h-16 w-auto`, centered in `mb-6 flex justify-center` wrapper. Omit if no logo available. |
| **Client** | Company name |
| **Industry** | Primary industry or vertical |
| **Services** | What DS provided (comma-separated) |
| **Engagement** | Timeframe (e.g., "March 2021 - Present" or "8 weeks") |

Do NOT add extra fields (Point of Contact, Platform, Integrations, Status, Timeline). Keep it consistent across all case studies.

**Visual Style:**
- Card: `bg-white rounded-xl p-6 border border-gray-200 h-fit`
- Label: `text-xs font-medium text-dsBlue uppercase tracking-wider mb-1`
- Value: `text-gray-600 text-sm`
- Field spacing: each field in a `div` with `mb-4` (last field has no `mb-4`)

**HTML Template:**

```html
<section class="py-20 px-6 bg-dsGray fade-up">
    <div class="max-w-screen-xl mx-auto">
        <div class="grid lg:grid-cols-3 gap-12">
            <div class="lg:col-span-2">
                <span class="text-xs font-medium text-dsBlue uppercase tracking-wider">Overview</span>
                <h2 class="text-3xl md:text-4xl font-bold text-dsBlack mt-3 mb-6">
                    Section heading here
                </h2>
                <p class="text-gray-600 text-lg mb-4">
                    Overview paragraph(s).
                </p>
            </div>
            <div class="bg-white rounded-xl p-6 border border-gray-200 h-fit">
                <div class="mb-6 flex justify-center">
                    <img src="images/client-logo.png" alt="Client Name logo" class="h-16 w-auto">
                </div>
                <div class="mb-4">
                    <p class="text-xs font-medium text-dsBlue uppercase tracking-wider mb-1">Client</p>
                    <p class="text-gray-600 text-sm">Client Name</p>
                </div>
                <div class="mb-4">
                    <p class="text-xs font-medium text-dsBlue uppercase tracking-wider mb-1">Industry</p>
                    <p class="text-gray-600 text-sm">Industry</p>
                </div>
                <div class="mb-4">
                    <p class="text-xs font-medium text-dsBlue uppercase tracking-wider mb-1">Services</p>
                    <p class="text-gray-600 text-sm">Service 1, Service 2, Service 3</p>
                </div>
                <div>
                    <p class="text-xs font-medium text-dsBlue uppercase tracking-wider mb-1">Engagement</p>
                    <p class="text-gray-600 text-sm">Start - End</p>
                </div>
            </div>
        </div>
    </div>
</section>
```

### 14.4 Testimonial Placement

**Purpose:** Client testimonials establish credibility early in the case study narrative. They appear **immediately after the Overview + Sidebar section** (or after the Impact Stats bar if one separates the two), before the Challenge section begins.

**Standard case study section order:**

```
1. Hero
2. Impact Stats Bar (bg-dsBlue) — optional
3. Overview + Sidebar
4. Client Testimonial  <-- HERE (immediately after Overview)
5. The Challenge
6-N. Content sections (research, design, architecture, features, etc.)
N+1. Results
N+2. Deliverables
N+3. Next Case Study
N+4. CTA (bg-dsBlue)
```

**Why early?** The testimonial validates the engagement before the reader dives into the details. It signals "this client was happy with the work" at the moment the reader is deciding whether to keep reading.

**Pattern (centered quote):**

```
Background: bg-white (or alternate to avoid same-bg adjacency)
Container: max-w-3xl mx-auto text-center
Section padding: py-16 (slightly tighter than content sections)
Quote icon: w-12 h-12 text-dsBlue/20 mx-auto mb-6
Quote: text-xl text-gray-700 italic mb-8 leading-relaxed
Attribution: flex items-center justify-center gap-4
  Avatar: w-14 h-14 rounded-full object-cover (or initials circle if no photo)
  Name: font-semibold text-dsBlack
  Title: text-gray-500 text-sm
```

**HTML Template:**

```html
<section class="py-16 px-6 bg-white fade-up">
    <div class="max-w-3xl mx-auto text-center">
        <svg class="w-12 h-12 text-dsBlue/20 mx-auto mb-6" fill="currentColor" viewBox="0 0 24 24"><path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-9.983zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h3.983v10h-9.983z"/></svg>
        <p class="text-xl text-gray-700 italic mb-8 leading-relaxed">
            "Client quote here."
        </p>
        <div class="flex items-center justify-center gap-4">
            <img src="images/photo-name.jpg" alt="Name, Title" class="w-14 h-14 rounded-full object-cover">
            <div class="text-left">
                <p class="font-semibold text-dsBlack">Client Name</p>
                <p class="text-gray-500 text-sm">Title, Company</p>
            </div>
        </div>
    </div>
</section>
```

If no photo is available, use an initials circle:

```html
<div class="w-14 h-14 rounded-full bg-dsBlue flex items-center justify-center flex-shrink-0">
    <span class="text-white font-bold text-lg">AB</span>
</div>
```

---

## 15. SEO Implementation

Every page on the DS site must be optimized for both traditional search engines (Google, Bing) and AI-powered answer engines (ChatGPT, Gemini, Perplexity, Claude). The goal is to **retain existing rankings**, **improve positions on high-impression pages**, and **become a cited source in LLM responses** for healthcare technology, MVP development, and custom software queries.

### 15.1 Required Meta Tags

Every page MUST include these in `<head>`. Restyled WP pages already have most of these preserved from WordPress — verify they are present and accurate.

```html
<!-- Core SEO -->
<title>Page Title | Digital Scientists</title>
<meta name="description" content="120-160 char summary. Lead with what the page delivers, not who DS is.">
<link rel="canonical" href="https://digitalscientists.com/page-url/" />

<!-- Open Graph -->
<meta property="og:locale" content="en_US" />
<meta property="og:type" content="website" />  <!-- or "article" for blog posts -->
<meta property="og:title" content="Same as <title>" />
<meta property="og:description" content="Same as meta description" />
<meta property="og:url" content="https://digitalscientists.com/page-url/" />
<meta property="og:site_name" content="Digital Scientists" />
<meta property="og:image" content="https://digitalscientists.com/path/to/social-image.png" />

<!-- Twitter/X -->
<meta name="twitter:card" content="summary_large_image" />
```

**Rules:**
- `<title>` must be under 60 characters. Format: `{Page Topic} | Digital Scientists`
- `meta description` must be 120-160 characters. Write it as a clear, factual statement — LLMs extract these.
- `canonical` must point to the production Netlify URL (not GitHub Pages)
- `og:image` should be a 1200x630px image specific to the page content. Do not use a generic site logo.

### 15.2 JSON-LD Structured Data

JSON-LD helps search engines and LLMs understand page content with precision. Add the appropriate schema block in `<head>` based on page type.

#### Organization (site-wide, on homepage only)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Digital Scientists",
  "url": "https://digitalscientists.com",
  "logo": "https://digitalscientists.com/ds-logo-black.svg",
  "description": "Digital Scientists is a digital product consultancy based in Atlanta, GA specializing in healthcare software, AI/ML development, and custom application development.",
  "foundingDate": "2007",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Atlanta",
    "addressRegion": "GA",
    "addressCountry": "US"
  },
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+1-404-654-3855",
    "contactType": "sales"
  },
  "sameAs": [
    "https://www.linkedin.com/company/digital-scientists_2",
    "https://github.com/digital-scientists"
  ]
}
</script>
```

#### Service Pages (capabilities, solutions, service offerings)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Service",
  "name": "Healthcare UX Design & Research",
  "description": "Clear 1-2 sentence description of what this service delivers and for whom.",
  "provider": {
    "@type": "Organization",
    "name": "Digital Scientists",
    "url": "https://digitalscientists.com"
  },
  "serviceType": "Healthcare UX Research",
  "areaServed": "United States",
  "url": "https://digitalscientists.com/healthcare/capabilities/healthcare-ux-design-research/"
}
</script>
```

#### Case Studies

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Outcome-focused case study title",
  "description": "Brief factual summary of what was built and the measurable results.",
  "author": {
    "@type": "Organization",
    "name": "Digital Scientists"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Digital Scientists",
    "url": "https://digitalscientists.com"
  },
  "datePublished": "2024-01-15",
  "url": "https://digitalscientists.com/case-studies/slug/"
}
</script>
```

#### Blog Posts

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "Blog post title",
  "description": "Factual summary of the post's content.",
  "author": {
    "@type": "Person",
    "name": "Author Name"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Digital Scientists"
  },
  "datePublished": "2025-06-01",
  "dateModified": "2025-06-15",
  "url": "https://digitalscientists.com/blog/slug/"
}
</script>
```

#### FAQ Sections (when present on page)

If a page contains an FAQ accordion, add FAQPage schema:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is clinical decision support?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Clinical decision support (CDS) systems provide clinicians with knowledge and patient-specific information at the point of care to improve decision-making."
      }
    }
  ]
}
</script>
```

### 15.3 Heading Hierarchy

**Rules:**
- Every page MUST have exactly one `<h1>` tag — the primary topic of the page
- Use `<h2>` for major sections, `<h3>` for subsections. Never skip levels (e.g., h1 -> h3)
- Headings should read as a scannable outline of the page's content
- Include target keywords naturally in `<h1>` and `<h2>` tags — do not keyword-stuff
- LLMs use heading structure to understand page organization. Clear hierarchy = better extraction.

### 15.4 Content Writing for Discoverability

LLMs prioritize content that is **factual, specific, well-structured, and authoritative**. Every page should follow these guidelines:

**Lead with facts, not marketing language:**
- YES: "Digital Scientists built an AI-powered medical coding platform that reviews patients 50X faster than manual coding, achieving 90%+ accuracy across 20,000+ patients."
- NO: "We're passionate about leveraging cutting-edge technology to transform healthcare delivery."

**Include entity-rich statements:**
- Name the company, the technology, the industry, the outcome, and the location in natural prose
- LLMs index entity relationships — "Digital Scientists, an Atlanta-based healthcare software consultancy" is more discoverable than "our team"

**Structure content for extraction:**
- Use definition-style patterns: "**Population health management** is the practice of..."
- Use clear cause-effect statements: "By implementing AI-driven RAF coding, CommuniCare reduced chart review time from 60 minutes to 60 seconds per patient."
- Include specific numbers, dates, and proper nouns — LLMs weight factual specificity

**Internal linking creates topical authority:**
- Every page should link to 3-5 related pages within the DS site
- Use descriptive anchor text: "our healthcare interoperability solutions" not "click here"
- The healthcare hub -> domain -> market -> case study link structure builds a content cluster that signals expertise to both Google and LLMs

### 15.5 URL Structure

**Rules:**
- Use descriptive, keyword-rich slugs: `/case-studies/ai-medical-coding-platform/` not `/case-studies/client-name/`
- Keep client names out of URLs — use the service or outcome as the slug
- All URLs must use lowercase, hyphens (not underscores), and end with `/`
- Never change a URL without setting up a 301 redirect from the old path (see `redirect-tracking.md`)
- Maximum URL depth: 3 levels (e.g., `/healthcare/solutions/cdss/`)

### 15.6 Image SEO

**Rules:**
- Every `<img>` MUST have a descriptive `alt` attribute: "Screenshot of the AI medical coding workbench showing ICD-10 suggestions with confidence scores" not "image1" or ""
- Use descriptive filenames: `raf-coder-workbench.png` not `Screenshot-2024-01-15.png`
- Include `width` and `height` attributes to prevent layout shift (CLS)
- Use `loading="lazy"` for images below the fold
- Hero images and social share images should be optimized to < 200KB

### 15.7 Page Speed

Static sites inherently outperform WordPress on speed. Maintain this advantage:

- **No render-blocking resources** — use `defer` on all scripts (already standard in Section 1)
- **Minimize external requests** — Tailwind CDN, Google Fonts, and Swiper are the only external dependencies
- **Image optimization** — serve appropriately sized images; do not serve 3000px originals at 800px display size
- **Font display** — Google Fonts link already uses `display=swap` (prevents FOIT)

### 15.8 LLM-Specific Optimization

Beyond traditional SEO, these practices improve how LLMs reference your content:

**Topical authority through content depth:**
- The healthcare hub structure (hub -> capabilities -> solutions -> domains -> markets -> case studies -> AI guides) creates the kind of comprehensive topic coverage that LLMs recognize as authoritative
- Each page should cover its topic thoroughly — thin pages get skipped by LLMs

**Structured data for knowledge graph inclusion:**
- JSON-LD (Section 15.2) helps LLMs map your content to their internal knowledge graphs
- Organization schema establishes Digital Scientists as an entity LLMs can reference
- Service schema connects specific capabilities to the organization

**Cite-worthy content patterns:**
- Original research, benchmarks, and methodology descriptions get cited by LLMs
- Case study results with specific metrics ("50X faster", "$10M+ in RAF improvements") are extractable facts
- Comparison content and "how it works" explanations are high-citation patterns
- Industry frameworks and glossary-style definitions establish authority

**robots.txt and crawling:**
- Ensure the production site allows all major crawlers (Googlebot, Bingbot, GPTBot, Google-Extended, ClaudeBot, PerplexityBot)
- Do NOT block AI crawlers in robots.txt — blocking them removes you from LLM training data and responses
- The staging site (GitHub Pages) should block all crawlers to prevent duplicate content

### 15.9 Per-Page Audit Checklist

Before a page is considered complete, verify:

- [ ] `<title>` present, under 60 chars, includes primary keyword
- [ ] `meta description` present, 120-160 chars, factual statement
- [ ] `canonical` URL points to production path
- [ ] Open Graph tags complete (title, description, url, image, site_name)
- [ ] JSON-LD block present, matches page type (Service, Article, BlogPosting, FAQPage)
- [ ] Exactly one `<h1>`, logical heading hierarchy (h1 -> h2 -> h3)
- [ ] All images have descriptive `alt` text
- [ ] All images have `width` and `height` attributes
- [ ] Internal links use descriptive anchor text (3-5 per page minimum)
- [ ] URL is descriptive, lowercase, hyphenated, no client names
- [ ] Page content includes entity-rich factual statements (company, tech, industry, outcome)
- [ ] No blocked crawlers in robots.txt for production

---

## 16. CSP & Security Headers

The site sends a `Content-Security-Policy` header with every page response. It tells the browser exactly which external domains are allowed to load scripts, images, fonts, make API calls, etc. Anything not explicitly whitelisted gets blocked silently.

### 16.1 Content Security Policy

**Why we have it:** CSP defends against **cross-site scripting (XSS)** and **data injection attacks**. If someone managed to inject malicious code into the site (through a form, a compromised third-party script, etc.), the CSP prevents that code from phoning home to an attacker's server or loading malicious scripts — because those domains wouldn't be on the whitelist.

**Where it lives:** The CSP is defined in `netlify.toml` at the repo root, inside the `[[headers]]` block for `/*` (all pages). It deploys automatically with every push to main.

**Directive Reference:**

| Directive | Controls | Currently Allowed |
|---|---|---|
| `script-src` | JavaScript execution | Our site, inline scripts, GTM, GA, StatCounter, Pipedrive, RB2B (S3 + app), CookieYes, Workable, jsDelivr CDN |
| `connect-src` | API calls (fetch/XHR) | Formspree, Pipedrive, GA, StatCounter, RB2B (app + AWS API Gateway), S3 |
| `img-src` | Image loading | Our site, data URIs, StatCounter pixels, YouTube thumbnails, Google/GTM pixels, RB2B, EventScribe, CDC |
| `style-src` | CSS loading | Our site, inline styles, jsDelivr CDN (Tailwind) |
| `font-src` | Font files | Our site only (Inter + Roboto Mono are self-hosted) |
| `frame-src` | Iframes / embeds | YouTube, Vimeo, SlideShare, Workable (job listings) |
| `media-src` | Video / audio files | Our site + `media.digitalscientists.com` (Cloudflare R2) |
| `form-action` | Form submission targets | Our site + Formspree |
| `frame-ancestors` | Who can iframe our site | Nobody (`'none'`) — prevents clickjacking |
| `object-src` | Flash / plugins | Nobody (`'none'`) |

**Adding a new third-party service:**

When onboarding a new tool (analytics, chat widget, CRM integration, etc.), its domains must be added to the CSP or the browser will silently block it. This is the most common gotcha.

1. **Identify all domains the service uses.** Check the vendor's docs or load the site with DevTools Console open — CSP violations show as red errors with the blocked domain name.
2. **Add each domain to the correct directive(s)** in `netlify.toml`. A single service often needs multiple directives (e.g., `script-src` to load its JS, `connect-src` to phone home, `img-src` for tracking pixels).
3. **Push and verify.** Open the live site in incognito, open DevTools -> Console. Zero CSP errors = working. Check the Network tab to confirm the service's requests return 200.

### 16.2 Other Security Headers

The CSP is the most complex header, but we also set four others in the same `netlify.toml` block:

| Header | What It Does |
|---|---|
| `Strict-Transport-Security` | Forces HTTPS for 1 year. Browsers remember and never attempt HTTP. |
| `X-Frame-Options: DENY` | Prevents other sites from embedding ours in an iframe (clickjacking). |
| `X-Content-Type-Options: nosniff` | Prevents browsers from guessing file types. A .css file is always CSS, never JS. |
| `Referrer-Policy` | Only sends the origin domain (not full URL path) when linking to external sites. |
| `Permissions-Policy` | Disables camera, microphone, and geolocation APIs. Not needed, common attack vectors. |

### 16.3 Cache Policy

Cache headers are set in `netlify.toml` and control how long Cloudflare (CDN) and browsers hold onto files before checking the origin for updates.

| File Type | Cache-Control | Meaning |
|---|---|---|
| HTML (`.html`, `/`) | `max-age=0, must-revalidate` | Always check origin. Pages update immediately after deploy. |
| JS (`.js`) | `max-age=3600, must-revalidate` | Cache 1 hour, then recheck. Updates visible within 60 minutes. |
| CSS (`.css`) | `max-age=3600, must-revalidate` | Cache 1 hour, then recheck. Updates visible within 60 minutes. |
| Images, fonts (`.webp`, `.png`, `.jpg`, `.svg`, `.woff2`) | `max-age=31536000, immutable` | Cache forever. Safe because image filenames don't change in place. |

**Why JS and CSS are not `immutable`:** These files (`ds-includes-v2.js`, `ds-nav.css`, etc.) are edited in place and redeployed with the same filename. If Cloudflare caches them as `immutable`, updates become invisible until the cache expires (up to a year). This caused a 3-day outage of RB2B visitor tracking in March 2026. Only use `immutable` for files with hashed/versioned filenames that never change.

**Rule:** Never set `immutable` on any file that gets updated in place. If you add a new file type to `netlify.toml` cache headers, use `max-age=3600, must-revalidate` unless the filename includes a content hash.

---

## Revision History

- 2026-03-07: v1.0 — Extracted from ds-design-standard.md as part of brand guide consolidation
