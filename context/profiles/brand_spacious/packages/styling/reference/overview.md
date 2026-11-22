# Spacious brand

The **Spacious** brand profile. A Tier 3 brand that fills the abstract component
slots defined by the design umbrella (the `core` profile) — as concretized for the web by
`web` — with concrete styling for a single conviction: the most important
element in any interface is the *space between elements*.

Spacious is whitespace-first. It is built on an 8pt grid with deliberately
generous defaults, pairs Open Sans (body) with Montserrat (headings), and uses a
conventional blue-violet accent on light, neutral surfaces. Color is intentionally
quiet so that space can be the hero: hierarchy is communicated by how much room a
thing is given, not by how loud its color is.

## What this profile provides

- **<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/brand.md" />** — the
  brand essence: palette, typography, motion, shape/surface, the 8pt grid, and the
  do/don't discipline that makes the aesthetic cohere.
- **Component styling** — concrete looks for each umbrella slot, generous by
  default:
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/buttons.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/inputs.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/cards.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/navigation.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/feedback.md" />.

Each component file inherits the slot *contract* from the umbrella (variants,
states, responsibilities) and supplies only the Spacious-specific values: the
spacing tokens, the colors, the radii, the motion. Where a behavior is already
mandated by the slot, this profile does not restate it — it concretizes it.
