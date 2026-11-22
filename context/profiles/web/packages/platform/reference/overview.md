# Web medium

The **medium tier** of the user-facing-surface design stack. This profile takes
the framework-agnostic principles defined by the `core`
umbrella and concretizes them for the web platform: the DOM, CSS, SVG, the
browser's rendering pipeline, the multi-viewport reality, and the web's
accessibility model.

It sits between the abstract umbrella above it and the concrete brand profiles
below it:

```
core                   ← principles + abstract component taxonomy (framework-agnostic)
  └── web               ← this profile: web concretization (CSS, viewports, a11y, perf)
        └── brand_<b>   ← brand: concrete palette, type, motion timings, signature
```

## What lives here

- **Principles** (this `platform` package) —
  the web-specific layer the umbrella deliberately left abstract:
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/responsive_layout.md" /> —
    fluid layout, container vs media queries, fluid type, CLS as a design failure.
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" /> —
    CSS transitions/animations, View Transitions, `prefers-reduced-motion`,
    compositor-friendly motion.
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_accessibility.md" /> —
    semantic HTML, ARIA, WCAG contrast, focus management, keyboard nav.
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/rendering_performance.md" /> —
    the perf consequences of visual decisions: layers, layout thrash, images, fonts.
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" /> —
    CSS custom properties, `@layer`, modern selectors, OKLCH, SVG/Canvas.
- **Rules** (`css_conventions`, `responsive_discipline` in this package) —
  short guardrails on web CSS hygiene and responsive discipline.

## What does NOT live here

- **Abstract principles** — visual hierarchy, color theory, the spacing model,
  the component taxonomy. Those stay in the `core` umbrella;
  this profile references them and maps them onto web primitives.
- **Framework plumbing** — React, Vue, Svelte components; Tailwind config; shadcn
  registries. That belongs to the frontend-framework modules (`github.com/ctxmod/typescript/context`). This profile speaks **plain CSS
  and platform primitives**; where Tailwind implements a primitive, it is noted as
  *one delivery mechanism*, cross-referenced to
  `v4/reference/architecture.md` in `github.com/ctxmod/typescript/context` (profile `tailwind`),
  not adopted as the medium's vocabulary.
- **Concrete brand values** — chosen hex palettes, typefaces, exact motion
  timings, the signature element. Those belong to brand profiles that extend this
  one.

## How brand profiles use this

A `brand_<style>` profile extends `web` and inherits this web layer
unchanged: it does not re-derive how container queries work or how focus rings are
made visible. It fills the umbrella's abstract component slots
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />) with
concrete styling, expressed through the web primitives this profile establishes —
CSS custom properties for tokens, compositor-only properties for motion, semantic
HTML for structure.
