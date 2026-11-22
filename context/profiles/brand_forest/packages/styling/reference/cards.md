# Forest — Cards

Forest concrete card styling — rounded flat panels on a lighter green surface step, hairline border (no shadow), header/body/footer padding, interactive states with lime focus, skeletons.

Concrete Forest styling for the **cards** slot. Fills the umbrella
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" /> — the header/body/footer regions, the
interactive-vs-static fork, the state set, density variants — with Forest values.
Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />.

The Forest card is the system's signature surface: **rounded, flat, shadow-free.**
It is one green step *lighter* than the page (`--forest-surface-raised`), separated
by surface contrast and an optional hairline border — never by a drop shadow (in a
dark UI, light recedes; raise by lightening, not by shadow — see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).

## Surface & shape

| Property | Value |
|----------|-------|
| Fill | `--forest-surface-raised` (`#3E6402`) — one step lighter than `--forest-surface` |
| Border | optional 1px `--forest-border` hairline (use when cards sit on the same surface step) |
| Radius | `--forest-radius-lg` (16px); large hero panels use `--forest-radius-xl` (24px) |
| Shadow | **none** |

Cards on the *deep* surface can drop the border (the surface step alone separates
them); cards on the *raised* surface keep the hairline so the boundary reads.

## Region padding (header / body / footer)

Regions are optional but consistent across a collection (every card places title,
media, actions in the same slots). 8px-rhythm padding:

| Density | Padding | Region gap |
|---------|---------|------------|
| **Comfortable** (default) | 24px | 16px between regions |
| **Compact** (dense dashboards) | 16px | 12px between regions |

- **Header** — title in `--forest-heading` (H4), optional overline/eyebrow in
  `--forest-brand-medium`, optional media or overflow action. A 1px
  `--forest-border` divider below the header is optional.
- **Body** — content in `--forest-body`; metrics/figures may use the mono face.
- **Footer** — actions (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/buttons.md" /> — at most one lime primary per
  card) and metadata in `--forest-body` @ 80%.

Density is a systematic token swap; all cards in one collection share a density.

## Interactive vs static

- **Static card** — presentation container; only its inner controls are
  interactive.
- **Interactive card** (whole card is a target) behaves like a control and gets the
  full state set below, a visible focus ring, and keyboard operability. Resolve the
  **nested-action conflict** deliberately: a clickable card with inner buttons must
  keep the inner controls independently operable and non-overlapping.

## States

| State | Treatment |
|-------|-----------|
| **Default** | raised-surface fill, optional hairline |
| **Hover** (interactive) | border → `--forest-brand`; fill lifts to `color-mix(in oklch, var(--forest-surface-raised) 92%, var(--forest-brand-medium))` — subtle, no shadow |
| **Focus** (interactive) | 2px `--forest-brand-medium` ring, 2px offset |
| **Active/pressed** | fill settles back ~1 step darker |
| **Selected** | 2px `--forest-brand` border + lime-tinted fill wash |
| **Loading / skeleton** | skeleton blocks in `color-mix(in oklch, var(--forest-surface-raised) 80%, var(--forest-surface-deep))`, matching final layout to prevent reflow |
| **Empty** | meaningful empty state (icon + reason + next action), not a blank box (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/feedback.md" />) |
| **Disabled** (interactive) | reduced contrast, `cursor: not-allowed` |

Hover/focus transitions sit in the *fast* band (~200ms ease-in-out); skeletons
match the card shape so data load doesn't reflow the grid (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

## CSS tokens

```css
.forest-card {
  --forest-card-bg: var(--forest-surface-raised);
  --forest-card-border: var(--forest-border);
  --forest-card-radius: var(--forest-radius-lg);   /* 16px */
  --forest-card-pad: 24px;

  background: var(--forest-card-bg);
  border: 1px solid var(--forest-card-border);
  border-radius: var(--forest-card-radius);
  padding: var(--forest-card-pad);
  /* no box-shadow — Forest is flat */
}
.forest-card--compact { --forest-card-pad: 16px; }
.forest-card--interactive {
  transition: border-color var(--forest-dur) var(--forest-ease),
              background var(--forest-dur) var(--forest-ease);
}
.forest-card--interactive:hover { border-color: var(--forest-brand); }
.forest-card--interactive:focus-visible {
  outline: 2px solid var(--forest-brand-medium);
  outline-offset: 2px;
}
.forest-card--selected {
  border: 2px solid var(--forest-brand);
  background: color-mix(in oklch, var(--forest-surface-raised) 88%, var(--forest-brand));
}
```

## Anti-patterns (Forest-specific)

- Adding a drop shadow to lift a card — Forest raises by lightening the green, not
  by shadow.
- Same-color card on same-color page with no border — the boundary vanishes; step
  the surface or add the hairline.
- Wrapping every region in a card until the page is a grid of green boxes — use
  whitespace where it groups better.
- Two competing lime primaries inside one card footer.
- A loading state that pops content in and reflows the grid (use a matching
  skeleton).
