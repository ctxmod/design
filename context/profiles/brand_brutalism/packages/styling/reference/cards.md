# Brutalism — Cards

Brutalism cards — thick-bordered boxes, zero radius, no soft shadow (hard offset block only), visible thick dividers between header/body/footer regions.

Concrete styling for the umbrella's
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" />, in the Brutalism brand. A card is a
**thick-bordered box** with sharp corners and exposed internal structure — the
header / body / footer regions are separated by real, visible dividers, not faint
hairlines. Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/brand.md" />.

## The box

```css
.bb-card {
  background: var(--bb-surface);
  border: var(--bb-border-w) solid var(--bb-border);
  border-radius: 0;
  /* No box-shadow by default. Elevation, when needed, is a hard offset block: */
}
.bb-card--raised { box-shadow: 8px 8px 0 0 var(--bb-text); }  /* hard, zero blur */
```

A card earns its border by grouping a genuine unit (a product, a metric, an
article preview). Brutalism's border *is* the grouping signal — but the umbrella's
caution still holds: don't wrap every region in a box. Where whitespace alone
groups, use space, not another bordered block.

## The header / body / footer contract

The regions are made **visible by thick dividers** — the structure is exposed, per
the brand essence.

```css
.bb-card__header,
.bb-card__footer { padding: 1rem 1.25rem; }
.bb-card__body   { padding: 1.25rem; }

.bb-card__header { border-block-end: var(--bb-border-w) solid var(--bb-border); }
.bb-card__footer { border-block-start: var(--bb-border-w) solid var(--bb-border); }

.bb-card__title  { font-weight: var(--bb-w-heavy); text-transform: uppercase;
                   letter-spacing: var(--bb-track-tight); font-size: var(--bb-text-lg); }
.bb-card__eyebrow{ font-weight: var(--bb-w-light); text-transform: uppercase;
                   letter-spacing: var(--bb-track-wide); font-size: var(--bb-text-sm); }
```

A collection of cards uses the regions **consistently** so the grid scans as a
rhythm of identical blocks. Within one collection, density is a single token swap
(`--bb-card-pad`), not per-card tweaking.

## Interactive vs. static

- **Static card** — the box groups content; inner
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/buttons.md" /> are the interactive parts.
- **Interactive card** — the whole box is a target and must carry the full control
  state set. The brutalist treatment: hover and focus drive a **hard offset block**
  and a **border-thickness jump**, not a soft lift.

```css
.bb-card--interactive { cursor: pointer;
  transition: box-shadow var(--bb-dur-fast) var(--bb-ease-snap); }
.bb-card--interactive:hover         { box-shadow: 8px 8px 0 0 var(--bb-text);
                                      transform: translate(-3px, -3px); }
.bb-card--interactive:focus-visible { outline: none; border-width: var(--bb-border-w-bold); }
.bb-card--interactive[aria-pressed="true"],
.bb-card--selected                  { border-color: var(--bb-terracotta);
                                      border-width: var(--bb-border-w-bold); }
```

Resolve the **nested-action conflict** deliberately: an interactive card keeps its
inner buttons independently operable with non-overlapping targets.

## States

| State | Applies to | Brutalist expression |
|-------|-----------|----------------------|
| **Default** | all | Flat bordered box. |
| **Hover / Active** | interactive | Hard offset block + slight translate (mechanical). |
| **Focus** | interactive | Bold (4px) ink border, no ring. |
| **Selected** | selectable | Terracotta bold border. |
| **Loading / skeleton** | collections | Bordered box with blocky concrete bars matching the final layout — no shimmer. |
| **Empty** | data cards | A meaningful empty state, not a blank box (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/feedback.md" />). |
| **Disabled** | interactive | Concrete fill, border kept visible. |

## Responsibilities

- Group genuinely related content; the border asserts "these belong together".
- **One primary action at most** inside the card (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/buttons.md" />).
- Resolve interactive vs. static explicitly; interactive cards get the full state
  set and keyboard support.
- Skeletons are **blocky** (concrete bars), matching shape to prevent reflow.

## Anti-patterns

- Rounded corners or a blurred drop shadow on the box.
- A grid of bordered boxes with no hierarchy (over-carding).
- Inconsistent region placement across a collection.
- A shimmer/pulse skeleton — keep loading blocky and still.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
