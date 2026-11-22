# Spacing Scale

Spacing as the invisible skeleton — base units, linear vs. non-linear scales, rhythm, density, whitespace, and its bond with the type scale.

Spacing is the invisible skeleton of an interface. Padding, margins, and gaps
control grouping, rhythm, and density more than any visible element does. A
consistent spacing system is what separates a designed interface from an
assembled one — and it is the most common place ad-hoc "magic numbers" sneak in.

This document is about the *system*. The CSS units (rem, px, logical properties)
belong to the medium tier; here we define how a scale is built and used.

## A spacing scale, not arbitrary values

Pick a **base unit** and derive every spacing value from it. The two standard
bases:

- **4px base** — fine-grained control, good for dense UIs and data tools.
- **8px base** — fewer steps, enforces more breathing room, common in marketing
  and consumer apps (a 4px half-step is allowed for tight inline gaps).

Every gap in the product should be a step on this scale. A `13px` margin next to a
`16px` one is a defect, not a refinement (see the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/rules/token_usage.md" />).

## Linear vs. non-linear scales

A **linear** scale (4, 8, 12, 16, 20, 24, …) is predictable but offers too many
near-identical large steps and not enough separation at the top.

A **non-linear** scale grows the gaps as the values increase, which matches how
spacing is actually used — small elements need fine control, large layout gaps
need bold jumps:

| Token | Value (4px base) | Typical use |
|-------|------------------|-------------|
| `space-0` | 0 | reset |
| `space-1` | 2 | hairline inset |
| `space-2` | 4 | icon-to-text, tight inline |
| `space-3` | 8 | related items, list rows |
| `space-4` | 12 | default element gap |
| `space-5` | 16 | internal card padding |
| `space-6` | 24 | section padding |
| `space-7` | 32 | between groups |
| `space-8` | 48 | major section break |
| `space-9` | 64 | page region break |
| `space-10` | 96 | hero / page top |

The exact values are a brand/medium decision; the *shape* (geometric-ish growth)
is the principle. Larger jumps near the top make the difference between "section
gap" and "page gap" unmistakable, reinforcing <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />.

## Rhythm

Rhythm is the regular repetition of spacing that lets the eye predict where the
next element sits. It comes from:

- **Vertical rhythm** — consistent spacing between stacked blocks, ideally
  aligned to a baseline grid derived from the body line height (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />). When gaps are multiples of one unit, the page
  feels settled.
- **Consistent insets** — the same component always has the same internal
  padding. A card's padding does not change because of what is inside it.
- **The law of proximity** — space encodes relationship. Items closer together
  read as a group; more space means a stronger boundary. Spacing *is* grouping —
  this is the Gestalt proximity law (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" /> and
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />).

A frequent bug: equal space above and below a heading. The heading belongs to the
content *after* it, so it should sit closer to that content (less space below,
more above). Spacing should express the structure, not distribute evenly.

## Density and whitespace

**Density** is the inverse of spacing. The scale lets you express density
deliberately rather than accidentally:

- **Comfortable** density (generous steps) for reading, onboarding, decisions.
- **Compact** density (smaller steps) for expert tools and data tables, where
  more information per screen is the goal (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />).

Offer density as a *systematic* choice — e.g. a compact mode that swaps the
component-level spacing tokens — not as scattered tightening of individual
elements.

**Whitespace is a design element, not leftover space.** Empty area is what gives a
focal point room to be a focal point. Generous whitespace signals calm, quality,
and confidence; cramped layouts signal anxiety and clutter. Negative space is
content: it does the work of separating, grouping, and emphasizing without adding
a single visible mark.

## Spacing and the type scale are siblings

Spacing and type are not independent systems. They share a base and a sense of
proportion:

- Vertical gaps that are multiples of the body line height keep text on a rhythm.
- The spacing ratio and the type ratio should feel related — a dramatic type
  scale (large ratio) paired with a timid spacing scale feels mismatched.
- Component padding scales with the type it contains: a large CTA needs more
  padding than a small inline button so the text-to-edge proportion stays
  constant (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />).

Treat the spacing scale, the type scale, and the radius scale as one coordinated
system expressing a single design language (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />).
