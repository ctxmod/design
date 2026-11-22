# Dark Mode

Dark mode is role-remapping with different contrast targets, not value inversion. Document the pattern; the feature is optional and context-dependent.

Dark mode is a **theme mode** — one value of the orthogonal mode axis that cuts
across the token layers (see the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />).
A mode re-resolves the **semantic → primitive** mapping while role names stay
constant. Dark mode is therefore **role-remapping with different contrast targets
and elevation cues**, NOT value inversion. The most common failure is treating it
as a filter — flipping the light palette's numbers and shipping the result — which
breaks contrast, kills elevation, and over-saturates accents on a dark ground.

This document covers the *pattern*. The color-system view of dark mode lives in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> (surface ladders, the shadow/elevation asymmetry, accent
lightness nudges); this file is the canonical home for the pattern as a whole and
the position on when to ship it.

## The pattern (mandate when offered)

When a product offers dark mode, the implementation must follow this pattern.
These obligations are non-negotiable *given* the feature ships; the feature itself
is not (see Position below).

- **Primitives become mode-aware.** A `surface` primitive carries both a light
  and a dark value. Dark is a property of the primitive ramp, not a transform
  applied after the fact.
- **Semantic tokens swap their primitive reference per mode.** The role
  (`bg-surface`, `text-primary`, `accent`) is stable; only the primitive it points
  to changes when the mode changes. **Components change nothing** — a button still
  references `accent` and renders correctly in both modes because the role
  re-resolves underneath it.
- **Different contrast targets.** Dark surfaces need their own ratios computed
  against the dark ground. Do not reuse light-mode ratios — an accent that cleared
  4.5:1 on white usually needs a lightness nudge to clear it on charcoal. Verify
  contrast in each mode independently (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />
  for the WCAG success criteria).
- **Elevation cues shift.** Shadows barely read on dark grounds. Suggest elevation
  with **lighter raised surfaces and borders** instead — light recedes in dark UIs,
  so raised cards become *lighter*, not darker. This asymmetry is detailed in
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />; do not carry light-mode shadows into dark mode.

## Position: pattern is mandated, feature is optional

Dark mode is a **context-dependent option, not a universal quality mandate.**
There is no scientific consensus that it confers a cognitive benefit, and
readability research favors light mode (dark text on light ground) for long-form
reading. So the position is split:

- **Mandate the pattern.** When dark mode is shipped, it must be done right — the
  obligations above are required, not aspirational.
- **Do not mandate the feature.** Whether to offer dark mode at all is a product
  decision driven by context (audience, usage environment, content type), not a
  quality gate. A product with no dark mode is not deficient for lacking one.

## Obligations

- If dark mode is offered, primitives are mode-aware and semantic tokens swap their
  primitive reference per mode.
- Components reference semantic roles only; no component contains a hardcoded dark
  value or a "if dark then…" branch.
- Contrast is recomputed and verified per mode against the actual mode background.
- Elevation in dark mode uses lighter surfaces and borders, never reused light-mode
  shadows.

## How to verify

- Confirm semantic tokens **swap per mode** — search components for hardcoded dark
  hex values or mode conditionals; finding any is a failure (the swap belongs at the
  token layer, not in the component).
- Toggle the mode and re-run contrast checks against the *dark* background; do not
  assume light-mode ratios transfer.
- Inspect raised surfaces in dark mode: elevation should read via lightness and
  borders, not shadows.

## Anti-patterns

- **Inverting hex values.** Running an invert filter or negating the light palette's
  numbers. This is the canonical dark-mode mistake — it destroys contrast targets,
  over-saturates accents, and breaks elevation.
- **Hardcoding dark values in components.** Any dark-specific value or conditional
  living in a component instead of being resolved through a mode-aware semantic
  token.
- **Reusing light-mode contrast ratios and shadows on a dark ground.** Treating
  dark mode as the same palette under a tint rather than a re-resolved mapping with
  its own targets.
- **Treating dark mode as a universal requirement.** Shipping it as a checkbox quality
  item regardless of whether the product's context warrants it.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
