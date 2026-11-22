# Storytelling brand

The **Storytelling** brand profile. A narrative-driven aesthetic that treats
every interface as a story with a beginning, middle, and end — a cohesive
emotional journey. It fills the abstract component slots defined by the
`core` umbrella with concrete styling, expressed through
the web primitives established by `web`.

```
core                   ← principles + abstract component taxonomy
  └── web               ← web concretization (CSS, viewports, a11y, perf)
        └── brand_storytelling  ← this profile: Inter + Abril Fatface, three-act, pacing
```

## What this profile decides

- **The palette** — a deliberately restrained, editorial set (blue "next step",
  violet "important beat", conventional status hues) on a blank-page white
  ground, so typography and pacing carry the narrative. See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/brand.md" />.
- **The type pairing** — Inter for body (the narrator's voice) and Abril Fatface
  for display (the chapter title). The Inter-to-Abril switch is the most dramatic
  visual shift in the system.
- **Motion** — slow, scroll-tied reveals that let the story unfold; page-turn
  easing; mandatory reduced-motion fallbacks.
- **The three-act structure** — how a page or flow maps to setup / confrontation
  / resolution, and how spacing and pacing differ across the acts.
- **Component styling** — concrete looks for every umbrella slot, in its own file:
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/buttons.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/inputs.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/cards.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/navigation.md" />
  - <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/feedback.md" />

## What this profile does NOT decide

- **Abstract principles** — color theory, the spacing model, the component
  contracts. Those live in the `core` umbrella.
- **Web mechanics** — container queries, focus-ring plumbing, `prefers-reduced-motion`
  wiring. Those live in `web` and are inherited unchanged.
- **Framework plumbing** — React, Tailwind config, shadcn registries. Those are
  a frontend-framework concern (the `typescript` module). This profile speaks plain CSS custom properties.

## When to use Storytelling

Reach for this brand when the surface needs an **emotional arc**: brand and
launch pages, onboarding flows, case-study and editorial content, mission- and
cause-driven products, fundraising campaigns, long-form reading. Avoid it for
dense, utilitarian tooling where pacing and display drama would only slow the
user down.
</content>
</invoke>
