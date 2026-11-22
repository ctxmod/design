# Affordance Adaptation

Charter section 4 for the paginated-print medium — read-only input model, no hit targets (minimum legible type at reading distance replaces them), page-in-hand viewing distance, comfortable density default, and the per-principle meaning shifts print introduces.

This is **section 4 of the five the medium charter makes mandatory**. It
declares the medium's interaction reality and states how each umbrella
principle's *meaning* shifts when the surface is a page rather than a screen.

## The medium's interaction reality

### Input model — none

The medium supports **none** of pointer, touch, or keyboard. It is
**read-only / text-and-image**. The reader's only channel into the artifact is
their eyes; their only channel out of it is turning the page, which the
document cannot observe.

This is the fact that drives "no interaction states are live" in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/capability_declaration.md" />.
It is not a separate determination — it is the same determination stated from
the input side.

### Target-size rules — no hit targets exist

There is nothing to hit. WCAG 2.2 SC 2.5.8's 24×24 CSS-px floor and the 44×44
best-practice target have no referent here: no pixels, no pointer, no target.

The charter's pattern for non-pointer media is a **substitute economy metric** —
`cli` replaces target size with keystroke economy. For print the
substitutes are physical rather than procedural, because the reader's effort is
optical and manual rather than motor-targeting:

- **Minimum legible type size at reading distance.** This is the primary
  substitute. It is the constraint that actually bounds how small an element may
  be, exactly as target size bounds it on the web. Body running text sits at
  **10–12pt** for the page-in-hand case; annotation strata (footnotes, captions,
  table cells) may drop toward **8–9pt** but not below, and never for sustained
  running text. Below roughly 8pt reading speed measurably degrades and fixation
  duration climbs.
- **Thumb-reachable page turn.** The physical analogue of reach. Content pushed
  into the outer trim edge, or a folio placed where a hand naturally rests, is
  the print form of an unreachable control. The outer and bottom margins are not
  waste — they are the handling zone.

Stated plainly so no reviewer looks for one: **there are no pixel targets in
this medium, and no finding may be raised about their size.**

### Viewing distance — page-in-hand

The charter names three cases (arm's-length, across-the-room, page-in-hand) and
this medium is the third. Reading distance is roughly **30–40cm** — nearer than
a desktop screen, and held at an angle the reader controls.

The consequence is the one figure that most visibly separates this medium from
the web: **print body type is 10–12pt where web body type is 16px.** That is not
print being less accessible. A 16px screen glyph viewed at 50–70cm subtends a
comparable visual angle to an 11pt printed glyph viewed at 30–40cm, and print
carries no subpixel rendering penalty, no gamma-dependent stroke thinning, and
no reflow. The umbrella's `≥ 16px` floor is a screen figure at screen distance
and **does not transfer**; the figures above are its page-in-hand restatement.

Two corollaries follow from the reader controlling the angle: glare and ambient
light vary, which is a further reason the contrast decisions in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/token_translation.md" /> are
made against the substrate rather than against a luminous white.

### Density default — comfortable

The medium defaults to **comfortable**.

The justification is that reading here is **sustained and linear**. The reader
is not scanning for a control; they are consuming continuous prose across many
pages, and the umbrella's leading and measure bands exist for exactly that mode.
A compact default would be the wrong optimization: the page is a *fixed* budget,
so compacting does not buy scroll-free density the way it does on the web — it
buys one fewer page at a measurable cost in reading speed.

Margins are the visible expression of this default, and they are a legibility
instrument, not empty space: they carry the handling zone, they bound the
measure, and they host the folio and running head.

The default is a default, not a fixed point. A data-dense stratum inside an
otherwise comfortable document — an invoice line table, a report appendix, a
reference table — legitimately tightens to compact locally. What is not
legitimate is a compact *whole document* chosen to save a page.

## Per-principle meaning shifts

These are the principles classified **adapted** in the capability declaration,
stated as the substitution the reviewer applies.

| Principle | Adaptation in print |
|---|---|
| `visual-hierarchy` | Gains **page-position weight**. The top of a page is a stronger position than the middle, and the recto (right-hand) page is stronger than the verso. Position is a hierarchy channel the umbrella does not have, because a scrolling surface has no fixed top. A heading that lands mid-page carries less weight than the same heading at a page top, regardless of its size. |
| `information-density` | Bounded by **physical page area** rather than by scroll. There is no "below the fold" to defer into; content that does not fit is content that moves to another page, which costs the reader a page turn. Density is therefore a hard allocation problem here, not a soft comfort preference. |
| `composition` | Gains **the spread as a unit**. In a twoside document, facing pages are seen simultaneously and read as one composition. Balance, alignment, and float placement are judged across the spread — a figure placed at the outer edge of the verso and one at the outer edge of the recto frame the spread; two at the same inner position unbalance it. Responsive reflow is void and is not a substitute concern. |
| `motion` | **Void.** No duration, no easing, no choreography, no transition. Nothing on a printed page moves. |
| `dark-mode` | **Void.** One surface, one rendering, no theme axis to switch. |

## Perception and cognition survive — except Fitts

The charter states that perception/cognition laws are medium-agnostic and
survive translation unchanged
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />).
That holds here, and it is worth affirming rather than assuming:

- **Proximity and the other Gestalt grouping laws hold on paper.** Items placed
  near each other are read as a group whether the substrate is a screen or a
  sheet — this is a property of the visual system, not of the display.
- **Working-memory limits hold.** A table with too many simultaneously relevant
  columns overloads a reader on paper exactly as it does on screen; a page turn
  makes it worse, because the reader must now hold the header row in memory
  across the turn.
- **Serial position, von Restorff, processing fluency, and
  aesthetic-usability all hold** unchanged.

**Fitts's law is the one that genuinely voids.** It predicts acquisition time
for a pointing task as a function of target distance and width. There is no
pointing task in this medium, so the law has no term to bind to. This is a real
void, not an adaptation: unlike `cli`, which restates Fitts as keystroke
economy because a CLI still has a *selection* task, print has no selection at
all. The substitutes named above (legible type size, thumb-reachable page turn)
are legibility and handling constraints, not disguised Fitts restatements, and
should not be presented as such.

## Testable obligations

- **Body running text resolves to 10–12pt** at the style's `base-font-size ×
  size`; annotation strata do not fall below 8pt.
- **The outer and bottom margins are preserved as a handling zone.** No body
  content, and no element the reader must read fully, extends into them.
- **Hierarchy is evaluated with page position as a channel.** A section opening
  is expected at a page top or with deliberate space above it, not stranded
  mid-page beneath a preceding section's last two lines.
- **Composition is evaluated per spread on twoside documents**, not per page.
- **The document reads as comfortable density by default**, with compact
  strata confined to genuinely data-dense regions.
- **No finding cites motion, theme, hit-target size, hover, focus, or scroll.**
  All are void in this medium.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Body size | Divide measured body size by `base-font-size`; confirm the product lands in 10–12pt | Outside the band, or an annotation stratum below 8pt |
| Handling zone | Measure the distance from the outermost text to the trim edge | Body content encroaches on the outer or bottom margin |
| Page-position hierarchy | Locate each top-level section opening on the page image | A major section opens on the last few lines of a page |
| Spread composition | View facing pages side by side | Floats or heavy blocks cluster on one side, or the two pages' text blocks do not align across the gutter |
| Density default | Measure leading ÷ size for body, and the margin fraction of the sheet | Body leading below the umbrella's comfortable band, or margins compressed to gain a page |
| Void principles unreported | Read each finding's mechanism | It names motion, theme, hit-target size, hover, focus, or scroll |

## Anti-patterns

- Applying the umbrella's `≥ 16px` body floor to a printed page and reporting
  11pt body text as too small. It is the medium's norm; the floor did not
  transfer.
- Reporting a "target too small" finding against a printed cross-reference or
  folio. There are no targets.
- Judging a twoside document page by page and missing that the spread is
  unbalanced — the failure is only visible at the unit the medium actually
  presents.
- Compacting a whole document to save one page and calling it density. That is
  the invoice single-page pressure problem solved at the reader's expense; the
  correct lever is content, not leading.
- Restating Fitts's law as "the eye must travel to the folio" to keep the law in
  play. It voids; pretending otherwise produces findings with no mechanism
  behind them.
- Treating margins as wasted area to be reclaimed. They are the handling zone,
  the measure bound, and the home of the running head and folio.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/confidence_note.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />
