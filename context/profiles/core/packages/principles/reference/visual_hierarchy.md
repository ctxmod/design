# Visual Hierarchy

Deliberate ordering of elements so the eye is guided in task order — contrast channels, one focal point, scan patterns, density, and the hierarchy of needs.

## What + why

Visual hierarchy is the deliberate ordering of elements so the eye is guided
through them in the order that serves the user's task. Every interface answers
the question "what do I look at first?" — the only choice is whether you answer
it on purpose. It works because perception is pre-attentive: before a user reads
anything, the visual system separates **figure from ground** and snaps to the
element that differs most from its surroundings (the **von Restorff**, or
isolation, effect) — both named laws in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />. A clear hierarchy is the
single highest-leverage quality in UI design: it makes a screen instantly
legible, and its absence makes even beautiful screens feel confusing.

Hierarchy is established through **contrast** — making important things *differ*
from their surroundings along one or more channels:

| Channel | Increases prominence by… | Notes |
|---------|--------------------------|-------|
| **Size** | Larger area / type size | The most reliable signal; jumps of 1.5–3x read clearly, 1.1x reads as noise (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />) |
| **Weight** | Heavier font weight, denser fill | Reserve bold for hierarchy, not emphasis-by-default |
| **Color** | Higher saturation/contrast, accent vs. neutral | Use sparingly — color is signal (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />) |
| **Space** | More surrounding whitespace | Isolation elevates; crowding demotes (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />) |
| **Position** | Top-left / optical center / above the fold | Follows reading order |
| **Motion** | Movement draws the eye involuntarily | The strongest and most disruptive signal; use rarely (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />) |

## Testable obligations

- Each view has exactly **one** primary focal point; all other elements are
  explicitly secondary or tertiary.
- The focal point is chosen from the view's *job*, not its prettiest element, and
  carries the most contrast.
- Each importance level uses **the fewest channels needed** to read as distinct —
  no redundant stacking of size + weight + color + caps on the same element.
- Visual order matches the expected scan path for the layout type (F, Z, or
  layer-cake), not against it.
- Density varies *intentionally* to express hierarchy — owned by
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />.
- Semantic order (heading levels, landmark regions, DOM/reading order) matches the
  visual order.

## How to verify

- **One focal point**: apply the *squint test* — blur the screen (squint, or a
  Gaussian blur); exactly one element should remain dominant. Two survivors means
  competing focal points.
- **Focal point from the job**: name the view's primary task in one sentence; the
  dominant element must be the control or content that task requires.
- **Fewest channels**: list the channels applied to the heading/primary element;
  remove any one channel — if the element still reads as dominant, that channel
  was redundant and should go.
- **Scan path**: trace the intended scan (F/Z/layer-cake) and confirm key terms,
  nav, and CTA fall on it; mismatch is a violation.
- **Semantic match**: read the heading-level / landmark outline (or run an
  accessibility tree dump); its order must equal the visual order — e.g. the
  visual focal point must not be an `<h3>` buried after decorative `<h1>`s.

## Anti-patterns

- **Everything is shouting** — redundant signals stacked on many elements (bold +
  colored + large + uppercase everywhere) flatten the hierarchy so nothing leads.
- **Many primaries** — multiple "primary" buttons on one screen; there is one
  primary action, the rest are secondary or ghost (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />).
- **Two equal focal points** — competing elements cancel; the eye ricochets and
  lands nowhere. The isolation (von Restorff) effect only fires when *one*
  element is distinct (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />).
- **Fighting the scan** — placing the CTA off the Z-path, or key terms mid-line on
  an F-pattern page.
- **Polishing a broken base** — spending effort on micro-contrast and alignment
  while the primary action is not yet findable. Resolve hierarchy in dependency
  order — **findability → order → grouping → rhythm → refinement** — each level
  depends on the ones below it (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" /> for grouping).
  A clear visual hierarchy is also a clear semantic one: a well-ordered page is
  more usable, not merely more compliant (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/information_architecture.md" />
