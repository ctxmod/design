# Forest brand

A **brand tier** profile in the user-facing-surface design stack. Forest is a
sustainability-inspired, dark-green design system: deep forest surfaces, a
high-energy lime brand accent, rounded shadow-free cards, and clean technical
layouts that feel grounded, ecological, and trustworthy.

```
core                   ← principles + abstract component taxonomy
  └── web               ← web concretization (CSS, viewports, a11y, perf)
        └── brand_forest  ← this profile: concrete Forest palette, type, motion, components
```

This profile fills the umbrella's abstract component slots
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />)
with **concrete Forest values**, expressed through the web primitives the
`web` medium establishes — CSS custom properties
for tokens, compositor-only properties for motion, semantic HTML for structure.
It does not re-derive how container queries, focus rings, or reduced-motion work;
those are inherited unchanged.

## What lives here

- **<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />** — the
  identity card: essence, full palette, type pairing, motion vocabulary, shape &
  surface, and do/don't.
- **Component specializations** — one file per umbrella slot, giving Forest's
  concrete values, token names, and states:
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/buttons.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/inputs.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/cards.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/navigation.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/feedback.md" />

## How to use it

Read <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" /> first for
the tokens, then a component file for build-ready values. Tokens are CSS custom
properties (`--forest-*`); see the

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />

doc for the carrier mechanism. The framework that ships them (Tailwind, shadcn,
vanilla CSS) is a frontend-framework concern (the `typescript` module) — these values are expressible in plain CSS.
