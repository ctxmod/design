# Composition

Arrangement of elements in space — alignment, grids, Gestalt grouping, balance, density, and responsive reflow.

Composition is the arrangement of elements in space — how they align, group,
balance, and breathe. Where <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" /> decides *what*
the user looks at, composition decides *how the whole holds together*. A
well-composed layout feels stable and effortless to read even before the user
notices any individual element. A poorly composed one feels "off" in ways users
can't name but always sense.

This document is platform-agnostic theory. The medium tier concretizes it into
responsive grids, breakpoints, and layout primitives (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" />).

## Alignment

Alignment is the cheapest way to make a layout look intentional.

- **Establish alignment edges.** Every element should align its edge or center to
  something else. Stray elements that align to nothing create visual static.
- **Prefer few alignment lines.** A layout that snaps to a small number of shared
  edges reads as ordered; one with dozens of slightly-different left edges reads as
  sloppy.
- **Optical over mathematical.** Sometimes mathematically-centered elements look
  off-center (a triangle "play" icon, text with descenders, a label next to an
  icon). Nudge for what *looks* aligned, not what measures aligned.

## Grids

A grid is a shared structure that columns, gutters, and margins snap to. It is the
substrate that makes alignment systematic.

- **Columns + gutters + margins.** Content occupies columns; gutters separate
  them; margins frame the whole. All three come from the
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />.
- **The grid is a guide, not a cage.** Most elements obey it; a deliberate
  break — an image bleeding past the margin, an asymmetric hero — earns attention
  precisely because the rest is disciplined.
- **Consistency across the product.** The same grid underlies every page so that
  switching screens feels continuous (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />).

## Grouping (Gestalt principles)

The brain assembles individual marks into groups using predictable cues — the
**Gestalt laws of grouping** (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />
for each law, its obligation, and how to verify it). Design *with* these, because
the user perceives them whether you intend them or not:

| Principle | The eye groups things that are… | Design lever |
|-----------|--------------------------------|--------------|
| **Proximity** | close together | spacing — the primary grouping tool |
| **Similarity** | alike in shape/color/size | consistent component styling |
| **Common region** | inside the same boundary | cards, panels, background fills |
| **Continuity** | along a line or curve | alignment, reading flow |
| **Closure** | forming a recognizable whole | implied shapes, partial borders |

Proximity is the most powerful and most abused: if related fields are spaced like
unrelated ones, no border or color will fully fix the confusion. Get grouping
right with **space first**, then reinforce with region/similarity only if needed.

## Balance

Balance is the distribution of visual weight across the composition. Weight comes
from size, density, color, and contrast.

- **Symmetric balance** — mirrored weight around an axis. Reads as formal, stable,
  calm, classic. Good for focused, ceremonial, or trustworthy moments.
- **Asymmetric balance** — unequal elements counterweighted (a large quiet area
  balanced by a small dense one). Reads as dynamic, modern, editorial. Harder to
  pull off; requires a real eye for weight.
- **Imbalance is a tool, not always a flaw** — an intentionally heavy corner can
  pull the eye exactly where you want it. The failure is *accidental* imbalance
  that makes the layout feel like it's tipping over.

## Density and whitespace

Composition decides how tightly the space is packed. (The mechanics live in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />; here it is a compositional choice.)

- **Whitespace frames.** Space around a group defines it as a unit and gives the
  focal point room. Macro-whitespace (between regions) sets the overall calm;
  micro-whitespace (between lines and controls) sets legibility.
- **Density expresses purpose.** A dense composition says "work happens here"; a
  spacious one says "consider this." Vary density between regions deliberately, and
  keep each region internally consistent.

## The grid-vs-asymmetry tension

Two valid compositional stances pull against each other:

- **Strict grid** — order, predictability, trust, scannability. The risk is
  blandness; precision in spacing, type, and detail is what saves it.
- **Asymmetry / grid-breaking** — energy, distinctiveness, memorability. The risk
  is chaos; it only works when anchored by an underlying structure the breaks play
  against.

The strongest layouts usually do both: a disciplined grid with **one** deliberate
break that becomes the signature. Spend that boldness once (see the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/rules/aesthetic_discipline.md" />).

## Responsive composition (abstract)

Composition is not a single arrangement but a *family* of arrangements across
sizes. Think about it abstractly here; the medium tier sets the actual
breakpoints.

- **Reflow, don't just shrink.** As space narrows, multi-column layouts should
  *reorganize* (columns stack, side-by-side becomes sequential), not merely scale
  down until everything is tiny.
- **Reading order is preserved.** However the layout reflows, the priority order
  from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" /> must survive — the most important
  element stays first.
- **Density adapts to context.** Smaller surfaces and touch input favor lower
  density and larger targets; larger surfaces can afford more columns and
  information.
- **Containers have intent.** Reading content gets a constrained measure;
  dashboards fill the width. The composition declares which (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" />).
