# Digital Scientists Brand Guide

**Version 1.0 — March 2026**

**Companion Documents:**
- `web-implementation.md` — HTML templates, Tailwind classes, CSS overrides, JS config (website builds only)
- `image-generation.md` — LLM prompt construction for blog heroes, LinkedIn graphics, OG images
- `method-illustration-prompts.md` — Nana Banana prompts for METHOD figure plates

**Who this is for:** Human designers, agency partners, and Claude. If you are producing any Digital Scientists marketing asset — website page, LinkedIn post, slide deck, email, PDF, business card — this document defines how it should look, read, and feel.

---

## Table of Contents

### Part 1: Brand Foundation
1. [Purpose & Scope](#1-purpose--scope)
2. [Brand Identity](#2-brand-identity)
3. [Logo & Brand Marks](#3-logo--brand-marks)
4. [Color System](#4-color-system)
5. [Typography](#5-typography)
6. [Voice & Tone](#6-voice--tone)
7. [Visual Principles (All Imagery)](#7-visual-principles-all-imagery)

### Part 2: Imagery Standards
8. [Image Types & Specifications](#8-image-types--specifications)
9. [METHOD Illustration Standard](#9-method-illustration-standard)
10. [Image Processing & Naming](#10-image-processing--naming)
11. [Quality Control](#11-quality-control)

### Part 3: Digital Channel Standards
12. [Website](#12-website)
13. [LinkedIn](#13-linkedin)
14. [Email Marketing](#14-email-marketing)

### Part 4: Print & Physical Channel Standards
15. [Presentations (Google Slides / PowerPoint)](#15-presentations-google-slides--powerpoint)
16. [Sales Collateral](#16-sales-collateral)
17. [Stationery](#17-stationery)
18. [Signage & Environmental](#18-signage--environmental)

### Part 5: Appendices
- [A. Brand Asset Inventory](#a-brand-asset-inventory)
- [B. Quick Reference Card](#b-quick-reference-card)
- [C. Brand Evolution Notes](#c-brand-evolution-notes)
- [D. Revision History](#d-revision-history)

---

# Part 1: Brand Foundation

---

## 1. Purpose & Scope

### What This Document Covers

Every visual, verbal, and structural decision for Digital Scientists marketing assets across all channels:

- Website (digitalscientists.com)
- LinkedIn (Bob Klein personal + DS company page)
- Email marketing and signatures
- Google Slides / PowerPoint presentations
- Sales collateral (one-pagers, case study PDFs, proposals)
- Stationery (business cards, letterhead, note cards)
- Signage and environmental branding

### What This Document Does NOT Cover

- Website HTML/CSS/JS implementation details → see `web-implementation.md`
- LLM image prompt construction → see `image-generation.md`
- METHOD illustration prompts → see `method-illustration-prompts.md`
- Content strategy and editorial calendar → see `content-strategy.md`
- Publishing procedures and workflows → see `ds-operating-procedures.md`

### Who Uses This

| Audience | Reads This For |
|----------|---------------|
| Human designer / agency | Full brand system — can produce any DS asset |
| Claude (web page tasks) | Brand context + cross-ref to web implementation companion |
| Claude (image generation) | Visual principles + cross-ref to image generation companion |
| Claude (content writing) | Voice & tone + channel-specific rules |
| New team members | Brand orientation |

---

## 2. Brand Identity

### The DS METHOD

Everything Digital Scientists produces — services, content, imagery — flows from the DS METHOD:

**Discover → Experiment → Engineer → Optimize**

This four-phase cycle is not a sales pitch. It is how DS actually works. Every engagement follows this structure, and every piece of marketing should reflect this disciplined, evidence-driven approach.

### Positioning

**Primary positioning (healthcare-first):**
> Digital Scientists reduces clinician burden and recovers lost revenue through custom healthcare software and AI.

**Supporting proof points:**
- $10M+ in PDPM revenue recovered
- 50X faster medical coding
- 90%+ coding accuracy across 20,000+ patients
- 45-minute → 5-minute clinical documentation

**Company identity:**
Digital Scientists is a digital product consultancy based in Atlanta, GA. Founded in 2007. Specializes in healthcare software, AI/ML development, and custom application development.

### Executive Tone

Every DS asset — image, page, slide, post — should feel:

- **Calm** — no urgency theater, no countdown timers, no "act now"
- **Deliberate** — every element earns its place
- **Structured** — information has clear hierarchy
- **Accountable** — claims backed by evidence
- **Professional** — would a CIO share this?

If it feels flashy, dramatic, busy, or generic — it fails.

---

## 3. Logo & Brand Marks

### 3.1 Primary Logo

The DS logo is the **"DIGITAL SCIENTISTS" stacked wordmark** — "DIGITAL" above "SCIENTISTS" in a clean sans-serif typeface. It exists in two versions:

| Version | File | Use On |
|---------|------|--------|
| Black | `ds-logo-black.svg` | Light backgrounds (white, dsGray, light images) |
| White | `ds-logo-white.png` | Dark backgrounds (dsBlack, #333, dark images, dsBlue) |

**Rules:**
- The logo is ALWAYS the full wordmark. Never abbreviate to "DS" in the logo context (the "DS" monogram is only for the favicon).
- Never recreate or retype the logo. Always use the source files.
- The logo is always horizontal (stacked). There is no vertical or single-line variant.

### 3.2 Favicon / Monogram

| Element | File | Description |
|---------|------|-------------|
| Favicon | `favicon.svg` | "DS" monogram on dsBlue (#304FFF) background |

Used only in browser tabs and app icons. Never as a replacement for the full wordmark.

### 3.3 Clear Space

Minimum clear space around the logo on all sides:

| Context | Minimum Clear Space |
|---------|-------------------|
| Print | 0.375 inches (≈ 10mm) |
| Digital | 10px padding on all sides |

The clear space must be free of text, graphics, and page edges. When the logo appears near page margins, ensure the clear space does not extend beyond the printable area.

### 3.4 Minimum Size

| Context | Minimum Width |
|---------|--------------|
| Print | 0.69 inches |
| Digital | 50px |

Below these sizes, the wordmark becomes illegible. Do not attempt to use the logo smaller than this.

### 3.5 Incorrect Usage

Never:
- Distort, stretch, or rotate the logo
- Apply drop shadows, outlines, or effects
- Place the logo on busy backgrounds without sufficient contrast
- Recolor the logo (only black and white versions exist)
- Crowd the logo with adjacent elements (respect clear space)
- Use the logo as a decorative pattern
- Lock up the logo with other brand logos without clear separation

### 3.6 Logo on Colored Backgrounds

| Background | Logo Version | Notes |
|------------|-------------|-------|
| White / dsGray (#F5F5F5) | Black | Standard |
| dsBlack (#050505) | White | Standard |
| #333333 (dark sections) | White | |
| dsBlue (#304FFF) | White | |
| dsTeal (#26D9C4) | Black | Dark text on light background |
| dsLime (#D1F259) | Black | Dark text on light background |
| Photography / imagery | White with sufficient contrast | May need semi-transparent dark overlay behind logo |

### 3.7 Pixel Extractions (Brand Shapes)

Geometric shapes derived from the DS brand system — L-shaped, square, and quarter-circle forms rendered in brand colors on dark backgrounds.

**Where pixel extractions are used:**
- LinkedIn cover photos (company + personal)
- Office signage (interior window banners)
- Presentation divider slides (dark backgrounds)
- Collateral accent elements (one-pager headers, proposal covers)

**Where pixel extractions are NOT used:**
- Website pages (the website uses editorial illustration + clean Tailwind layouts)
- Blog imagery
- Email templates

**Rules:**
- Always on dark backgrounds (dsBlack or #333)
- Use brand colors only: dsBlue, dsTeal, dsLime, white
- Never as primary content — always as accent/decorative elements
- Never overlapping or crowding text or logos
- Maintain geometric precision — no freeform or organic shapes

---

## 4. Color System

### 4.1 Primary Palette

| Token | Hex | RGB | Usage |
|-------|-----|-----|-------|
| dsBlue | `#304FFF` | 48, 79, 255 | Primary CTA, links, section labels, badges, accents |
| dsBlack | `#050505` | 5, 5, 5 | Headings, body text, dark backgrounds, dark buttons |
| White | `#FFFFFF` | 255, 255, 255 | Primary backgrounds, cards, dark-section text |

### 4.2 Secondary Palette

| Token | Hex | RGB | Usage |
|-------|-----|-----|-------|
| dsGray | `#F5F5F5` | 245, 245, 245 | Alternating section backgrounds |
| dsTeal | `#26D9C4` | 38, 217, 196 | Accent highlights (checkmarks, icons, dark-section accents) |
| dsLime | `#D1F259` | 209, 242, 89 | Accent backgrounds (CTA banners, attention) |

### 4.3 Supporting Grays

| Token | Hex | Usage |
|-------|-----|-------|
| gray-50 | `#F9FAFB` | Subtle backgrounds |
| gray-200 | `#E5E7EB` | Card borders, dividers |
| gray-500 | `#6B7280` | Secondary text, captions |
| gray-600 | `#4B5563` | Body text (primary reading) |

### 4.4 Status Indicator Colors

Used in blog hero imagery, METHOD diagrams, presentations, and dashboards:

| Color | Meaning | When to Use |
|-------|---------|-------------|
| Green | Validated, approved, complete | Approved gates, passing checks, active status |
| Amber | Under review, in progress, attention needed | Pending items, review gates, caution |
| Red | Gap found, risk identified, rejected | Failed checks, blocked items, problems surfaced |
| Gray | Not selected, pending, inactive | Muted options, deferred items |

Status indicators should be the **brightest visual elements** in any composition. They are accent, never fill.

### 4.5 Color Pairing Rules

| Background | Text | Buttons | Links |
|------------|------|---------|-------|
| White / dsGray | dsBlack headings, gray-600 body | bg-dsBlue text-white | text-dsBlue |
| dsBlack | White headings, gray-500 body | bg-dsBlue text-white | text-white |
| #333333 | White headings, gray-300 body | bg-white text-dsBlack | text-white |
| dsBlue | White text | bg-white text-dsBlue | text-white underline |
| dsTeal | dsBlack text | bg-dsBlack text-white | text-dsBlack underline |
| dsLime | dsBlack text | bg-dsBlack text-white | text-dsBlack underline |

### 4.6 Colors in Imagery

**LLM-generated illustrations (blog heroes, conceptual):**
- Muted corporate blues, soft slate grays, warm neutral backgrounds
- Low saturation overall
- Status indicators (R/A/G) are the most saturated elements
- No bright fills, no neon, no gradients

**Product screenshots and mockups:**
- Show the product as-is — do not color-grade or filter
- Container framing (rounded corners, shadow) provides visual separation

**Stock photography:**
- Muted, natural tones preferred
- Avoid oversaturated, HDR-processed, or heavily filtered images
- Healthcare stock: calm clinical settings, not dramatic ER scenes
- Technology stock: clean workspaces, not "hacker in dark room" clichés

---

## 5. Typography

### 5.1 Font Families

| Role | Family | Weights | Source |
|------|--------|---------|--------|
| Primary (all text) | Inter | 300, 400, 500, 600, 700, 800 | Google Fonts |
| Monospace (code, data) | Roboto Mono | 400, 500 | Google Fonts |

**Inter replaced RM Pro** (the previous brand typeface) across all channels as of 2025. All new assets must use Inter. Do not use RM Pro in any new material.

### 5.2 Typography Scale

| Element | Size | Weight | Additional |
|---------|------|--------|------------|
| h1 (hero titles) | 3.5rem (56px) | 800 (ExtraBold) | letter-spacing: -0.02em |
| h2 (section headings) | 2.5rem (40px) | 700 (Bold) | letter-spacing: -0.02em |
| h3 (subsection / card headings) | 1.5rem (24px) | 600 (SemiBold) | letter-spacing: -0.02em |
| h4 (card titles alt) | 1.25rem (20px) | 600 (SemiBold) | letter-spacing: -0.02em |
| h5 / label | 0.875rem (14px) | 600 (SemiBold) | dsBlue, uppercase, tracking 0.05em |
| Body | 1.125rem (18px) | 400 (Regular) | line-height: 1.6 |
| Small / caption | 0.875rem (14px) | 400 (Regular) | |

**Critical rule:** All headings (h1–h4) get `letter-spacing: -0.02em`. This tightened tracking is a signature DS typographic detail.

### 5.3 Channel-Specific Font Rules

| Channel | Primary Font | Fallback | Notes |
|---------|-------------|----------|-------|
| Website | Inter (Google Fonts CDN) | system-ui, sans-serif | Loaded via `display=swap` |
| LinkedIn graphics | Inter (installed locally) | — | Export as image, no fallback needed |
| Email | Arial, Helvetica, sans-serif | System font stack | Email clients don't support web fonts reliably |
| Google Slides | Inter (upload to Slides) | Arial | Install Inter on presentation machine |
| PowerPoint | Inter (installed locally) | Arial | Embed fonts in file if sharing externally |
| Print (InDesign/PDF) | Inter | — | Use OpenType files for full weight range |

### 5.4 Responsive Typography (Web)

| Element | Desktop | Mobile (< 768px) |
|---------|---------|-------------------|
| h1 | 3.5rem | 2.25rem |
| h2 | 2.5rem | 1.75rem |

See `web-implementation.md` §2 for Tailwind class strings.

---

## 6. Voice & Tone

### 6.1 DS Voice Profile

Digital Scientists content is:

- **Expert but not academic** — we explain complex things simply, without jargon
- **Confident but not arrogant** — we state what we know, acknowledge what we don't
- **Outcome-focused** — we lead with results, not process
- **Anti-sales** — no urgency theater, no superlatives, no "revolutionary" or "cutting-edge"
- **Generous** — we share how things work, not just that they work

### 6.2 Two Voices

**Bob Klein (personal LinkedIn, bylined blog posts):**
- Opinionated and direct
- Story-driven — often starts with an anecdote or observation
- First person: "I've seen this pattern repeatedly..."
- Willing to be contrarian: "Most healthcare apps fail HIPAA not out of ignorance but because..."
- Still professional — never snarky or dismissive

**DS Company (company LinkedIn, website pages, collateral):**
- Expert and generous
- Third person or second person: "Digital Scientists built..." or "Your organization can..."
- Data-backed: leads with metrics and outcomes
- Structured: uses frameworks and clear comparisons
- Authoritative without being preachy

### 6.3 Writing Rules

1. **Active voice.** "We reduced documentation time from 45 minutes to 5 minutes" not "Documentation time was reduced."
2. **Specific over vague.** "$10M+ in PDPM revenue recovered" not "significant cost savings."
3. **Lead with the result.** "50X faster medical coding — here's how" not "How we improved medical coding."
4. **No buzzword soup.** Never: "leveraging cutting-edge AI to transform healthcare delivery." Instead: "We built an AI coding platform that reviews patients 50X faster than manual coding."
5. **No urgency theater.** Never: "Act now before it's too late." Never: countdown timers, false scarcity, "limited spots."
6. **Earn every claim.** Every quantitative claim must be traceable to a real engagement. Never fabricate or round up metrics.

### 6.4 Terminology Preferences

| Use | Don't Use |
|-----|-----------|
| custom software | bespoke solutions |
| AI-powered | AI-driven, AI-enabled, intelligent |
| healthcare software | health tech, healthtech, digital health |
| clinician burden | provider burnout (unless quoting) |
| lost revenue | revenue leakage (unless in context) |
| build | develop, engineer (in marketing copy) |
| engagement | project (we run engagements, not projects) |

---

## 7. Visual Principles (All Imagery)

These principles apply to every image across every channel — website, LinkedIn, slides, collateral, email.

### 7.1 One Image, One Job

Each image communicates one thing:
- A product we built (case study)
- An argument we're making (blog hero)
- A capability we offer (service page)
- A result we delivered (testimonial/stats context)

If the viewer needs to study the image, it's too complex. If the image could belong to a different page on the same topic, it's too generic.

### 7.2 Argument Over Topic

**This is the most important distinction in the entire standard.**

- **Topic** = what the article/post is about
- **Argument** = what it concludes

An image that illustrates the topic is generic. An image that illustrates the argument is specific.

| Article | Topic (Generic) | Argument (Specific) |
|---------|----------------|---------------------|
| Software Development Risk | "Risk exists in software" | "Proactive governance protects ROI" |
| Buy, Build, or Partner | "Three options exist" | "Discovery finds gaps, SaaS falls short, partnering is the path" |
| Platform Modernization | "Legacy systems need updating" | "Architectural validation before migration reduces cost" |

### 7.3 Visual Hierarchy

Every image has a single dominant focal point. Supporting elements are muted or smaller. Nothing competes for attention.

### 7.4 No Visual Slop

Absolutely avoid — across all channels, all asset types:

- Glowing arrows or neon gradients
- 3D render effects or cyber grids
- Floating tech icons, DNA strands, random gears
- Fake dashboards or fake metrics
- Stock photo clichés (handshakes over laptops, pointing at screens)
- Hexagon network patterns
- "Futuristic" anything
- Overly dramatic lighting
- Abstract tech vortex imagery
- Tron-style grid backgrounds
- Giant upward arrows
- Dollar icons scattered everywhere
- Overly glossy 3D UI
- Rubber stamps, starbursts, gauges, speedometers

If it looks like a SaaS landing page from 2016, reject it.

### 7.5 Human Figures

When used in illustrations:
- Calm posture, focused, reviewing documents, engaged in evaluation
- Always viewed from fully behind, in profile, or from above — **never facing camera, no visible faces**
- Gray/dark suits for business, scrubs for healthcare
- Figures always have purpose — doing something, not posing

Avoid:
- Salesy gestures or presentation poses
- Smiling theatrics or overly expressive emotion
- The tone is disciplined, not inspirational

### 7.6 AI Representation

When AI is included in imagery:
- Subtle interface, clean data rows, minimal flow symbol
- AI should look **operational**, not mystical
- No glowing neural networks, no sci-fi imagery, no robots

### 7.7 Risk Representation

Risk should be shown through:
- Structured indicators (R/A/G dots)
- Governance checkpoints
- Review gates, status signals
- Controlled progression

Risk should **NOT** be shown as:
- Fire, cracks, collapsing bridges
- Chaos explosions, dramatic red pathways
- Catastrophic imagery of any kind

Risk at Digital Scientists is managed through discipline — not avoided through magic.

---

# Part 2: Imagery Standards

---

## 8. Image Types & Specifications

### 8.1 Combined Specifications Table

| Image Type | Dimensions | Aspect Ratio | Format | Max Size | Used In |
|------------|-----------|-------------|--------|----------|---------|
| Blog hero | 1440×810 | 16:9 | WebP | 200 KB | Blog post pages |
| Service page hero | 1200×800 min | ~3:2 | WebP | 200 KB | Service pages |
| Case study hero | 1200×800 (landscape) or 600×1066 (portrait) | Varies | WebP | 200 KB | Case study pages |
| Homepage hero | 1440×810 min | Free | WebP | 200 KB | Homepage, landing pages |
| Card thumbnail | 640×360 | 16:9 | WebP | 60 KB | Blog grid, case study grid, related cards |
| Section content | Max 1280 wide | Proportional | WebP | 150 KB | 2-column layouts |
| Blog inline | Max 960 wide | Proportional | WebP | 100 KB | Within article body |
| OG / social preview | 1200×630 | 1.91:1 | PNG | 300 KB | Social sharing, link previews |
| Team headshot | 400×400 | 1:1 | WebP | 40 KB | Team pages, testimonials |
| Logo / icon | Max 200 wide | Proportional | SVG (preferred) or WebP | 15 KB | Logo ribbons, partner sections |
| METHOD diagram | Max 1440 wide | Landscape | WebP (quality 90+) | 200 KB | METHOD pages, blog inline |
| LinkedIn single post | 1200×1200 or 1200×627 | 1:1 or ~1.91:1 | PNG | 500 KB | LinkedIn feed |
| LinkedIn carousel slide | 1080×1350 | 4:5 | PNG | 500 KB | LinkedIn carousels |
| Presentation graphic | 1920×1080 | 16:9 | PNG | 1 MB | Google Slides, PowerPoint |
| Email header | 600 wide | ~3:1 | PNG or JPEG | 100 KB | Email marketing |

### 8.2 Blog Hero Images

16:9 smooth editorial illustrations (simplified but realistic — not flat vector, not clip-art).

- Illustrate the article's **argument**, not just its topic
- Four composition types: Partnership Scene (A), Decision Desk (B), Lifecycle View (C), Minimal Boardroom (D)
- Three artifact layers: Focal (required), Context (2-3), Environmental (1-2)
- Muted corporate blues, soft slate grays, warm neutral backgrounds
- Status indicators (R/A/G) are the brightest elements
- Max 3 short labels and 1 short title in the image
- Alternate composition types between adjacent posts

**Full prompt construction process:** See `image-generation.md`

### 8.3 Service Page Heroes

Show what DS delivers — the capability made tangible.

**Preferred image types (priority order):**
1. Product screenshot or dashboard showing real DS work
2. Device mockup (phone, tablet, laptop) showing a real interface
3. Custom illustration in the blog hero visual language

**Do NOT use:**
- Raw phone screenshots with removed backgrounds
- Personal headshots
- Generic stock photos
- Canva-style graphics

**Composition:** Landscape preferred. Portrait (mobile app) uses constrained width. Consistent rounded-2xl shadow-xl treatment. White background (service pages are inner pages).

### 8.4 Case Study Heroes

Show the product we built — the work made visible.

**Preferred image types (priority order):**
1. Multi-device mockup (phone + tablet + laptop showing the product)
2. Product screenshot (dashboard, key screen, primary workflow)
3. App overview composite (2-3 screens side by side)
4. Single device screenshot for mobile-only products

**What makes a great case study hero:**
- Shows the actual product at its best moment
- The product is clearly identifiable even at thumbnail size
- Clean, uncluttered — no browser chrome, no system UI, no debug overlays

### 8.5 Homepage & Landing Page Heroes

Set the brand tone — structured, confident, distinctive.

**Pattern:** `bg-dsBlack` dark hero differentiates top-of-funnel pages from inner pages. This is intentional and should be maintained.

**Preferred images:** Custom illustration (branded character, workflow diagrams). Hero can bleed to edges (no rounded corners required on dark backgrounds). Should feel premium and distinctive.

### 8.6 Card Thumbnails

Quick visual identification at small size. Must be instantly recognizable and differentiated from adjacent cards.

**Rules:**
- All cards use 16:9 containers with object-cover
- Image must work at 16:9 crop — portrait images get heavily cropped
- Adjacent thumbnails should be visually distinct (different composition, different dominant color)
- Thumbnail is always the same image as the page's hero — never a separate asset

### 8.7 OG / Social Preview Images

Every page has a branded OG image for social sharing (1200×630, PNG).

**Layout (A2 template):**
- Hero image background (blurred/darkened) with gradient overlay
- DS logo (top-left, white)
- Title text (white, Inter Bold)
- Category pill (dsBlue bg, white text)

Generated by `scratchpad/generate_og_images.py`. Re-run after changing hero images.

---

## 9. METHOD Illustration Standard

These specifications define the requirements for generating formal process diagrams and technical illustrations in the aesthetic of a published figure plate from a 1950s–1960s scientific or engineering textbook. Used for DS METHOD diagrams, system architecture views, process flows, and performance charts.

### 9.1 General Aesthetic

- **Restraint and Precision:** Images must appear as published illustrations — precise, informational, and elegant in their restraint
- **Scholarly Tone:** Scholarly, timeless, and quietly authoritative, rewarding close inspection
- **1950s Optimism:** Content reflects authentic 1950s optimism regarding science, industrial automation, and technological progress

### 9.2 Contrast, Tone, and Media (CRITICAL)

- **Pure White Background:** #FFFFFF — resembling bright copy paper under fluorescent light
- **Dense Black Ink:** All linework, text, and marks in true black (#000000) — full coverage, no fading
- **Pristine Original Print:** First-run letterpress impression where the type bit deep into the paper — NOT a vintage scan or reproduction
- **Zero Noise:** White areas perfectly clean — no texture, grain, noise, yellowing, or paper texture. Gray washes prohibited
- **Monochromatic Constraint:** Pure black ink on pure white paper, maximum contrast. No color except where explicitly noted

### 9.3 Layout and Structural Elements

- **Orientation:** Landscape, enclosed in thin-thick-thin triple rule border
- **Typography:** Typeset serif fonts (Garamond, Caslon, Century Schoolbook style) — never casual handwriting
- **Integrated Title:** Main title integrated into the caption at the bottom of the plate, not as a large header
- **Figure Caption:** Formal, centered at bottom in italic serif type
- **Technical Labels:** Small, spaced serif capitals
- **Annotations:** Typeset in italics

### 9.4 Rendering Technique

- **Fine Pen-and-Ink Style:** Precise style of technical illustrators (Encyclopaedia Britannica, patent drawings)
- **Shading:** Tonal gradation through stipple shading (dots) and cross-hatching only — no soft gradients
- **Linework:** Crisp, confident, bold, mechanical — technical pen precision. Connector lines routed orthogonally (right angles only)
- **Drafting Accuracy:** Precise ruled axes, technical instrument conventions, proper engineering cross-hatching
- **Sequence Markers:** Small Roman numerals (i, ii, iii, iv) along primary paths

### 9.5 Standard Diagram Archetypes

**9.5.1 Refined Iterative Circular Diagram** — For METHOD cycle and iterative process visualizations
- Nodes on a precise circle, connected by curved clockwise arrows
- Four phases at 90° intervals (12, 3, 6, 9 o'clock)
- Transition annotations in italic along arrow paths
- Center: clear serif title with infinity/circular arrow motif

**9.5.2 Branching Flowchart** — For decision flows, validation gates, METHOD phase decisions
- Left-to-right flow with branching decision structures
- Diamond decision points with stipple fill
- Diverging paths labeled in italics

**9.5.3 Layered System Architecture** — For technology stacks, platform architecture, integrations
- Technical cross-section / "exploded view" with structured layers
- Components illustrated with cross-hatching and dense stipple
- Bottom stratum line with tick marks (geological diagram style)

**9.5.4 Performance and Scientific Charts** — For ROI, progress metrics, data-driven content
- Precise ruled axes with tick marks and typeset labels
- Heavy stepped data lines with dense black data-point circles
- Target thresholds as horizontal dashed lines in typeset italics
- Area beneath data lines filled with stipple shading

### 9.6 Current METHOD Images

| Fig. | Phase | File | Archetype |
|------|-------|------|-----------|
| 1 | Overview | `public/images/services/hero-method.webp` | Iterative circular (§9.5.1) |
| 2 | Discover | `public/images/services/hero-method-discover.webp` | Radial cardinal diagram |
| 3 | Experiment | `public/images/services/hero-method-experiment.webp` | Branching flowchart (§9.5.2) |
| 4 | Engineer | `public/images/services/hero-method-engineer.webp` | Layered architecture (§9.5.3) |
| 5 | Optimize | `public/images/services/hero-method-optimize.webp` | Performance chart (§9.5.4) |

All images: 1440×803px, WebP, pure B&W, under 200KB.

### 9.7 METHOD Image Processing

- **Generation tool:** Nana Banana (ChatGPT image generation)
- **Prompts:** See `method-illustration-prompts.md`
- **JPEG/WebP quality:** 90+ (not standard 82) — preserves stipple shading and fine linework
- **Naming:** `hero-method-{phase}.webp` for hero use; `method-{subject}-{variant}.{ext}` for inline use

---

## 10. Image Processing & Naming

### 10.1 Processing Workflow

Every image added to any DS channel must be resized and optimized. Never publish raw LLM outputs or unprocessed uploads.

**Standard workflow (macOS):**

```bash
# 1. Resize to target width (example: hero at 1440px)
sips --resampleWidth 1440 input.png --out /tmp/resized.png

# 2. Convert to WebP (quality 82 for standard, 90+ for METHOD illustrations)
cwebp -q 82 /tmp/resized.png -o output.webp

# 3. Verify file size
ls -la output.webp  # Must be under target for its role
```

**OG images stay PNG** (social platforms handle PNG better):
```bash
pngquant --quality=80-95 --speed 1 --force --output output.png input.png
```

### 10.2 Dimensions by Role (All Channels)

| Role | Max Width | Max File Size | Format |
|------|-----------|---------------|--------|
| Hero / banner | 1440px | 200 KB | WebP |
| Section content | 1280px | 150 KB | WebP |
| Blog inline | 960px | 100 KB | WebP |
| Card thumbnail | 640px | 60 KB | WebP |
| OG / social preview | 1200×630 | 300 KB | PNG |
| Team headshot | 400px | 40 KB | WebP |
| Logo / icon | 200px | 15 KB | SVG preferred |
| LinkedIn post | 1200px | 500 KB | PNG |
| LinkedIn carousel | 1080px | 500 KB | PNG |
| Presentation graphic | 1920px | 1 MB | PNG |
| Email header | 600px | 100 KB | PNG or JPEG |

### 10.3 Naming Convention

**Pattern:** `{type}-{subject}-{variant}.{ext}`

| Prefix | Use Case | Example |
|--------|----------|---------|
| `hero-` | Hero section images | `hero-healthcare-tablet.webp` |
| `img-` | Section content images | `img-data-dashboard.webp` |
| `cs-` | Case study assets | `cs-guardian-ipad-mockup.png` |
| `logo-` | Client/partner logos | `logo-office-depot.svg` |
| `icon-` | UI/feature icons | `icon-blueprint.png` |
| `photo-` | Team/event photos | `photo-team-retreat.jpg` |
| `bg-` | Background/decorative | `bg-pattern-dots.svg` |
| `method-` | METHOD diagrams | `method-iterative-cycle.webp` |
| `og-` | Social preview images | `og-healthcare.png` |
| `li-` | LinkedIn graphics | `li-quote-card-clinician-burden.png` |
| `slide-` | Presentation graphics | `slide-case-study-results.png` |

**Rules:**
- Always lowercase, kebab-case
- No generic names (`image-1.png`, `Untitled-design-5.png`, `Screenshot_2.png`)
- No WordPress dimension suffixes (`-768x768`, `-1024x576`)
- No hash filenames
- Include variant suffix when multiple versions exist: `-black`, `-white`, `-color`
- Logo variants: `logo-{company}-black.svg`, `logo-{company}-white.svg`

---

## 11. Quality Control

### 11.1 Approval Checklist

Before adding any image to any channel:

**Must pass all:**
- [ ] Is the image type appropriate for its context? (§8)
- [ ] Has it been resized per the standard? (§10.1)
- [ ] Is the file under the target size for its role? (§10.2)
- [ ] Does it follow the naming convention? (§10.3)
- [ ] Does it work at thumbnail size (distinct from neighbors)?
- [ ] Would a CIO share this page/post/deck?
- [ ] Does it communicate the article's **argument**, not just topic? (for blog heroes)
- [ ] For METHOD illustrations: pure black-on-white, no gray washes, no color? (§9.2)

**Must fail all:**
- [ ] Could this image be on any competitor's site?
- [ ] Does it feel like a SaaS ad?
- [ ] Is it a raw, unprocessed LLM output?
- [ ] Is the file over 300KB?
- [ ] Is it wider than 1440px?
- [ ] Does it rely on glow effects?

### 11.2 Thumbnail Differentiation

At card grid size, images must be instantly distinguishable from neighbors.

**Checklist:**
- [ ] Different dominant color from adjacent cards
- [ ] Different composition type (overhead vs scene vs lifecycle)
- [ ] Different focal artifact shape
- [ ] Readable at 300×170px

**Common failure:** Two blog posts using the same flat-vector desk composition with the same blue accent.

### 11.3 Image Debt Tracking

Post-launch cleanup items (site live on Netlify as of Feb 2026):

**Remaining:**
1. File renaming — Many images still have WP-era names. Rename incrementally.
2. PNG-to-WebP conversion — Requires HTML reference updates. Batch operation.
3. Duplicate image cleanup — Several images exist in multiple locations.
4. Case study hero standardization — Inconsistent dimensions and some oversized files.

---

# Part 3: Digital Channel Standards

---

## 12. Website

### 12.1 Design System Summary

The DS website uses Tailwind CSS (CDN) with a custom color/font configuration. All pages share a common design system.

**Section Pattern:**
- Full-width backgrounds alternating `bg-white` / `bg-dsGray`
- Content constrained to `max-w-screen-xl mx-auto` (1280px)
- Section padding: `py-20 px-6` (80px vertical, 24px horizontal)

**Cards:**
- Standard: `rounded-xl border border-gray-200 p-6 hover:border-dsBlue hover:shadow-sm`
- Image cards: `rounded-xl overflow-hidden border border-gray-200` with `aspect-video object-cover` image and `p-6` body
- Equal height via flexbox (cards in grids match tallest card)

**Buttons (3 tiers):**
1. **Primary filled:** `bg-dsBlue text-white px-6 py-3 rounded-full font-medium hover:bg-dsBlack` — normal case
2. **Outline:** `border-2 border-dsBlack text-dsBlack px-6 py-3 rounded-full font-medium hover:bg-dsBlack hover:text-white` — UPPERCASE
3. **Text link:** `text-dsBlue font-semibold text-sm uppercase tracking-wider` — with → arrow

**Labels:** `text-xs font-medium text-dsBlue uppercase tracking-wider`

**Pills:** `inline-block bg-dsBlue/10 text-dsBlue text-xs font-medium px-3 py-1 rounded-full uppercase tracking-wider`

### 12.2 Component Inventory

The site uses 24 component patterns. Each has a live reference page and a full HTML template in the web implementation companion.

| # | Component | Best Example Page |
|---|-----------|------------------|
| 1 | Dark hero header | `healthcare/index.html` |
| 2 | Content + Image (right/left) | `healthcare/index.html` |
| 3 | Client logo ribbon | `healthcare/index.html` |
| 4 | Case study cards / carousel | `healthcare/index.html` |
| 5 | Case study list grid | `case-studies/index.html` |
| 6 | Capabilities / feature grid | `ai-machine-learning/index.html` |
| 7 | Horizontal boxes | `healthcare/capabilities/index.html` |
| 8 | Three-column cards with logos | `case-studies/index.html` |
| 9 | C13 list (image cards) | `blog/index.html` |
| 10 | Plans / pricing cards | `services/index.html` |
| 11 | Cards 1-3 width | `healthcare/index.html` |
| 12 | Process line / timeline | `services/blueprint/index.html` |
| 13 | Framework lists | `healthcare/capabilities/index.html` |
| 14 | Testimonial quote (single) | Case study pages |
| 15 | Testimonial carousel | `healthcare/index.html` |
| 16 | FAQ accordion | `healthcare/ai-agents/intelligent-scheduling/` |
| 17 | Services list / tabbed accordion | `services/index.html` |
| 18 | Condensed content / tabs | `healthcare/capabilities/ai-integration/` |
| 19 | CTA banners | `services/blueprint/index.html` |
| 20 | Next page navigation | `healthcare/ai-agents/intelligent-scheduling/` |
| 21 | Benefits & images / icon cards | `services/blueprint/index.html` |
| 22 | Dividers | Various |
| 23 | Process timeline | `services/blueprint/index.html` |
| 24 | Reference page mapping | See web companion §6.24 |

**Full HTML templates and class strings:** See `web-implementation.md` §6.

### 12.3 Video & Animation

| Format | Use Case | Max Size |
|--------|----------|----------|
| GIF | Short UI animations (3-5 sec) | 500 KB |
| MP4 (H.264) | Product demos, walkthroughs | Host on Cloudflare R2 |
| YouTube embed | Long-form video | Privacy-enhanced: `youtube-nocookie.com` |
| Vimeo embed | Premium portfolio video | Same lazy-loading pattern |

**Never:** Commit video files to Git. Autoplay with sound. Embed without `loading="lazy"`.

### 12.4 SEO Principles

- Every page: `<title>` (< 60 chars), `meta description` (120-160 chars), `canonical` (production URL)
- Open Graph tags complete (title, description, url, image, site_name)
- JSON-LD structured data per page type (Organization, Service, Article, BlogPosting, FAQ)
- One `<h1>` per page, logical heading hierarchy
- Descriptive `alt` text on all images
- Internal links with descriptive anchor text (3-5 per page)
- Allow all major crawlers including GPTBot, ClaudeBot, PerplexityBot

**Full SEO implementation:** See `web-implementation.md` §15.

---

## 13. LinkedIn

### 13.1 Two Accounts, Two Voices

| Account | Voice | Frequency | Purpose |
|---------|-------|-----------|---------|
| **Bob Klein (personal)** | Opinionated, story-driven, first person | 1x/week | Thought leadership, relationship building |
| **DS Company Page** | Expert, generous, data-backed | 1x/week | Brand authority, content distribution |

See §6 for full voice profiles.

### 13.2 Image Specifications

| Type | Dimensions | Aspect Ratio | Format | Notes |
|------|-----------|-------------|--------|-------|
| Profile image | 400×400 | 1:1 | PNG | Current: DS wordmark on white |
| Company cover | 1128×191 | ~6:1 | PNG | Black bg, pixel extraction shapes, blue/teal accents |
| Personal cover | 1584×396 | 4:1 | PNG | Same visual language as company cover |
| Single post (square) | 1200×1200 | 1:1 | PNG | High engagement format |
| Single post (landscape) | 1200×627 | ~1.91:1 | PNG | Standard format |
| Carousel slide | 1080×1350 | 4:5 (portrait) | PDF or PNG | Best engagement format |

### 13.3 Post Graphic Templates

**Quote Card**
- Background: dsBlack (#050505)
- Large pull quote in white Inter Bold
- Attribution line below (name, title, company)
- dsBlue accent bar (left edge or bottom)
- DS logo small, bottom-right, white

**Data Callout**
- Background: white or dsGray
- Single metric large (dsBlue, Inter ExtraBold, 72pt+)
- Context line below (gray-600, Inter Regular)
- Source attribution at bottom
- Minimal design — one number, one idea

**Framework Graphic**
- 2-4 column comparison or process
- Muted palette, dsBlue highlights on the recommended option
- Header row in dsBlack
- Clean grid lines (gray-200)
- Based on the blog hero "argument over topic" principle

**Case Proof**
- Lead metric (dsBlue, large)
- One-line context ("across 20,000+ patients")
- Client industry tag (not client name unless approved)
- dsBlue accent
- Links to full case study

### 13.4 Carousel Standards

| Slide | Content | Design |
|-------|---------|--------|
| Cover (slide 1) | Hook title + topic context | dsBlack bg, white text, dsBlue accent |
| Content (slides 2-N) | One idea per slide, numbered | White bg, consistent header strip (dsBlue), body text in dsBlack |
| CTA (final slide) | Clear next step + URL | dsBlue bg, white text, DS logo |

**Rules:**
- 5-10 slides per carousel (sweet spot: 7)
- Each content slide has ONE idea — not a wall of text
- Consistent header strip across all content slides
- Page numbers on each slide
- Cover slide must hook attention without requiring swipe

### 13.5 Post Format Summary

Six formats for DS LinkedIn content (full details in `content-strategy.md` §4):

1. **Narrative Arc** — Bob's voice. Personal story → lesson → DS capability proof
2. **Contrarian Take** — Bold statement that challenges industry conventional wisdom
3. **Case Proof** — Lead with metric, expand with context, link to full case study
4. **Framework Share** — Teach a mental model or evaluation framework
5. **Industry Observation** — Timely commentary on healthcare/AI news
6. **Behind the Build** — How we solved a specific technical challenge

### 13.6 Anti-Patterns

Never:
- Emoji walls (3+ emoji in a row, or emoji as bullet points)
- "Agree?" bait or engagement farming
- Generic stock photos as post images
- Canva templates with multiple fonts/colors
- "I'm humbled to announce..." humblebrags
- Reposting content without adding original commentary
- Hashtag stuffing (max 3-5 relevant hashtags)
- Tagging people who aren't mentioned in the content

---

## 14. Email Marketing

### 14.1 Email Layout

| Element | Specification |
|---------|--------------|
| Max width | 600px (centered) |
| Background | White (#FFFFFF) |
| Side padding | 20px |
| Section spacing | 24-32px between content blocks |

### 14.2 Typography

Email clients do not reliably support web fonts. Use the system font stack:

```
font-family: Arial, Helvetica, sans-serif;
```

| Element | Size | Weight | Color |
|---------|------|--------|-------|
| Heading | 24-28px | Bold | dsBlack (#050505) |
| Subheading | 18-20px | SemiBold (600) | dsBlack |
| Body | 16px | Regular | #4B5563 (gray-600) |
| Caption / preheader | 14px | Regular | #6B7280 (gray-500) |

### 14.3 CTA Buttons

```
background-color: #304FFF;  /* dsBlue */
color: #FFFFFF;
padding: 12px 24px;
border-radius: 24px;        /* rounded-full */
font-weight: 500;
font-size: 14px;
text-decoration: none;
display: inline-block;
```

For dark-background email sections: white button with dsBlue text.

### 14.4 Header / Banner

- Width: 600px (full email width)
- DS logo: top-left or centered, white version on dsBlack/dsBlue background
- Optional hero image: 600px wide, under 100KB
- Keep header height under 200px — don't push content below the fold

### 14.5 Email Signature Standard

Reference the existing Word-based email signature templates in the stationery assets. Standard fields:

```
Name
Title | Digital Scientists
phone | email
digitalscientists.com
```

- DS wordmark (small, linked to website)
- No social media icon rows (keeps signature clean)
- No banner images or promotional graphics in signatures

### 14.6 Digital Letterhead

Reference the existing Word template. Standard layout:
- DS wordmark top-left
- Address and contact info in footer
- Clean white body area
- dsBlue accent lines (header rule, footer rule)

### 14.7 Anti-Patterns

Never:
- Custom web fonts in email HTML (they won't render)
- Complex multi-column layouts (breaks on mobile email clients)
- Dark-mode-breaking colors (test with both light and dark)
- Images without alt text (many clients block images by default)
- Embedding video (use thumbnail + play button linking to hosted video)
- Background images on buttons (not supported in Outlook)

---

# Part 4: Print & Physical Channel Standards

---

## 15. Presentations (Google Slides / PowerPoint)

### 15.1 Slide Dimensions

Standard: **16:9 (1920×1080px)**

All DS presentations use widescreen 16:9 format. Never 4:3.

### 15.2 Background Colors by Slide Type

| Slide Type | Background | Text Color | When to Use |
|------------|-----------|------------|-------------|
| Content / body | White (#FFFFFF) | dsBlack | Default for most slides |
| Section divider | dsBlack (#050505) | White | Between major sections |
| Title slide | dsBlack (#050505) | White | First slide |
| CTA / contact | dsBlue (#304FFF) | White | Final slide |
| Feature highlight | dsGray (#F5F5F5) | dsBlack | Optional variety |

### 15.3 Typography

| Element | Font | Size | Weight |
|---------|------|------|--------|
| Slide title | Inter | 36-44pt | Bold (700) |
| Slide subtitle | Inter | 20-24pt | Regular (400) |
| Body text | Inter | 18-24pt | Regular (400) |
| Caption / footnote | Inter | 14pt | Regular (400) |
| Data / metrics | Inter or Roboto Mono | 44-72pt | ExtraBold (800) |
| Labels | Inter | 12-14pt | Medium (500), uppercase |

**All headings:** letter-spacing -0.02em (consistent with web).

### 15.4 Standard Slide Types

Derived from the Healthcare Capabilities 2026 deck and PowerPoint sales templates:

**Title Slide**
- dsBlack background
- DS wordmark (white, top-left or centered)
- Presentation title (Inter Bold, 44pt, white)
- Subtitle / date (Inter Regular, 20pt, gray-400)
- Optional: pixel extraction shapes as accent (bottom-right, low opacity)

**Value Proposition Slide ("Top 5 Reasons")**
- White background
- Numbered list (dsBlue numbers, dsBlack text)
- Each reason: bold headline + one-line explanation
- Icon optional (dsBlue, simple line icon)

**Service Overview Slide**
- White or dsGray background
- 2×3 or 3×2 icon + description grid
- Icons: simple line style, dsBlue on white circle or square
- Brief description under each (2-3 lines max)

**Case Study Slide**
- Challenge → Approach → Results format
- Lead with the metric (dsBlue, 44pt+, prominent)
- Challenge: 2-3 bullet points
- Results: 2-3 metrics with context
- Optional: product screenshot (right column)

**Team / Capability Slide**
- Headshots: rounded-full, consistent size
- Name + title + brief specialization
- Or: capability list with checkmarks

**CTA / Contact Slide**
- dsBlue background
- "Let's talk" or similar headline (white, centered)
- Bob Klein — CEO, bob@digitalscientists.com
- Nick Alexander — COO, nick@digitalscientists.com
- DS logo (white, bottom)

### 15.5 Chart & Data Visualization Colors

| Role | Color |
|------|-------|
| Primary data series | dsBlue (#304FFF) |
| Secondary data series | dsTeal (#26D9C4) |
| Tertiary data series | dsLime (#D1F259) |
| Neutral / comparison | Gray-400 (#9CA3AF) |
| Axis lines, grid | Gray-200 (#E5E7EB) |
| Labels | dsBlack (#050505) |

**Rules:**
- Maximum 4 colors per chart
- Always label data directly (no legend if avoidable)
- Use Roboto Mono for data labels on charts

### 15.6 Pixel Extractions in Presentations

Allowed on:
- Section divider slides (dsBlack background)
- Title slide accent elements
- Decorative elements at low opacity

Not allowed on:
- Content slides (they compete with information)
- Charts or data slides

Colors: dsBlue, dsTeal, dsLime, white only. Always on dark backgrounds.

### 15.7 Anti-Patterns

Never:
- WordArt or decorative text effects
- Stock clip art or generic icons
- Gradient backgrounds (solid colors only)
- More than 3 bullet points per section on a slide
- Walls of text (if you need paragraphs, it should be a document, not a slide)
- Transition animations beyond simple fade
- Sound effects
- Multiple fonts on one slide

---

## 16. Sales Collateral

### 16.1 One-Pagers

| Element | Specification |
|---------|--------------|
| Size | 8.5×11" (US Letter) |
| Margins | 0.75" all sides |
| Typography | Inter (same scale as slides, adapted for print) |
| Primary accent | dsBlue |
| Layout | Single column or 2-column |

**Structure:**
1. Header: DS logo + document title + dsBlue accent bar
2. Value proposition (1-2 sentences, bold)
3. Key capabilities (3-5, with icons or checkmarks)
4. Proof point / case study callout (metric + context)
5. CTA: "Let's talk" with contact info

### 16.2 Case Study PDFs

Follow the same **Challenge → Approach → Results** format used on the website and in slide decks.

| Section | Content |
|---------|---------|
| Header | DS logo + "Case Study" label + client industry |
| Hero metric | The single most impressive result (large, dsBlue) |
| Challenge | 2-3 bullet points describing the problem |
| Approach | What DS did, which METHOD phases applied |
| Results | 3-5 metrics with context |
| Tech stack | Technologies used (tag format) |
| CTA | Contact info, link to full case study on website |

**Rules:**
- Lead with the metric, not the client name
- Include real screenshots or product images when available
- 1-2 pages maximum
- Can use METHOD diagram as accent element

### 16.3 Proposals

| Element | Standard |
|---------|---------|
| Cover page | DS wordmark (centered or top-left), proposal title, client name, date, dsBlue accent |
| Section headers | Inter Bold, dsBlue underline or dsBlue left border |
| Body text | Inter Regular, 11-12pt, 1.5 line height |
| Page numbers | Bottom-center, Inter Regular, gray-500 |
| METHOD integration | Include METHOD diagram where relevant (Discover → Experiment → Engineer → Optimize) |

**Anti-patterns:**
- Word/Google Docs default formatting (Calibri, Times New Roman)
- Clip art or generic graphics
- Dense paragraphs with no visual hierarchy
- Inconsistent heading styles

---

## 17. Stationery

### 17.1 Business Cards

Reference the existing InDesign templates in the stationery assets.

| Element | Specification |
|---------|--------------|
| Size | 3.5×2" (standard US) |
| Front | DS wordmark + name + title + contact info |
| Back | dsBlack or dsBlue background, optional pixel extraction accent |
| Font | Inter (name: SemiBold, title/contact: Regular) |
| Font sizes | Name: 9pt, Title: 7pt, Contact: 7pt |
| Print | Matte finish preferred |

### 17.2 Digital Letterhead

Reference the existing Word template.

| Element | Specification |
|---------|--------------|
| Header | DS wordmark (top-left), dsBlue rule below |
| Footer | Address, phone, email, website — gray-500, 8pt |
| Body | Inter Regular, 11pt, 1.5 line height |
| Margins | 1" top/bottom, 0.75" sides |

### 17.3 Note Cards / Thank-You Cards

| Element | Specification |
|---------|--------------|
| Size | A2 (4.25×5.5") or A6 |
| Front | DS wordmark centered, dsBlue accent element |
| Inside | Blank (handwritten message area) |
| Back | Address + website, small text |
| Stock | Heavy card stock, matte finish |

### 17.4 Anti-Patterns

Never:
- Non-brand fonts (Calibri, Times New Roman, Helvetica Neue)
- Color deviations from the defined palette
- Low-resolution logo reproductions
- Glossy or metallic finishes (matte is the DS aesthetic)

---

## 18. Signage & Environmental

### 18.1 Exterior Signage

Reference the Alpharetta office building signage.

| Element | Specification |
|---------|--------------|
| Content | DS wordmark only (no tagline, no pixel extractions) |
| Material | Brushed metal or matte black on building facade |
| Illumination | Backlit or edge-lit (not front-lit neon) |
| Clear space | Minimum 2× logo height on all sides |

### 18.2 Interior Branding

| Element | Specification |
|---------|--------------|
| Window banners | Large-format prints with pixel extraction shapes on dsBlack |
| Lobby signage | DS wordmark, dimensional letters preferred |
| Conference rooms | Optional: METHOD phase names as room names |
| Common areas | METHOD diagram or brand-color accent walls |

### 18.3 Rules

- Exterior signage uses the wordmark ONLY — no pixel extractions unless on dark substrate
- Interior allows more creative brand expression (pixel extractions, color accents)
- All signage must use the exact brand colors (provide Pantone references for print production)
- Never use the logo at less than minimum size, even on large signage (scale proportionally)

---

# Part 5: Appendices

---

## A. Brand Asset Inventory

### Logos

| Asset | File Path | Format |
|-------|-----------|--------|
| Primary logo (black) | `public/ds-logo-black.svg` | SVG |
| Primary logo (white) | `public/ds-logo-white.png` | PNG |
| Favicon | `public/favicon.svg` | SVG |

### Fonts

| Font | Source | Weights |
|------|--------|---------|
| Inter | Google Fonts | 300, 400, 500, 600, 700, 800 |
| Roboto Mono | Google Fonts | 400, 500 |

### OG Image Template

| Asset | File Path |
|-------|-----------|
| OG generator script | `scratchpad/generate_og_images.py` |

### METHOD Illustrations

| Asset | File Path |
|-------|-----------|
| Overview | `public/images/services/hero-method.webp` |
| Discover | `public/images/services/hero-method-discover.webp` |
| Experiment | `public/images/services/hero-method-experiment.webp` |
| Engineer | `public/images/services/hero-method-engineer.webp` |
| Optimize | `public/images/services/hero-method-optimize.webp` |
| Prompts | `method-illustration-prompts.md` |

### Stationery Templates

| Asset | Notes |
|-------|-------|
| Business card | InDesign template (stationery assets) |
| Email signature | Word template (stationery assets) |
| Digital letterhead | Word template (stationery assets) |

### Presentation Templates

| Asset | Notes |
|-------|-------|
| Healthcare Capabilities 2026 | 16-page PDF, most current deck |
| Sales deck templates | PowerPoint (~15 client case studies) |

### LinkedIn Assets

| Asset | Notes |
|-------|-------|
| Company cover photos | 3 variants, dsBlack + pixel extractions |
| Personal cover photos | 3 variants, matching style |
| Profile image | DS wordmark on white |

---

## B. Quick Reference Card

### Colors
| Token | Hex | Print (Pantone) |
|-------|-----|-----------------|
| dsBlue | `#304FFF` | PMS 2728 C (closest) |
| dsBlack | `#050505` | Process Black |
| dsGray | `#F5F5F5` | Cool Gray 1 C |
| dsTeal | `#26D9C4` | PMS 3262 C (closest) |
| dsLime | `#D1F259` | PMS 381 C (closest) |

### Fonts
- **Primary:** Inter (300–800)
- **Mono:** Roboto Mono (400, 500)
- **Email fallback:** Arial, Helvetica, sans-serif
- **All headings:** letter-spacing -0.02em

### Key Dimensions by Channel

| Channel | Key Dimension |
|---------|--------------|
| Website section | max-width 1280px, py-20 px-6 |
| Website hero | 1440×810, bg-dsBlack for top-of-funnel |
| Website card | rounded-xl, border gray-200, p-6 |
| Blog hero | 1440×810, 16:9, WebP, < 200KB |
| OG image | 1200×630, PNG, < 300KB |
| LinkedIn post | 1200×1200 (square) or 1200×627 |
| LinkedIn carousel | 1080×1350 (4:5) |
| Email | 600px max width |
| Slides | 1920×1080 (16:9) |
| Business card | 3.5×2" |

---

## C. Brand Evolution Notes

### What Changed from 2019 Brand Guidelines

| Element | 2019 | Current (2026) | Rationale |
|---------|------|----------------|-----------|
| Typography | RM Pro (Regular, Light, Bold) | Inter (300-800) + Roboto Mono (400, 500) | RM Pro was a licensed font with limited weights. Inter provides the full weight range needed for web + print, is free, and has excellent web performance. |
| Secondary colors | dsBlue, Middle Blue (#3B86E5), dsTeal, dsLime | dsBlue, dsTeal, dsLime | Middle Blue (#3B86E5) dropped — too close to dsBlue, caused confusion in digital contexts. |
| Photography | Abstract details, dynamic stills, culture shots, product photos | Editorial illustration (blog heroes), METHOD textbook diagrams, real product screenshots | Stock photography replaced by distinctive LLM-generated illustrations that are uniquely DS. |
| Positioning | "Experience lab that accelerates innovation for growth" (general tech consultancy) | "Reduces clinician burden and recovers lost revenue" (healthcare-first) | Company pivoted to healthcare specialization. Positioning now reflects the actual client base and service focus. |
| Pixel extractions | Used broadly across all collateral | Preserved for LinkedIn covers, signage, presentation dividers only | Website moved to clean Tailwind layouts with editorial illustration. Pixel extractions reserved for off-web brand accents. |
| Logo | Stacked wordmark, B&W | Same + "DS" monogram favicon | Favicon added for browser tab identification. Core wordmark unchanged. |
| Clear space | 0.69in print / 50px digital | Same | Unchanged. |

### What Carries Forward Unchanged

- Primary logo: "DIGITAL SCIENTISTS" stacked wordmark
- Primary colors: Black + White
- dsBlue (#304FFF) as primary accent
- dsTeal (#26D9C4) and dsLime (#D1F259) as secondary accents
- Pixel extraction shapes (L-shaped, square, quarter-circle) for off-web use
- Logo clear space and minimum size rules
- Roboto Mono as monospace companion

---

## D. Revision History

- **2026-03-07: v1.0** — Initial unified brand guide. Consolidated from `ds-design-standard.md`, `ds-visual-standard.md`, and `ds-blog-hero-image-standard.md`. Added new channel sections: LinkedIn (§13), Email (§14), Presentations (§15), Sales Collateral (§16), Stationery (§17), Signage (§18). Incorporates brand elements from the 2019 Brand Guidelines PDF, Healthcare Capabilities 2026 deck, LinkedIn assets, stationery templates, and office signage.

---

*End of Document.*
