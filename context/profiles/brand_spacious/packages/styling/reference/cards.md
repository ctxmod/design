# Spacious — Cards

Spacious card styling — soft-shadow surfaces, generous internal padding, thin borders, large margins between cards, breathing-room header/body/footer.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" /> for Spacious. The slot
owns the header/body/footer contract, the static-vs-interactive fork, and the state
set; this file supplies the look. The Spacious signature on a card is **room** —
generous internal padding, a soft diffused shadow, a thin border, and ample margin
*between* cards so each reads as its own calm unit.

## Foundations

Cards lean hardest on the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/brand.md" /> ethos: whitespace groups (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />), so the card border earns its keep only by
adding gentle elevation, never a hard frame.

```css
.card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);   /* thin hairline */
  border-radius: var(--radius-lg);         /* 12px */
  box-shadow: var(--shadow-soft);          /* soft, diffused */
  padding: var(--space-5);                 /* 32px — generous internal padding */
}
```

## Spacing between cards

A Spacious card collection breathes. Inter-card gaps use a large step from the 8pt
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" /> so the grid reads as a calm rhythm, not a
packed grid of boxes.

```css
.card-grid {
  display: grid;
  gap: var(--space-5);                      /* 32px between cards */
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
}
```

## Header / body / footer

Each region is given room; they are separated by spacing, not rules. A title in
Montserrat anchors the open space.

```css
.card__header { font-family: var(--font-display); font-weight: 600; font-size: 18px;
                margin-block-end: var(--space-3); }   /* 16px */
.card__body   { font-family: var(--font-body); line-height: 1.6;
                color: var(--color-text); }
.card__footer { display: flex; gap: var(--space-3); align-items: center;
                margin-block-start: var(--space-4); } /* 24px */
```

Use the regions consistently across a collection (umbrella rule) so the grid scans
as a rhythm. At most one primary action lives in the footer.

## Static vs. interactive

A static card is a presentation container — its inner buttons/links are the
interactive parts. An interactive card (the whole surface is a target) takes the
full control state set below and a visible focus ring; resolve nested-action
conflicts deliberately.

## States

| State | Treatment |
|-------|-----------|
| **Default** | Soft shadow, hairline border, resting surface |
| **Hover** (interactive) | Shadow deepens slightly — a calm lift, no movement |
| **Focus** (interactive) | `0 0 0 3px` accent ring, never suppressed |
| **Active** (interactive) | Shadow settles back; brief, immediate |
| **Selected** | Accent border + faint accent-tinted surface |
| **Loading / skeleton** | Neutral skeleton matching the card's shape — no reflow |
| **Empty** | Meaningful empty state inside the padding, not a blank box |

```css
.card--interactive { transition: box-shadow var(--dur-base) var(--ease-standard); cursor: pointer; }
.card--interactive:hover { box-shadow: 0 2px 6px rgba(17,24,39,.08), 0 8px 24px rgba(17,24,39,.07); }
.card--interactive:focus-visible { outline: none; box-shadow: 0 0 0 3px rgba(59,130,246,.4); }
.card[aria-selected="true"] { border-color: var(--color-accent); background: #F5F8FF; }

@media (prefers-reduced-motion: reduce) { .card--interactive { transition-duration: 1ms; } }
```

## Density

Spacious defaults to **comfortable** density. A compact variant exists for denser
contexts but still pads more than other brands — it swaps padding tokens
systematically, never per-card.

```css
.card--compact { padding: var(--space-4); }   /* 24px, still roomy */
```

See <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" /> for the CSS
carriers behind these tokens.

## Anti-patterns (brand-specific)

- Tight `padding < --space-4` or cards packed edge-to-edge — kills the breathing
  room that defines the brand.
- A hard, dark drop shadow or a heavy border — Spacious elevation is soft.
- Wrapping every region in a card until the page is a grid of boxes; prefer
  whitespace grouping first (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />).
