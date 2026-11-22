# Brutalism brand

The **Brutalism** brand tier. It extends `web` — and
through it the `core` umbrella — filling the abstract
component slots with one concrete, opinionated look: raw structural honesty.
Inspired by 1950s brutalist architecture, it celebrates exposed structure, thick
visible borders, stark extreme-weight typography, and a terracotta + ochre
material palette. No soft shadows, no gradients, no rounded corners. Everything
shows its bones.

```
core                   ← principles + abstract component taxonomy
  └── web               ← web concretization (CSS, viewports, a11y, perf)
        └── brand_brutalism  ← this profile: terracotta/ochre, Darker Grotesque, thick borders
```

## What lives here

- **<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/brand.md" />** — the
  brand essence: color palette, typography, motion vocabulary, shape & surface,
  and the do/don't list. The foundation the component files build on.
- **Component styling** — one file per umbrella component slot, concretizing it
  for Brutalism:
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/buttons.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/inputs.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/cards.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/navigation.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/feedback.md" />

## How it specializes the tiers

This profile inherits the web layer unchanged — it does not re-derive container
queries, focus management, or compositor-friendly motion. It fills the umbrella's

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />

slots with concrete values, expressed through the web primitives

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />

establishes: CSS custom properties for tokens, semantic HTML for structure,
compositor-only properties for the (deliberately abrupt) motion.

The brand's signature is **the exposed border**. Where other brands lean on
shadow and radius for elevation and softness, Brutalism uses border weight and
hard offset blocks. Structure is never hidden; it is the aesthetic.
