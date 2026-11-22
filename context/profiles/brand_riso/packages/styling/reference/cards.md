# Riso — Cards

Riso card styling — paper surface with 2px blue outline and the signature offset print-shadow, near-sharp corners, header/body/footer contract, interactive states with the registration shift.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" /> for Riso. The card is where
the **offset print-shadow** does its most characteristic work: a paper rectangle,
outlined in `--ink-blue`, lifted off the page by a blurless blue misregistration
shadow. It looks like a printed sticker on the sheet.

## Surface, outline, and the print-shadow

- **Surface** — `--paper` (the same sheet; the card is *not* a different
  background, it is paper outlined). `--paper-deep` only for a sunken inner well.
- **Outline** — `2px solid --ink-blue`. The boundary is ink, not a hairline.
- **Shadow** — `--print-shadow-md` by default; `--print-shadow-lg` for the few
  hero cards. Always blue, always blurless. Used **sparingly** — only cards that
  genuinely need a hard boundary or repeat in a collection earn it; otherwise let
  whitespace group (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" />).
- **Corners** — near-sharp: `--radius-card: 4px`. Riso reads as printed, so
  corners stay tight, never pill-soft.

```css
.card { background: var(--paper);
  border: 2px solid var(--ink-blue); border-radius: 4px;
  box-shadow: var(--print-shadow-md);
  padding: 24px; }
.card--hero { box-shadow: var(--print-shadow-lg); }
.card__well { background: var(--paper-deep); border-radius: 4px; }
```

## Header / body / footer contract

- **Header** — title in `--ink-blue` (Space Grotesk 600), optional eyebrow/category
  in caption size, optional overflow action. Establishes what the card is.
- **Body** — primary content in `--text`; this is the reason the card exists.
- **Footer** — actions (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/buttons.md" />) and metadata; at most one pink
  primary action per card.

Across a collection the regions stay in the **same slots and order** so the grid
scans as a rhythm; density is a systematic token swap (comfortable 24px /
compact 12px padding), uniform within one collection.

## States

| State | Applies to | Treatment |
|-------|-----------|-----------|
| **Default** | all | paper + blue outline + `--print-shadow-md` |
| **Hover** | interactive | shadow grows to `--print-shadow-lg` (lifts further) |
| **Focus** | interactive | pink `:focus-visible` ring, ≥3:1 |
| **Active/pressed** | interactive | registration shift: `translate(6px,6px)`, shadow → `--print-shadow-sm` |
| **Selected** | selectable | outline → `--ink-pink`, pink check/corner marker |
| **Loading / skeleton** | collections | paper blocks matching final layout, blue hairline |
| **Empty** | data cards | meaningful empty state, not a blank box (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/feedback.md" />) |
| **Disabled** | interactive | muted outline, no shadow |

```css
.card--interactive { cursor: pointer;
  transition: transform var(--dur-instant) var(--ease-out),
              box-shadow var(--dur-instant) var(--ease-out); }
.card--interactive:hover { box-shadow: var(--print-shadow-lg); }
.card--interactive:focus-visible { outline: 3px solid var(--ink-pink);
  outline-offset: 3px; }
.card--interactive:active { transform: translate(6px, 6px);
  box-shadow: var(--print-shadow-sm); }
.card--selected { border-color: var(--ink-pink); }
```

The **selected state is pink** (interaction color); the **active press** drives
the card into its offset shadow, the signature registration gesture at card scale.
Skeletons match the card's real shape to prevent reflow when data lands.

## Responsibilities & anti-patterns

- Group genuinely related content; consistent regions across a collection; **one**
  primary action max inside a card.
- Resolve the **interactive-vs-static** choice explicitly; if interactive, provide
  the full control-state set, the pink focus ring, and keyboard operability.
- **Boundaries earn their keep** — the blue outline + offset shadow is a strong,
  expensive mark; don't apply it to every region or the page becomes a wall of
  printed boxes with no hierarchy.
- Don't nest a button inside a clickable card ambiguously; don't swap the offset
  shadow for a soft drop shadow; don't round corners into pills.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/brand.md" />
