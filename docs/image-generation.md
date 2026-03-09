# DS Brand Guide -- Image Generation Reference

**Companion to:** `brand-guide.md` (master brand guide)
**Purpose:** Prompt construction for LLM-generated images -- blog heroes, LinkedIn graphics, METHOD illustrations, and OG images. Read the master brand guide first for visual principles, then use this file when generating images.

---

## Table of Contents

1. [Blog Hero Prompt Construction](#1-blog-hero-prompt-construction)
2. [Visual Style Specification](#2-visual-style-specification)
3. [Scene Selection Guide](#3-scene-selection-guide)
4. [Composition Types Deep Dive](#4-composition-types-deep-dive)
5. [Artifact Layer System](#5-artifact-layer-system)
6. [Visual Storytelling Through State](#6-visual-storytelling-through-state)
7. [Messaging Goals by Article Theme](#7-messaging-goals-by-article-theme)
8. [Approval Checklist & Quality Control](#8-approval-checklist--quality-control)
9. [Prompt Templates & Tools](#9-prompt-templates--tools)
10. [Library Tracking](#10-library-tracking)
11. [LinkedIn Post Image Generation](#11-linkedin-post-image-generation)
12. [METHOD Illustration Reference](#12-method-illustration-reference)
13. [OG Image Generation](#13-og-image-generation)
14. [Supplemental Visual Rules](#14-supplemental-visual-rules)
15. [Philosophy](#15-philosophy)
16. [Revision History](#16-revision-history)

---

## 1. Blog Hero Prompt Construction

Our blog imagery exists to:

- Clarify complex ideas in under 2 seconds
- Reinforce executive credibility
- Reflect disciplined thinking
- Signal structured decision-making
- Support thought leadership without visual noise

Images are not decoration. They are visual summaries of structured reasoning.

### 1.1 The 6-Step Process

Every blog hero image is built through a 6-step process:

1. **Extract the article's argument** -- identify what the article concludes, not just what it covers.
2. **Choose a composition** -- select the physical arrangement that best carries the argument.
3. **Design the artifact layers** -- plan the focal artifact, context artifacts, and environmental details.
4. **Define visual emphasis** -- decide what's brightest, what's muted, where the accent lands.
5. **Write the prompt** -- assemble the prompt using the standard template.
6. **Evaluate the output** -- run through the approval checklist before publishing.

### 1.2 Step 1: Extract the Article's Argument

Before writing any prompt, answer:

- What is the article's **topic**?
- What is the article's **argument** (conclusion)?
- What is the article's **call to action**?
- What **specific vocabulary** does the article use?

This is the most important distinction in the entire standard:

**Topic** = what the article is about.
**Argument** = what the article concludes.

An image that illustrates the topic is generic.
An image that illustrates the argument is specific.

| Article | Topic (Generic) | Argument (Specific) |
|---|---|---|
| Software Development Risk | "Risk exists in software" | "Proactive governance protects ROI" |
| Buy, Build, or Partner | "Three options exist" | "Discovery finds gaps, SaaS falls short, partnering is the path" |
| Platform Modernization | "Legacy systems need updating" | "Architectural validation before migration reduces cost" |

If the image could belong to a different article on the same topic, it is illustrating the topic, not the argument.

Write one sentence before generating: *"After reading this post, the reader should believe that ___."* That sentence is the brief. If you can't write a sharp one-sentence argument, the image will feel generic. Sharpen the argument first.

| Post topic | Wrong (topic) | Right (argument) |
|---|---|---|
| AI in healthcare | Robot with stethoscope | Bar chart: clinical hours recovered before vs. after AI |
| Proof of concept | Lightbulb | Stalled meeting on one side, experiment already running on the other |
| Buy vs. build vs. partner | Person at a crossroads | Decision matrix with two options crossed out, one circled |
| Machine learning explained | Neural network diagram | Child learning vs. model learning -- parallel structure |
| Design sprints | Post-it notes | 5-day timeline with a working prototype at the end |

### 1.3 Step 2: Choose a Composition

- Partnership/collaboration story --> Composition A
- Framework/decision/evaluation story --> Composition B
- Process/lifecycle story --> Composition C
- Executive alignment story --> Composition D
- Check against recent posts for thumbnail differentiation

See [Section 4](#4-composition-types-deep-dive) for full composition descriptions.

### 1.4 Step 3: Design the Artifact Layers

- **Level 1:** What single artifact communicates the argument?
- **Level 2:** What 2-3 artifacts tell the story of how we got here?
- **Level 3:** What 1-2 environmental details add realism?

See [Section 5](#5-artifact-layer-system) for the full artifact layer system.

### 1.5 Step 4: Define Visual Emphasis

- What element should be the brightest/most prominent? (The argument.)
- What elements should be muted? (Rejected options, background context.)
- Where does the accent color land?

Each image must communicate one dominant concept. There must be a single dominant focal point. Everything else supports that focal element.

### 1.6 Step 5: Write the Prompt

Use this template:

```
Clean 16:9 smooth editorial digital illustration, minimal executive tone.
Not comic book, not technical illustration, not graphic novel, not flat vector.
[Composition description -- angle, setting, figures if any].
[Level 1 focal artifact -- detailed description with state signals].
[Level 2 context artifacts -- each with its specific story contribution].
[Level 3 environmental details].
[Visual emphasis instructions -- what's brightest, what's muted].
Muted corporate blues, soft slate grays, warm neutral [surface/background].
Soft directional light, gentle shadows, slight paper texture.
No glowing effects, no neon, no decorative icons, no complex dashboards.
No visible faces. Figures fully from behind.
The tone is executive, disciplined, accountable.
The image should instantly communicate: [one sentence restating the argument].
16:9, 1440x810px.
```

See also [Section 9.1](#91-blog-hero-prompt-template) for the alternate prompt template from the design standard.

### 1.7 Step 6: Evaluate the Output

Run through the approval checklist in [Section 8](#8-approval-checklist--quality-control) before publishing.

---

## 2. Visual Style Specification

### 2.1 Illustration Language

**Smooth editorial digital illustration.** Simplified but realistic -- not cartoonish, not clip-art, not flat vector, not comic book, not technical illustration, not graphic novel, not photorealistic. Reference: Harvard Business Review or MIT Sloan Management Review.

Always include in every prompt: *"Not comic book, not technical illustration, not graphic novel, not flat vector."*

Every image should feel:

- Calm
- Deliberate
- Structured
- Accountable
- Professional

If it feels flashy, dramatic, or busy -- it fails.

See `brand-guide.md` for the full DS visual identity and tone-of-voice principles.

### 2.2 Palette

**Base palette:**
- Muted corporate blues
- Soft slate grays
- Warm neutral backgrounds (cream, linen, off-white)
- Soft shadows
- Low saturation overall

**Status indicators (most saturated elements):**
- Red dots/bars = problem, flagged, unresolved, gap found, risk identified, rejected
- Amber dots = stalled, in review, uncertain, under review, attention needed
- Green dots/bars = working, validated, approved, complete
- Muted blue/slate = neutral data, structure
- Warm cream = backgrounds, lit surfaces
- Gray = not selected, pending, inactive

Status indicators should be the brightest visual elements in the image.

No saturated fills. No bright backgrounds. No color for decoration. Never use neon or glow.

### 2.3 Light and Texture

- Soft directional light from above or side
- Gentle shadows
- Slight texture throughout -- nothing perfectly flat
- Lighting contrast between two zones (cool vs. warm) is a powerful storytelling tool

### 2.4 Figures

- Always viewed from fully behind, in profile, or from above -- **never facing camera, no visible faces**
- Simplified but recognizable
- Gray/dark suits for business
- Scrubs for healthcare
- Figures always have purpose -- doing something, not posing
- Realistic proportions

When used:

- Calm posture
- Focused
- Reviewing documents
- Engaged in evaluation

Avoid:

- Salesy gestures
- Presentation poses
- Smiling theatrics
- Overly expressive emotion

The tone is disciplined, not inspirational. Use figures sparingly.

### 2.5 Text in Images

**No text labels.** Story told through scene, light, and visual contrast. If a label is essential (e.g., document title), 1-3 words maximum.

The style guide allows a maximum of 3 short labels and 1 short title.

**When text earns its place:**

- Framework labels that are the article's vocabulary (Buy / Build / Partner)
- Document titles that anchor what a document represents (Risk Assessment, Discovery Findings)
- Status labels that wouldn't read without text (Partner, SaaS)

**When text doesn't earn its place:**

- Explanatory text that duplicates the headline
- Fake metrics or percentages
- Paragraph-length content on documents
- Labels on obvious icons

**Test:** Remove the text. Does the image still partially work? If yes, the text is reinforcing -- keep it. If the image completely collapses, you may be relying on text instead of visual storytelling.

### 2.6 What Is Never in a DS Hero

- Glowing effects, neon, lens flares, gradients
- 3D elements, floating icons, hexagons, circuit boards, gears, robots
- Bright or saturated color fields
- Clip-art, flat vector, or stock-illustration aesthetics
- People facing the viewer or with visible faces
- Rubber stamps, starbursts, gauges, speedometers
- Text labels beyond 1-3 words
- "SUCCESS," "VALIDATED," or any conclusory word as a label
- Glowing arrows
- Neon gradients
- 3D render effects
- Cyber grids
- Floating tech icons
- DNA strands
- Exploding data visuals
- Random gears
- Fake dashboards
- Dense tables
- Fake metrics (e.g. "95% Risk Mitigation")
- Visual metaphors that look like stock marketing art
- Overly dramatic lighting
- Abstract tech vortex imagery
- "Futuristic" glowing network nonsense
- Tron-style grid backgrounds
- Hexagon network patterns
- Giant upward arrows
- Dollar icons scattered everywhere
- Overly glossy 3D UI

If it looks like a SaaS landing page from 2016, reject it.

### 2.7 Icon Use Rules

Icons are allowed only when:

- Simple
- Single-color
- Contextual
- Supporting structure

Never decorative. Never floating. Never illustrative filler.

Allowed examples:

- Box (Buy)
- Blueprint (Build)
- Handshake (Partner)
- Status dots (R/A/G)
- Checkmarks
- Simple architecture boxes

### 2.8 AI Representation Guidelines

When AI is included:

- Subtle interface
- Clean data rows
- Minimal flow symbol
- No glowing neural networks
- No sci-fi imagery

AI should look operational, not mystical.

### 2.9 Risk Representation

Risk should be shown through:

- Structured indicators (R/A/G dots)
- Governance checkpoints
- Review gates
- Status signals
- Controlled progression

Risk should NOT be shown as:

- Fire
- Cracks
- Collapsing bridges
- Chaos explosions
- Dramatic red pathways

Risk at Digital Scientists is managed through discipline -- not avoided through magic.

### 2.10 Branding Integration

Branding must be subtle.

Options:

- Small monochrome DS logo in bottom corner
- Consistent muted palette
- Structured composition aligned to our method
- Visual reflection of Discover --> Experiment --> Engineer --> Optimize thinking

Never:

- Large logo watermark
- Marketing overlays
- Taglines inside the illustration
- Excessive typography

The image supports the article -- it is not a banner ad.

---

## 3. Scene Selection Guide

### 3.1 Scene Language vs Diagram Language

Invent the scene fresh for each post. **Describe scenes, not diagrams.** "Three cards with arrows" is diagram language -- generators will produce flat infographic output. Describe a physical scene with objects, people, light, and space.

| Instead of (diagram language) | Use (scene language) |
|---|---|
| Three panels connected by arrows | Three document cards resting on a surface with soft shadows |
| A flow chart showing stages | A worktable with a sketch on one side and a working prototype on the other |
| A decision matrix | A figure seated at a desk, two documents in front of them, one crossed out |

### 3.2 Scene Approaches by Argument Type

- **Contrast/tension** ("X is holding you back from Y") --> Split scene with two zones. Cool flat light on stuck side, warm focused light on active side. Glass wall or open doorway as divider.
- **Transformation** ("X turns Y into Z") --> Worktable with before state on one side (rough sketch, red flags) and after state on the other (clean screen, green indicators). One figure bridging them, from behind.
- **Process/methodology** ("Here's how to do X") --> Single figure at clean workspace, from behind, focused on document/screen showing process in miniature.
- **Operational/clinical** ("This is what it looks like when it works") --> Real environment: clinical room, operations center. One or two figures in purposeful action. Focal object carries meaning.
- **Analytical/review** ("The evidence shows X") --> Two professionals at a table reviewing shared document with status indicators. From behind.

---

## 4. Composition Types Deep Dive

### 4.1 Composition A: Partnership Scene

- Three-quarter overhead view of two professionals at a conference table
- Best for articles about collaboration, consulting relationships, governance, shared evaluation
- Focal artifact on the table carries the article's argument
- Wall element (whiteboard, status board) adds secondary context
- **Live example:** `public/blog/assets/images/an-essential-guide-to-managing-software-development-risk-and-maximizing-roi/risk-assessment-hero.webp` -- two figures reviewing a risk assessment with R/A/G indicators

### 4.2 Composition B: Decision Desk (Top-Down)

- Bird's-eye view of a desk surface with arranged documents
- Best for articles about frameworks, evaluations, strategic choices, discovery outputs
- Central document carries the article's argument
- Surrounding artifacts tell the story of how the decision was reached
- A hand with a pen provides human presence and decisive energy
- **Live example:** `public/blog/assets/images/buy-build-or-partner-how-to-handle-gaps-you-find-during-software-discovery-in-an-ai-world/buy-build-partner-hero.webp` -- overhead desk with three-column framework, "Partner" highlighted

### 4.3 Composition C: Lifecycle View

- Horizontal progression with subtle checkpoint
- Clear phase emphasis
- Best for articles about method, process maturity, delivery governance
- **Live example:** `public/blog/assets/images/uncover-business-benefits-through-a-proof-of-concept/proof-of-concept-hero-1440x804.webp` -- horizontal flow with validation gate

### 4.4 Composition D: Minimal Boardroom

- One presentation screen with 2-3 status elements
- Best for articles about executive alignment, governance reporting
- No dashboards

### 4.5 Thumbnail Differentiation Rule

No two adjacent blog posts on the site should use the same composition type.

At thumbnail size, Composition A (two figures at table) and Composition B (overhead desk) are immediately distinguishable. Two posts using the same composition will blur together.

---

## 5. Artifact Layer System

Every hero image should contain visual artifacts at three levels of importance.

### 5.1 Level 1: Focal Artifact (Required)

The single most prominent element. Communicates the article's argument -- not just its topic.

Examples:

- A risk assessment document with R/A/G indicators (risk article)
- A three-column decision framework with Buy/Build/Partner labels, Partner highlighted (decision article)
- A compliance checklist with approval gates (compliance article)
- An architecture sketch with validated components (modernization article)

This artifact should be the largest, most visually prominent element in the image.

### 5.2 Level 2: Context Artifacts (2-3 Required)

Supporting documents and objects that tell the story of how the conclusion was reached.

Examples:

- A workflow diagram with a dashed-outline gap -- discovery found something
- A SaaS comparison with a strikethrough or X -- a path was rejected
- An architecture sketch with connected components -- software context
- A laptop showing code, a SaaS interface, or an AI model view -- technology context
- A timeline with phase blocks and an amber flag -- lifecycle risk
- A discovery findings page with red gap indicators -- problems surfaced

Each context artifact must earn its place by adding a specific word to the image's sentence.

### 5.3 Level 3: Environmental Details (1-2 Optional)

Small objects that imply human presence and professional setting.

Examples:

- Coffee cup
- Pen on the table
- Notepad with a short checklist
- A hand holding a pen (active, not passive)

These should never compete with Level 1 or Level 2 for attention.

---

## 6. Visual Storytelling Through State

The most effective hero images show artifacts in a specific state that implies a narrative. Static artifacts are decorative. Artifacts with visible state tell stories.

### 6.1 State Signals

| State Signal | What It Communicates |
|---|---|
| Red gap indicators on a document | Problems were found |
| Strikethrough or X on a SaaS sheet | An option was rejected |
| Amber flags on a timeline phase | Risk is being actively managed |
| A faded/muted column vs. a highlighted one | A decision has been made |
| A hand actively writing or circling | Someone is taking action now |
| Checkmarks on a partner plan | A path forward is being executed |
| Dashed outline on a component | Something is missing or planned |

### 6.2 The Muting Technique

For decision-framework images, show all options but visually dim the rejected ones.

This communicates two things simultaneously:

1. Evaluation happened (all paths were considered)
2. A conclusion was reached (one path is clearly selected)

Example: Buy/Build/Partner image where Buy is faded, Build is partially muted, and Partner is highlighted with a checkmark.

---

## 7. Messaging Goals by Article Theme

| Article Theme | Visual Goal | Focal Artifact Example |
|---|---|---|
| Risk Management | Show deliberate evaluation | Risk assessment with R/A/G column |
| AI Strategy | Show structured decision-making | AI readiness evaluation with status signals |
| Platform Modernization | Show architectural validation | Architecture diagram with approval gate |
| Buy / Build / Partner | Show elimination + structured selection | Three-column framework with Partner highlighted |
| Lifecycle | Show controlled progression with checkpoints | Horizontal phases with amber governance gate |
| Governance | Show risk gate before movement | Checkpoint barrier with status indicator |
| Discovery | Show gaps surfaced and addressed | Workflow diagram with dashed gaps and findings doc |

---

## 8. Approval Checklist & Quality Control

### 8.1 Must Pass All

Before approving an image:

- [ ] Does it communicate the article's **argument**, not just its topic?
- [ ] Could this image belong to a different article? (If yes --> too generic, reject)
- [ ] Is there one clear focal point?
- [ ] Can I understand the core idea in under 2 seconds?
- [ ] Does it feel calm and executive?
- [ ] At thumbnail size, is it visually distinct from adjacent posts?
- [ ] Would a CIO share this?

### 8.2 Must Fail All

- [ ] Does it feel like a SaaS ad?
- [ ] Does it rely on glow effects?
- [ ] Is there a giant arrow?
- [ ] Are there too many icons?
- [ ] Is the viewer forced to read?
- [ ] Does it look like a slide deck diagram?

If any item in the first group fails, or any item in the second group passes -- revise.

### 8.3 Common Failure Modes

| Failure | Symptom | Fix |
|---|---|---|
| Too generic | Image could illustrate any article on the same topic | Add article-specific vocabulary as labels; add state signals (gaps, rejections, approvals) |
| Too abstract | Shapes and arrows with no recognizable meaning | Ground in real artifacts (documents, laptops, whiteboards) with specific content |
| Slide deck energy | Looks like a presentation diagram floating in space | Embed the framework inside a scene (desk, table) with environmental context |
| No argument | Shows the topic but not the conclusion | Mute rejected options; highlight the chosen path; show decisive state |
| Thumbnail collision | Two posts look identical when small | Change composition type; shift accent color position; vary focal artifact shape |
| Too much text | Image requires reading to understand | Reduce to 3 labels max; let color and spatial hierarchy do the work |
| SaaS ad aesthetic | Glowing, neon, dramatic, promotional | Strip all effects; return to muted palette with controlled accent colors only |
| Risk as catastrophe | Fire, explosions, collapsing structures | Replace with structured indicators (R/A/G dots, amber flags, gap markers) |
| Person reading paper | Figure with no context could be any article | Add artifacts that identify the domain (architecture sketch, code, status signals) |

---

## 9. Prompt Templates & Tools

### 9.1 Blog Hero Prompt Template

Every prompt follows this structure (from the design standard):

```
Smooth editorial digital illustration, style must exactly match the reference
image -- soft edges, muted tones, simplified figures, gentle lighting. Not comic
book, not technical illustration, not graphic novel, not flat vector.

[Describe the scene in physical terms -- setting, figures, objects, light.
Use scene language, not diagram language.]

[Describe the focal element -- the one thing that carries the argument.]

[Describe 1-2 supporting elements that add context without competing.]

[If split scene: describe the lighting contrast between zones explicitly --
cooler flat light on one side, warmer focused light on the other.]

No text labels anywhere in the image. No visible faces. Figures fully from behind.

Muted palette -- cool grays, off-white, warm cream. [Name specific accent colors
and exactly where they appear -- red, amber, or green dots only.]

Soft directional light, gentle shadows, slight paper texture. Executive tone.
16:9, 1440x810px.
```

See also [Section 1.6](#16-step-5-write-the-prompt) for the alternate prompt template from the blog hero standard.

### 9.2 Reference Images

**Always load at least one existing DS hero as a style reference.** The reference image does more work than any text. Keep four reference images in a dedicated folder -- drag them in before pasting the prompt.

**Reference images and best use:**
- `risk-assessment-hero` -- scenes with figures at a table or in a room
- `buy-build-partner-hero` -- bird's-eye desk compositions
- `ai-claims-review-hero` -- flow/transformation compositions
- `post-acute-virtual-care-nurse` -- clinical or single-figure scenes

### 9.3 Worked Example

**Post:** "Why Most Healthcare Apps Fail HIPAA Compliance"
**Argument:** "After reading this, the reader should believe that most teams skip compliance not out of ignorance but because they treat it as a checklist instead of a design constraint."

**Prompt:**
```
Smooth editorial digital illustration, style must exactly match the reference
image -- soft edges, muted tones, simplified figures, gentle lighting. Not comic
book, not technical illustration, not graphic novel, not flat vector.

A split-scene office. On the left side, a developer viewed from behind at a desk
with a checklist document -- items checked off mechanically, one red dot flagging
a missed item. Cool, flat overhead light. On the right side, separated by a glass
partition, a small cross-functional team (2-3 figures, all from behind) around a
whiteboard with an app wireframe where compliance requirements are woven into the
layout itself. Warm focused light from a desk lamp.

The focal element is the contrast: checklist (left) vs. integrated design (right).

Supporting: a rejected app submission notice with a red indicator on the left desk.
A green status dot on the right-side wireframe.

No text labels anywhere. No visible faces. Figures fully from behind.

Muted palette -- cool grays, off-white, warm cream. Red dot on the flagged
checklist item and rejection notice. Green dot on the wireframe status.

Soft directional light, gentle shadows, slight paper texture. Executive tone.
16:9, 1440x810px.
```

**Style reference loaded:** `risk-assessment-hero` (figures in a room)

### 9.4 Troubleshooting

Adjust **one thing at a time**. Never rewrite the entire prompt.

| Problem | Fix |
|---|---|
| Flat diagram / infographic output | You used diagram language. Reframe as physical scene with objects and light. |
| Clip-art or flat vector style | Add: "smooth editorial illustration, not flat vector, not icons." Load more references. |
| Comic book or graphic novel style | Add: "not comic book, not graphic novel, not technical illustration" explicitly. |
| Colors too bright or saturated | Add: "extremely muted palette, desaturated throughout, no bright or saturated colors anywhere" |
| Text garbled or illegible | Remove all text from the prompt. Let the scene carry the argument. |
| Faces visible on figures | Add: "figures viewed fully from behind, no visible faces under any circumstances" |
| Too literal -- spells out argument | Remove conclusory labels ("Success," "Validated"). Trust the scene. |
| Concept feels generic | Post argument isn't sharp enough. Write the one-sentence argument first. |
| Good concept, wrong style | Reference image isn't loaded. Load it and regenerate before changing prompt. |

### 9.5 Image Generation Tool Notes

#### DALL-E Observations

- Follows composition instructions well (overhead desk, two figures at table)
- Handles the muted flat vector style reasonably
- Struggles with precise text rendering -- keep labels to single words
- Status dots and R/A/G indicators render reliably
- Defaults to generic without specific artifact descriptions
- Requires explicit emphasis instructions ("this should be the brightest element")
- May need multiple generations per post

#### Prompting Lessons

- Describe artifacts by their **content and state**, not just their shape
- Name the **brightest element** explicitly -- generators won't infer hierarchy
- Describe what's **muted or rejected** as clearly as what's highlighted
- End every prompt with a "The image should instantly communicate:" statement
- The more specific the artifacts, the more specific the output
- SVG/hand-coded approaches work for abstract compositions but struggle with human figures

### 9.6 Specs and Processing

| Setting | Value |
|---|---|
| Aspect ratio | 16:9 |
| Output size | 1440x810px |
| Final format | WebP, quality 82 |
| Max file size | 200 KB |
| Naming | `hero-[post-slug].webp` |

Process after generating (Mac):
```
sips --resampleWidth 1440 input.png --out /tmp/r.png && cwebp -q 82 /tmp/r.png -o hero-[slug].webp
```

Confirm the image reads clearly as a thumbnail at 300x170px before finalizing. No two adjacent posts on the blog index should use the same scene type.

---

## 10. Library Tracking

### 10.1 Published Images

Track published images to prevent repetition:

| Post Title | Composition | Focal Artifact | Accent Position | Hero File |
|---|---|---|---|---|
| Managing Software Development Risk | A (two figures) | Risk assessment with R/A/G | Center-left | `an-essential-guide-to-managing-software-development-risk-and-maximizing-roi/risk-assessment-hero.webp` |
| Buy, Build, or Partner | B (overhead desk) | Decision framework, Partner highlighted | Center-right | `buy-build-or-partner-how-to-handle-gaps-you-find-during-software-discovery-in-an-ai-world/buy-build-partner-hero.webp` |
| Uncover Benefits Through a POC | C (lifecycle) | Validation gate with phase progression | Center | `uncover-business-benefits-through-a-proof-of-concept/proof-of-concept-hero-1440x804.webp` |
| [Next post] | Alternate | [TBD] | [Vary] | -- |

All paths relative to `public/blog/assets/images/`.

### 10.2 Rules

- Alternate composition types between adjacent posts
- Vary where the brightest accent color sits (center, left-biased, right-biased)
- The combination of composition + focal artifact + accent position should be unique per post

---

## 11. LinkedIn Post Image Generation

### 11.1 Single Post Graphics

- Dimensions: 1200x1200 (square) or 1200x627 (landscape)
- 4 template types:
  - **Quote Card**: Dark background (dsBlack `#050505`), large pull quote in white, attribution below, dsBlue `#304FFF` accent bar on the left edge
  - **Data Callout**: Single stat (large dsBlue number), context line below in white or light gray, minimal design on dark or white background
  - **Framework Graphic**: 2-4 column comparison or process flow, muted palette, dsBlue highlights on the selected or recommended column, same visual language as blog heroes
  - **Case Proof**: Metric + one-line context + client industry tag, professional tone, no client logos without permission

### 11.2 Carousel Slide Graphics

- Dimensions: 1080x1350 (portrait, 4:5)
- **Cover slide**: Dark bg (dsBlack or dsBlue), title in white Inter Bold, dsBlue accent element (line, bar, or shape)
- **Content slides**: White bg, one idea per slide, consistent header strip (dsBlue bar or dsBlack strip with white text), body text in dsBlack
- **CTA slide**: dsBlue bg, white text, clear next step (e.g., "Read the full post" or "Book a discovery call")

### 11.3 Style Rules

- Same visual language as blog heroes (muted, professional, no slop)
- Use Inter font in graphics (or system equivalent)
- No stock photos, no emoji, no clip art
- Status indicators (R/A/G) allowed as accent elements
- No saturated fills or bright backgrounds -- same palette discipline as blog heroes
- See `brand-guide.md` for DS brand colors, typography, and tone-of-voice

---

## 12. METHOD Illustration Reference

Cross-reference to `brand-guide.md` Section 9 for the full METHOD illustration standard (1950s-60s textbook aesthetic, 4 archetypes). Prompts live in `method-illustration-prompts.md`.

METHOD illustrations use a **different visual language** from blog heroes:
- Blog heroes: smooth editorial digital illustration (HBR/MIT Sloan reference)
- METHOD illustrations: 1950s-60s technical textbook aesthetic (see brand guide for details)

Do not mix the two styles. Each has its own prompt patterns and reference images.

---

## 13. OG Image Generation

### 13.1 A2 Template Spec

- 1200x630px, PNG
- Layout: hero image background (blurred/darkened), gradient overlay, DS logo (top-left), title text (white, Inter Bold), category pill (dsBlue `#304FFF` bg, white text)
- Generated by: `scratchpad/generate_og_images.py`

### 13.2 Manual OG Generation

When the auto-generator doesn't have a hero image available, create manually following the same layout:

- Background: solid dsBlack `#050505` or dsBlue `#304FFF` gradient
- Logo placement: top-left, 40px margin
- Title: centered, white, Inter Bold, max 3 lines
- Category pill: dsBlue bg with white text, positioned below or above title
- Maintain 1200x630px dimensions for all OG images

---

## 14. Supplemental Visual Rules

These rules apply across all DS image types (blog heroes, LinkedIn graphics, OG images) unless a specific section overrides them.

### 14.1 Human Figures

Use sparingly.

When used:

- Calm posture
- Focused
- Reviewing documents
- Engaged in evaluation

Avoid:

- Salesy gestures
- Presentation poses
- Smiling theatrics
- Overly expressive emotion

The tone is disciplined, not inspirational.

Figures must always be viewed from fully behind, in profile, or from above. No visible faces. See [Section 2.4](#24-figures) for full figure rules.

### 14.2 AI Representation Guidelines

When AI is included:

- Subtle interface
- Clean data rows
- Minimal flow symbol
- No glowing neural networks
- No sci-fi imagery

AI should look operational, not mystical.

### 14.3 Risk Representation

Risk should be shown through:

- Structured indicators (R/A/G dots)
- Governance checkpoints
- Review gates
- Status signals
- Controlled progression

Risk should NOT be shown as:

- Fire
- Cracks
- Collapsing bridges
- Chaos explosions
- Dramatic red pathways

Risk at Digital Scientists is managed through discipline -- not avoided through magic.

### 14.4 Branding Integration

Branding must be subtle.

Options:

- Small monochrome DS logo in bottom corner
- Consistent muted palette
- Structured composition aligned to our method
- Visual reflection of Discover --> Experiment --> Engineer --> Optimize thinking

Never:

- Large logo watermark
- Marketing overlays
- Taglines inside the illustration
- Excessive typography

The image supports the article -- it is not a banner ad.

### 14.5 Icon Use Rules

Icons are allowed only when:

- Simple
- Single-color
- Contextual
- Supporting structure

Never decorative. Never floating. Never illustrative filler.

Allowed examples:

- Box (Buy)
- Blueprint (Build)
- Handshake (Partner)
- Status dots (R/A/G)
- Checkmarks
- Simple architecture boxes

### 14.6 Text in Hero Images

See [Section 2.5](#25-text-in-images) for the full text-in-images policy. The key test: remove the text. Does the image still partially work? If yes, the text is reinforcing -- keep it. If the image completely collapses, you may be relying on text instead of visual storytelling.

---

## 15. Philosophy

### What This Standard Signals

Digital Scientists blog imagery should ultimately communicate:

- We think before we build
- We evaluate before we recommend
- We govern before we execute
- We see the gaps others miss
- We are the calm, structured partner in a complex decision

Every hero image is a 2-second argument for why Digital Scientists is the right partner.

### Evolution Policy

We refine this system as we:

- Identify visual clutter
- Remove ambiguity
- Improve hierarchy
- Clarify messaging
- Add new composition types
- Learn what generators handle well and poorly

This is not about style.
It is about disciplined thinking made visible.

---

## 16. Revision History

- 2026-03-07: v1.0 -- Consolidated from `ds-blog-hero-image-standard.md` + `ds-design-standard.md` Section 8.7. Added LinkedIn post image generation (Section 11), METHOD illustration cross-reference (Section 12), OG image generation (Section 13), and supplemental visual rules appendix (Section 14).

---

End of Document.
