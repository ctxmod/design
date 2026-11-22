# Storytelling — Cards

Concrete Storytelling styling for the card slot — editorial chapter-like cards with Abril Fatface headlines, Inter body, generous padding, image-led layout.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" /> for Storytelling. A
card reads like a **chapter**: an image or eyebrow sets the scene, an Abril
Fatface headline announces it, and Inter body tells it. Generous padding and
whitespace — not heavy borders — make the grouping (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />). Reach for a card only when a unit repeats in a
collection or genuinely needs a boundary; otherwise let whitespace group.

## The header / body / footer contract

```css
.card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);   /* hairline — restrained chrome */
  border-radius: var(--bs-radius, 0.5rem);
  padding: 2rem;                            /* comfortable density — editorial */
  display: flex;
  flex-direction: column;
  gap: var(--bs-space-flow, 1rem);
}

.card__media { aspect-ratio: 16 / 9; object-fit: cover; border-radius: calc(var(--bs-radius, 0.5rem) - 2px); }
.card__eyebrow { font-family: var(--bs-font-body); font-size: var(--bs-text-caption); color: var(--color-muted); text-transform: uppercase; letter-spacing: 0.08em; }

/* The chapter title — Abril Fatface, the one display moment per card */
.card__title {
  font-family: var(--bs-font-display);
  font-size: var(--bs-h3);
  line-height: var(--bs-leading-display);
  color: var(--color-text);
}

.card__body { font-family: var(--bs-font-body); font-size: var(--bs-text-body); line-height: var(--bs-leading-body); color: var(--color-text); }
.card__footer { margin-block-start: auto; display: flex; gap: 1rem; align-items: center; }
```

Regions are used **consistently across a collection** — every card places media,
title, and footer in the same slots so a grid scans as a rhythm. The card holds
**at most one primary action** in its footer (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/buttons.md" />).

## Interactive vs. static

Make the choice explicit. An **image-led story card** is often a whole-card
target; a settings/metric card is usually static with inner controls.

```css
.card--interactive { cursor: pointer; transition: box-shadow var(--bs-dur-page) var(--bs-ease-page), transform var(--bs-dur-page) var(--bs-ease-page); }
.card--interactive:hover  { box-shadow: 0 8px 28px color-mix(in oklch, var(--color-text) 10%, transparent); transform: translateY(-2px); }
.card--interactive:focus-visible { outline: 3px solid color-mix(in oklch, var(--color-accent) 60%, transparent); outline-offset: 3px; }
```

When a whole-card target also contains a button/link, the inner control stays
independently operable and its hit area must not overlap the card target
ambiguously (the classic card pitfall — resolve it deliberately).

## States

```css
.card[aria-current="true"], .card--selected { box-shadow: inset 0 0 0 2px var(--color-beat); } /* violet beat marks the chosen one */
```

- **Default / hover / focus / active / selected** for interactive cards;
  **loading skeleton / empty / disabled** for data cards.
- Skeletons **match the final card shape** so the grid does not reflow when
  content arrives — a gentle reveal, not a pop (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/brand.md" />).

## Density

`Comfortable` (2rem padding) is the default — it suits the spacious, focused
editorial feel. `Compact` (1rem) exists for dense collections; density is a
systematic token swap, and all cards in one collection share it.

## Anti-patterns

- Wrapping every region in a card until the page is a grid of boxes with no arc.
- A clickable card that swallows its inner button/link.
- Inconsistent title/media/action placement across a collection.
- Two competing primary actions in one card.
- A heavy border/shadow where whitespace alone would group better.
- Body text set in Abril Fatface (reserve the display face for the title).
</content>

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
