# Dramatic brand

The **Dramatic** brand tier of the user-facing-surface design stack. It extends
`web` — inheriting the web platform layer (CSS custom
properties, viewports, focus management, compositor-friendly motion) unchanged —
and fills the umbrella's abstract component slots
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />)
with concrete, theatrical styling.

```
core                   ← principles + abstract component taxonomy
  └── web               ← web concretization (CSS, viewports, a11y, perf)
        └── brand_dramatic  ← this profile: near-black canvas, violet+rose, Outfit 400/900
```

## The essence in one line

High-contrast, dark-surface, theatrical — the intensity of a film title sequence.
Light text burns against near-black; vivid violet and rose accents cut through the
dark like stage lighting. Outfit, restricted to **two weights only** (400 and
900), enforces a binary "whisper or shout" hierarchy.

## What lives here

- **<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/brand.md" />** — the
  brand foundation: palette (near-black surfaces, near-white text, violet + rose
  accents), the two-weight typography system, cinematic motion vocabulary, dark
  surface/glow treatment, and the do/don't discipline.
- **Component files** — concrete styling for each umbrella slot, expressed in CSS
  custom properties this brand defines:
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/buttons.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/inputs.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/cards.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/navigation.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/feedback.md" />

## How to read these files

Each component file concretizes the matching umbrella slot. The slot defines the
*contract* (variants, states, responsibilities); this brand supplies the *look*
(exact tokens, glow treatment, weight usage). Where a value is a web primitive,
it is written as a CSS custom property (`--bd-*`) so the brand is portable across
frameworks (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />).
Accessibility obligations (focus rings, contrast, reduced-motion) are inherited
from `web` and restated only where the dark canvas changes the calculus.
