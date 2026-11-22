# Expressive brand

A **brand tier** profile in the user-facing-surface design stack. Expressive is a
vibrant, personality-driven design system: a single monospaced typographic voice
(IBM Plex Mono in every role), a pink + blue dual-accent palette, the full 100–900
weight spectrum used as hierarchy, and playful-but-structured layouts that feel
energetic and creative while staying sound.

```
core                   ← principles + abstract component taxonomy
  └── web               ← web concretization (CSS, viewports, a11y, perf)
        └── brand_expressive  ← this profile: concrete Expressive palette, type, motion, components
```

This profile fills the umbrella's abstract component slots
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />)
with **concrete Expressive values**, expressed through the web primitives the
`web` medium establishes — CSS custom properties
for tokens, compositor-only properties for motion, semantic HTML for structure.
It does not re-derive how container queries, focus rings, or reduced-motion work;
those are inherited unchanged.

## What lives here

- **<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/brand.md" />** — the
  identity card: essence, dual-accent palette, the IBM Plex Mono voice and
  weight-as-hierarchy model, spring motion vocabulary, shape & surface, do/don't.
- **Component specializations** — one file per umbrella slot, giving Expressive's
  concrete values, token names, and states:
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/buttons.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/inputs.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/cards.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/navigation.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/feedback.md" />

## How to use it

Read <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/brand.md" /> first
for the tokens, then a component file for build-ready values. Tokens are CSS custom
properties (`--be-*`); see the

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />

doc for the carrier mechanism. The framework that ships them (Tailwind, shadcn,
vanilla CSS) is a frontend-framework concern (the `typescript` module) — these values are expressible in plain CSS.
