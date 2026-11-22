# Expressive — Cards

Expressive cards — color-blocked pink/blue headers, thick ink borders with hard offset shadow, sticker layering, slight rotate/offset on hover, mono headers; static and interactive variants with full states.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" /> for Expressive. Cards
are color-blocked, ink-outlined, and sticker-layered, with a playful tilt on hover.
Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/brand.md" />. The header/body/footer contract and the
interactive-vs-static fork are inherited unchanged; this file fills in the look.

## Card shape

```css
.be-card {
  background: var(--be-surface);
  border: 2px solid var(--be-border);
  border-radius: var(--be-radius, 14px);
  box-shadow: 4px 4px 0 var(--be-ink);   /* hard offset, never a soft blur */
  overflow: visible;                       /* lets stickers spill the edge */
  transition: transform var(--be-dur-fast) var(--be-ease-spring),
              box-shadow var(--be-dur-fast) var(--be-ease-out);
}
```

## Header / body / footer

The header is a **color block** — solid pink or blue with mono-strong title — which
makes a card grid scan as a rhythm of accent blocks. Alternate pink/blue headers
across a collection to express the dual accent.

```css
.be-card__header { background: var(--be-pink); color: #fff;
                   padding: 14px 16px; border-bottom: 2px solid var(--be-border);
                   font: var(--be-weight-strong) var(--be-text-h3)/1.1 var(--be-font); }
.be-card--blue .be-card__header { background: var(--be-blue); }
.be-card__body   { padding: 16px;
                   font: var(--be-weight-body) var(--be-text-body)/1.6 var(--be-font); }
.be-card__footer { padding: 12px 16px; border-top: 2px solid var(--be-border);
                   display: flex; gap: 8px; } /* one primary action max (see buttons) */
```

Use regions consistently across a collection (title/media/actions in the same slots).
Density is a token swap: `--be-card-pad: 16px` comfortable, `10px` compact — all
cards in one grid share it.

## Sticker layering

The signature flourish: a small badge offset and rotated over the card's corner with
its own hard shadow.

```css
.be-card__sticker {
  position: absolute; top: -10px; right: -10px;
  transform: rotate(6deg);
  background: var(--be-blue); color: #fff;
  border: 2px solid var(--be-border); border-radius: 6px;
  padding: 4px 8px;
  font: var(--be-weight-strong) var(--be-text-caption)/1 var(--be-font);
  box-shadow: 3px 3px 0 var(--be-ink);
}
```

## Interactive vs static

A **static** card is a presentation container; its inner buttons are the interactive
parts. An **interactive** card is itself a target and must behave like a control —
hover, focus, active, selected — with a visible focus ring and keyboard operability.
Resolve the nested-action conflict deliberately (one whole-card target plus clearly
separated inner controls).

```css
.be-card--interactive { cursor: pointer; }
.be-card--interactive:hover  { transform: translate(-2px, -2px) rotate(-1deg);
                               box-shadow: 6px 6px 0 var(--be-ink); }  /* tilt + lift */
.be-card--interactive:focus-visible { outline: 3px solid var(--be-blue); outline-offset: 4px; }
.be-card--interactive:active { transform: translate(2px, 2px); box-shadow: 2px 2px 0 var(--be-ink); }
.be-card--selected { border-color: var(--be-pink); box-shadow: 4px 4px 0 var(--be-pink); }
```

## States

- **Default / hover / focus / active** — as above; static cards skip hover/active.
- **Selected** — pink border + pink offset shadow (dual-accent: blue for an
  alternate select group).
- **Loading / skeleton** — a skeleton matching the card's shape (color-block header
  rendered as a grey bar) to prevent reflow when data lands.
- **Empty** — a meaningful empty state inside the card, not a blank box (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/feedback.md" />).

## Anti-patterns

- Soft blurred shadows — Expressive cards use the hard offset shadow.
- A clickable card that swallows its inner buttons; keep targets separated.
- Inconsistent region placement across a grid.
- Two competing primary actions in the footer.
- Over-rotated stickers everywhere — one per card, ≤ ~6°, intentional.
- Reaching for a card where whitespace alone would group (umbrella restraint rule).

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
