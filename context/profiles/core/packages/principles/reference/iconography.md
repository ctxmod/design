# Iconography

Icon construction discipline — canvas/live-area, stroke-to-font-weight matching, grid alignment, optical centering, single-concept-per-icon. Construction is umbrella; style is brand/medium.

Icons are compressed language. Each one stands in for a word or an action in a
space too small for type, and a set of them reads as a system only when they are
*constructed* the same way. The recurring failure is to treat each icon as an
isolated drawing — get the metaphor right, ship it, move on — and end up with a
tray of glyphs that sit at different optical sizes, carry different stroke
weights, and shimmer at small sizes because their vertices fall between grid
units. The fix is to separate the two halves of the decision: how an icon is
*built* and how it is *styled*.

This document is about construction. Construction is a small set of obligations
that hold regardless of medium — they apply equally to SF Symbols in an iOS app,
glyphs in a CLI status line, symbols in a LaTeX document, and SVGs in a web page.
Style — outline versus filled, rounded versus sharp, corner radius, the signature
flourish — is a separate, lower-tier decision. The layering rule below states the
boundary explicitly so a brand can restyle freely without breaking the system,
and so construction discipline survives every restyle.

> **Construction is the system; style is the skin.** Two icon sets with opposite
> visual styles (one hairline-outline, one heavy-filled) can both be correctly
> constructed; two icons in the *same* style can read as foreign to each other if
> one ignores the live area or the stroke-matching rule. Judge a set on
> construction first.

## Fixed canvas with defined live area

Every icon in a set is drawn on the **same bounding box** (the canvas), and its
content stays within a **live area** — a defined inset from the canvas edge that
leaves consistent breathing room on all sides. The canvas guarantees that icons
occupy equal space when laid out; the live-area inset guarantees that they read
at the same *optical* size despite differing silhouettes.

A square glyph fills the live area edge-to-edge; a circular glyph is drawn
slightly larger so its visual mass matches the square (a mathematically
same-width circle looks smaller — see [optical centering](#optical-not-mathematical-centering)).
The live area, not the raw canvas, is the size contract. Many systems publish a
small family of canvases (e.g. 16 / 20 / 24) with redrawn — not merely scaled —
geometry per size, because optical adjustments that work at 24 break at 16.

**Anti-pattern:** drawing icons "to fit" with no shared inset, so a wide glyph
crowds the canvas edge while a narrow one floats in space, and the set looks
ragged when set in a row.

## Consistent stroke weight matched to adjacent font weight

An icon sitting next to text is read as part of the same line, so it must carry
the **same visual weight** as that text. Stroke weight is the icon's analogue of
font weight: a 1px-stroke icon beside a bold label looks anemic; a heavy-stroke
icon beside light body text looks like a typo. Match the icon's stroke to the
weight of the type it accompanies, and scale stroke weight *with* type weight
across the system rather than freezing a single stroke for all contexts (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />).

Within one set, stroke weight is a constant, not a per-icon choice. A single
deviating stroke is as conspicuous as one bolded word in a sentence.

**Anti-pattern:** mixing stroke weights inside one tray (some icons hairline,
some heavy) because they were sourced from different libraries; the tray reads as
a collage, not a system.

## Pixel / whole-unit grid alignment

At the small sizes icons live at, sub-unit geometry blurs. Snap vertices,
stroke centers, and key features to the **whole-unit grid** — the pixel grid for
raster/screen rendering, the terminal **cell** grid for CLI glyphs, the baseline
grid for typeset symbols — so edges land on unit boundaries and render crisp
rather than smeared across two units. This is why icons are redrawn per canvas
size: a feature that snaps cleanly at 24 px falls between pixels when scaled to
16 px.

**Anti-pattern:** designing one master icon and scaling it to every size; the
scaled copies miss the grid at small sizes and turn fuzzy, defeating the point of
a small icon (instant recognition).

## Optical (not mathematical) centering

Center icons by **visual mass**, not by bounding-box geometry. The eye locates a
shape's center at its weighted balance point, which rarely coincides with the
rectangle's midpoint: a play triangle centered mathematically looks shifted left
and must be nudged right; a circle must be drawn slightly larger than a
co-inscribed square to look the same size. Apple's SF Symbols are built this way —
glyphs are optically aligned to the text baseline and balanced by mass, not by
their bounding boxes — which is why they sit correctly inline with type.

**Anti-pattern:** centering a glyph with `margin: auto` / equal numeric padding
and accepting the result; geometrically-centered asymmetric glyphs (triangles,
arrows, speech bubbles) look off-center and the misalignment compounds across a
row.

## Single concept per icon; metaphor clarity

Each icon carries **one idea**, expressed through a metaphor a user recognizes
without a label. Two concepts crammed into one glyph (a gear *and* a cloud) read
as neither at small sizes. Prefer conventional metaphors over clever ones — a
magnifying glass for search beats an inventive symbol no one decodes — and reuse
the same metaphor for the same concept everywhere (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" /> on recognition and consistency).

**Anti-pattern:** overloading a glyph with detail to be "more descriptive,"
which collapses into noise when rendered at 16 px; or inventing a novel metaphor
where a conventional one exists, forcing users to learn it.

## Layering rule (T): construction is umbrella, style is brand/medium

The boundary between this document and a brand is sharp:

| Decision | Tier | Owns |
|----------|------|------|
| **Construction** — canvas + live area, stroke-to-type matching, grid alignment, optical centering, one-concept-per-icon | **umbrella** | the invariants in this document; identical for SF Symbols, CLI glyphs, LaTeX symbols, web icons |
| **Style** — outline vs filled, rounded vs sharp corners, corner radius, terminal weight (rounded/butt), the signature treatment | **brand / medium** | the look applied *on top of* a correctly constructed icon |

A brand may restyle the entire set — flip outline to filled, round every
corner — without touching a single construction obligation, and the set stays a
system. Conversely, no amount of consistent *style* rescues a set that violates
construction (mismatched live areas, mixed strokes, off-grid vertices). State
this boundary when authoring a brand: the brand specifies style and inherits
construction; it never redefines what "same canvas" or "matched stroke" means.

## Medium-conditionality note

Two facets of iconography are **not** umbrella-fixed and must be restated per
medium in that medium's <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />:

- **Icon size and minimum size** — a touch UI needs larger tap-target glyphs than
  a pointer UI; a CLI glyph is one or two cells wide; a typeset symbol is sized in
  em relative to running text. The construction rules hold; the *numbers* are a
  medium decision.
- **Raster vs. vector** — screens may ship vector (SVG/font) icons that re-snap to
  the grid at each size, while a terminal can only place glyphs from a fixed font
  at cell resolution and a print pipeline may rasterize at a target DPI. Grid
  alignment means *pixel* grid in one medium and *cell* grid in another.

A medium profile declares, per the capability-declaration mechanism, whether each
obligation here is *supported*, *adapted* (with its own units/thresholds), or
*dropped*, and overrides the medium-conditional facets above rather than ignoring
them.

## How to verify

Each obligation is checkable against a rendered icon set, in the medium's own
units (screen: px on the pixel grid; CLI: cells; typeset: em on the baseline
grid):

| Check | Method | Flag when |
|-------|--------|-----------|
| Live area | Overlay all icons on the shared canvas; measure the inset on each side | insets differ across icons, or content touches the canvas edge |
| Stroke matching | Compare icon stroke weight against the adjacent type's weight | stroke reads lighter/heavier than the text it sits beside, or varies within the set |
| Grid alignment | Inspect vertices/stroke centers against the unit grid at the smallest size | features fall between units and render fuzzy |
| Optical centering | Place asymmetric glyphs (triangle, arrow) in a row and view inline | a glyph looks shifted despite equal numeric padding |
| One concept | Read each glyph without its label | a glyph needs a label to decode, or carries two ideas |
| Layering | Confirm construction obligations hold independent of the chosen style | a restyle (outline↔filled) breaks size/stroke/centering consistency |
