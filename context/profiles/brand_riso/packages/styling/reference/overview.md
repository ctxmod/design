# Riso brand

The **Riso** brand tier — a two-color, risograph-inspired aesthetic that
specializes `web` with concrete styling. Riso renders
the whole product on a single warm off-white paper surface, structures it in
deep federal blue, and reserves a fluorescent pink for interaction. Its signature
mechanic is the **offset print-shadow** — a blurless, blue, misregistration
double-edge that makes the UI feel printed by hand rather than rendered by a
browser.

```
core                   ← principles + abstract component taxonomy
  └── web               ← web concretization (CSS, viewports, a11y, perf)
        └── brand_riso  ← THIS: Riso palette, Space Grotesk, offset print-shadow
```

This profile inherits the web layer unchanged (it does not re-derive container
queries, focus-ring mechanics, or reduced-motion handling) and fills the
umbrella's abstract component slots
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />)
with Riso values, expressed through the CSS custom properties established in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />.

## What lives here

All Riso concretization lives in this profile's `styling` package:

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/brand.md" /> — the essence,
  the full color palette, Space Grotesk type, motion vocabulary, and the
  signature offset print-shadow.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/buttons.md" /> —
  the action-invocation slot in Riso (pink primary + offset shadow).
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/inputs.md" /> —
  blue outlines on paper, pink focus ring.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/cards.md" /> —
  paper surface, blue outline, the print-shadow.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/navigation.md" /> —
  blue wayfinding, pink active state.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/feedback.md" /> —
  severity mapped onto the two-color logic plus reserved status hues.

## The constraint is the brand

Riso is defined as much by what it forbids as by what it uses. **Blue is the
ink** (text, headings, outlines, dividers, print-shadow); **pink drives
interaction** (primary actions, active, selected, focus, emphasis). One
continuous paper canvas — never alternating section backgrounds. No gradients,
no soft drop shadows, no third decorative accent. Status hues (success / warning
/ danger) are the only sanctioned colors beyond blue and pink, and they appear
only in feedback. Hold the constraint and the aesthetic holds; break it and Riso
becomes generic.
