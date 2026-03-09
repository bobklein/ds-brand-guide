# DS METHOD Illustration Prompts

> **Tool:** Nana Banana (ChatGPT image generation)
> **Standard:** See `brand-guide.md` §9 for the full aesthetic specification
> **Generated images:** `public/images/services/hero-method-{phase}.webp`

One prompt per METHOD phase. Each prompt produces a single figure plate in the 1950s-60s scientific textbook style defined in the visual standard. Prompts are stored here for reproducibility and consistency.

---

## Reference: Current METHOD Images

| Fig. | Phase | File | Dimensions | Size | Archetype |
|------|-------|------|-----------|------|-----------|
| 1 | Overview | `hero-method.webp` | 1440x803 | 58 KB | Iterative circular (§10.5.1) |
| 2 | Discover | `hero-method-discover.webp` | 1440x803 | 100 KB | Radial cardinal diagram |
| 3 | Experiment | `hero-method-experiment.webp` | 1440x803 | 97 KB | Branching flowchart (§10.5.2) |
| 4 | Engineer | `hero-method-engineer.webp` | 1440x803 | 152 KB | Layered architecture (§10.5.3) |
| 5 | Optimize | `hero-method-optimize.webp` | 1440x803 | 186 KB | Performance chart (§10.5.4) |

**All images:** Landscape, 1440x803px, WebP, pure black (#000000) on pure white (#FFFFFF), under 200KB.

**File naming:**
- Hero/service use: `hero-method-{phase}.webp` (stored in `public/images/services/`)
- OG images: `method--{phase}.png` for phases, `method.png` for overview (stored in `public/images/og/`)
- Blog inline/new diagrams: `method-{subject}-{variant}.{ext}`

**Processing:** JPEG quality 90+ / WebP quality 88+ to preserve stipple and fine linework. Standard 82 quality causes stipple dots to blur.

**Contrast escalation tip:** If Nana Banana results skew warm or gray, append to the prompt: "Render as if this is a freshly printed page from a Taschen monograph on technical illustration — gallery-quality reproduction, not an archival scan."

---

## Fig. 1 — METHOD Overview (Full Cycle)

**File:** `public/images/services/hero-method.webp`
**Archetype:** Refined Iterative Circular Diagram (§10.5.1)

```
Generate a formal process diagram in the visual style of a figure plate from a 1950s–60s scientific or engineering textbook. This should look like a published illustration — precise, informational, and elegant in its restraint.

CRITICAL — Contrast and tone: The background must be pure, flat white (#FFFFFF) — not cream, not ivory, not off-white, not parchment. Think bright copy paper under fluorescent light. The ink must be dense, saturated true black (#000000) — not gray, not faded, not washed out. The ink should look freshly printed with full coverage, like a first-run letterpress impression where the type bit deep into the paper. There should be no texture, grain, or noise in the white areas — the white is clean and absolute. The contrast ratio between ink and paper should be maximum. This is not a vintage scan — it is a pristine original print.

Layout: Landscape orientation on pure white paper. At the bottom, centered, a formal figure caption in italic serif type: "Fig. 1 — The four-phase iterative method for systems development, showing the cyclical relationship between discovery, experimentation, engineering, and optimization."

The diagram: Four phases arranged on a precise circle, evenly spaced at 90° intervals, connected by curved arrows forming a continuous clockwise loop:

- DISCOVER (12 o'clock) — Icon: a magnifying glass over a document, rendered in fine pen-and-ink stipple and line work (cross-hatching for shadow, fine contour lines). Label "DISCOVER" in small, spaced serif capitals below.
- EXPERIMENT (3 o'clock) — Icon: an Erlenmeyer flask on a ring stand, same pen-and-ink style. Label below.
- ENGINEER (6 o'clock) — Icon: interlocking gears in partial cutaway/section view with proper engineering cross-hatching on cut surfaces. Label below.
- OPTIMIZE (9 o'clock) — Icon: a dial gauge with needle and graduated scale, drawn as a technical instrument illustration. Label below.

Connecting arrows are elegant, thin, consistent-weight curved lines forming a perfect circle with small refined arrowheads. Between each phase, along the arrow path, a small annotation in italic: "identify → hypothesize → build → measure →" describing the transition activity.

At the center of the circle, in clean serif font: "ITERATIVE PROCESS" with a small circular arrow motif beneath it.

Rendering: Pure black ink on pure white. Every stroke, letter, and mark is dense black with full ink saturation — no gray tones except where stipple dots intentionally create tonal gradation in the illustrations. All illustration in fine pen-and-ink technique: stipple shading, cross-hatching for depth, clean contour lines. Reference the style of patent drawings or Encyclopaedia Britannica diagrams. Typography is typeset serif (Garamond, Caslon, or Century Schoolbook) — small caps for labels, italic for annotations. Fine-line ruled borders (thin-thick-thin triple rule). No color. No handwriting. No digital vector flatness. No yellowing. No paper texture. No faded appearance.
```

---

## Fig. 2 — Discover

**File:** `public/images/services/hero-method-discover.webp`
**Archetype:** Radial cardinal diagram (central hub with 4 branches)

```
Generate a formal process diagram in the visual style of a figure plate from a 1950s–60s scientific or engineering textbook.

CRITICAL — Contrast and tone: Background must be pure flat white (#FFFFFF). All ink must be dense saturated true black (#000000). No cream, no ivory, no gray washes. The ink looks freshly printed — full coverage, zero fade.
White areas are perfectly clean with no texture or grain. Maximum contrast ratio. This is a pristine original, not a reproduction or scan.

All illustration rendered in fine pen-and-ink technique with stipple shading and cross-hatching. Typography is typeset serif — small caps for labels, italic for annotations and captions.

Layout: Landscape orientation. At bottom, centered caption in italic serif: "Fig. 2 — The Discovery phase: a structured research process for identifying stakeholder needs, mapping existing processes, and surfacing critical pain points."

The diagram: A central element representing "RESEARCH" — drawn as a detailed pen-and-ink illustration of an open ledger or field notebook with a magnifying glass resting on it. Dense stipple shading on the page surfaces, bold cross-hatching on the magnifying glass handle.

Radiating outward from this central illustration, four branches extend to the cardinal directions, each connected by thin ruled lines with small arrowheads:

- Top: "STAKEHOLDERS" — A small pen-and-ink illustration of two figures at a table in profile (like a woodcut vignette), with the label in spaced small caps. Annotation in italic along the connecting line: "conduct interviews, observe workflows"
- Right: "PROCESS MAPPING" — A small illustration of a flowchart on a clipboard, drawn in miniature with visible boxes and arrows. Label in small caps. Annotation: "document current state, identify handoffs"
- Bottom: "PAIN POINTS" — A small illustration of a cracked or fractured beam under load (an engineering metaphor for stress/failure points), with fine line work showing the fracture pattern. Label in small caps. Annotation: "surface friction, quantify impact"
- Left: "REQUIREMENTS" — A small illustration of a checklist or specification sheet with checkmarks, rendered in fine detail. Label in small caps. Annotation: "define constraints, establish criteria"

Thin dashed lines connect the four outer elements to each other in a diamond pattern, suggesting their interdependence. Small reference markers (†, ‡, §, ¶) at each node correspond to footnote-style notes in the caption area.

Fine-line ruled border (thin-thick-thin triple rule). No color. No casual handwriting. No faded or washed-out appearance — every mark is bold and definitive.
```

---

## Fig. 3 — Experiment

**File:** `public/images/services/hero-method-experiment.webp`
**Archetype:** Branching Flowchart / Scientific Method Diagram (§10.5.2)

```
Generate a formal process diagram in the visual style of a figure plate from a 1950s–60s scientific or engineering textbook.

CRITICAL — Contrast and tone: Background must be pure flat white (#FFFFFF). All ink must be dense saturated true black (#000000). No cream, no ivory, no gray washes. The ink looks freshly printed — full coverage, zero fade.
White areas are perfectly clean with no texture or grain. Maximum contrast ratio. This is a pristine original, not a reproduction or scan.

All illustration rendered in fine pen-and-ink technique with stipple shading and cross-hatching. Typography is typeset serif — small caps for labels, italic for annotations and captions.

Layout: Landscape orientation. At bottom, centered caption in italic serif: "Fig. 3 — The Experimentation phase: a hypothesis-driven cycle of building, testing, and evaluating outcomes to validate or redirect approach."

The diagram: A left-to-right flow with a branching decision structure, resembling a classic scientific method diagram:

Starting point (left): "HYPOTHESIS" in small caps, enclosed in a rectangle with a fine ruled border. Next to it, a small pen-and-ink illustration of a hand writing in a lab notebook (seen from above, stipple-shaded).

Arrow flows right to: A detailed pen-and-ink illustration of a laboratory test setup — an Erlenmeyer flask on a ring stand with a Bunsen burner beneath, rendered with bold cross-hatching on the metal stand and dense stipple on the glass. Labeled "TEST" in small caps above.

Arrow flows right to: A diamond (decision point) labeled "EVALUATE" in small caps. Drawn with precise ruled lines, with fine stipple fill to distinguish it from the rectangular elements.

From the diamond, two paths diverge:

- Upper path (arrow up-right): labeled in italic "validated" — leads to "BUILD" in small caps within a rectangle. Beside it, a small illustration of an architectural/structural framework being assembled. Then an arrow to "RESULT" — a rectangle containing a small illustration of a completed document or report with a seal/stamp.
- Lower path (arrow down-right): labeled in italic "invalidated" — leads to "PIVOT" in small caps within a rectangle. Beside it, a small illustration of a compass rose (suggesting reorientation). A curved return arrow loops back from PIVOT to HYPOTHESIS, labeled in italic "reformulate".

Small roman numerals (i, ii, iii, iv) mark the sequence along the primary path.

Fine-line ruled border (thin-thick-thin triple rule). No color. No casual handwriting. Every line and mark at maximum ink density.
```

---

## Fig. 4 — Engineer

**File:** `public/images/services/hero-method-engineer.webp`
**Archetype:** Layered System Architecture (§10.5.3)

```
Generate a formal process diagram in the visual style of a figure plate from a 1950s–60s scientific or engineering textbook.

CRITICAL — Contrast and tone: Background must be pure flat white (#FFFFFF). All ink must be dense saturated true black (#000000). No cream, no ivory, no gray washes. The ink looks freshly printed — full coverage, zero fade.
White areas are perfectly clean with no texture or grain. Maximum contrast ratio. This is a pristine original, not a reproduction or scan.

All illustration rendered in fine pen-and-ink technique with stipple shading and cross-hatching. Typography is typeset serif — small caps for labels, italic for annotations and captions.

Layout: Landscape orientation. At bottom, centered caption in italic serif: "Fig. 4 — The Engineering phase: system architecture showing the structural relationship between presentation, orchestration, service, and data persistence layers."

The diagram: A layered system architecture rendered as a technical cross-section drawing — as if looking at the exploded view of a machine, with each layer clearly delineated:

Layer 1 — Left: "FRONTEND"
A pen-and-ink illustration of a terminal or display screen in three-quarter view, with bold cross-hatching on the casing and dense stipple on the screen surface. Label "FRONTEND" in spaced small caps below. Annotation in italic: "presentation layer"

Arrow flows right (thick ruled line labeled "requests") to:

Layer 2 — Center-left: "API GATEWAY"
Illustrated as a detailed pen-and-ink drawing of a mechanical switchboard or routing junction — a central hub with multiple connection points, drawn with patent-illustration precision. Gears and levers suggested in fine detail. Label in small caps. Annotation: "orchestration layer"

From the gateway, two paths branch (upper and lower), connected by thin ruled lines labeled "routes":

Layer 3 — Center-right: "SERVICES" (two instances)
Each drawn as a small, precise illustration of an interchangeable mechanical module or cartridge — suggesting modularity. Heavy cross-hatching on housings, stipple on interfaces. Labels in small caps, distinguished as "Service A" and "Service B". Annotation: "business logic layer"

Both services connect via arrows (labeled "read/write") to:

Layer 4 — Right: "DATABASE"
Illustrated as a pen-and-ink drawing of a filing cabinet or card catalog in section view — drawers partially open revealing organized index cards within. Bold cross-hatching on the cabinet exterior, detailed interior. Label in small caps. Annotation: "persistence layer"

Along the bottom, a thin ruled line spans the full width with scale-like tick marks dividing the architecture into its named layers, resembling a geological stratum diagram.

Fine-line ruled border (thin-thick-thin triple rule). No color. No casual handwriting. Every stroke fully saturated black.
```

---

## Fig. 5 — Optimize

**File:** `public/images/services/hero-method-optimize.webp`
**Archetype:** Performance and Scientific Charts (§10.5.4)

```
Generate a formal process diagram in the visual style of a figure plate from a 1950s–60s scientific or engineering textbook.

CRITICAL — Contrast and tone: Background must be pure flat white (#FFFFFF). All ink must be dense saturated true black (#000000). No cream, no ivory, no gray washes. The ink looks freshly printed — full coverage, zero fade.
White areas are perfectly clean with no texture or grain. Maximum contrast ratio. This is a pristine original, not a reproduction or scan.

All illustration rendered in fine pen-and-ink technique with stipple shading and cross-hatching. Typography is typeset serif — small caps for labels, italic for annotations and captions.

Layout: Landscape orientation. At bottom, centered caption in italic serif: "Fig. 5 — The Optimization phase: a continuous improvement cycle of measurement, analysis, and refinement, driving system performance toward defined targets."

The diagram in two tiers:

Upper tier — Performance chart:
A detailed pen-and-ink rendering of a scientific chart. Precise ruled axes with tick marks and scale labels in dense black. X-axis labeled in italic "iteration cycle" with roman numerals (I through VIII). Y-axis labeled "performance index." Data shown as a stepped ascending line with small data-point circles at each step, all in heavy black ink. A horizontal dashed line near the top labeled "target threshold." Dense stipple shading beneath the data line to indicate area/progress. The chart lines and labels should be bold and fully saturated.

Lower tier — Process flow:
Three phases arranged left to right, connected by heavy ruled arrows:

- "MEASURE" — A pen-and-ink illustration of a micrometer caliper or dial indicator, rendered with fine mechanical detail (knurled surfaces in dense stipple, graduated scale in hairline marks). Label in small caps below.
- "ANALYZE" — A pen-and-ink illustration of a slide rule lying flat with its scales visible. Bold cross-hatching on the body, fine graduation marks. Label in small caps below.
- "IMPROVE" — A pen-and-ink illustration of a hand adjusting a fine-tuning knob or calibration dial on an instrument panel. Dense stipple on the panel surface, cross-hatching on the knob. Label in small caps below.

A sweeping return arrow curves from IMPROVE back under to MEASURE, forming a continuous loop. Along this return arrow, in italic: "feedback loop — apply learnings to next measurement cycle."

Between the upper and lower tiers, thin vertical dashed lines connect each process step to corresponding regions of the performance chart.

Fine-line ruled border (thin-thick-thin triple rule). No color. No casual handwriting. No faded or vintage-scan appearance. Every mark dense, definitive, and fully black.
```
