# Forest — Buttons

Forest concrete button styling — lime primary with dark text, deep-surface secondary, ghost, warm-red danger; full state set, radius/padding tokens, flat (no shadow), lime focus ring.

Concrete Forest styling for the **buttons** slot. This fills the umbrella
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" /> (variants, sizing, the full state
set, responsibilities) with Forest's values; read that for *what* a button must
do, this for *how* it looks in Forest. Tokens come from
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />.

Forest buttons are **flat** (no shadow), **rounded** (`--forest-radius-md`,
10px), and use the lime brand as scarce signal. Layout stays stable across states
(see umbrella responsibilities).

## Variants

| Variant | Fill | Text | Border |
|---------|------|------|--------|
| **Primary** | `--forest-brand` (`#A1DA02`) | `--forest-on-brand` (`#16270A`) — dark for contrast | none |
| **Secondary** | `--forest-surface-deep` (`#1F3400`) | `--forest-heading` | 1px `--forest-border` |
| **Ghost / tertiary** | transparent | `--forest-brand-medium` | none |
| **Danger** | `--forest-danger` (`#FF5C49`) | `--forest-danger-fg` (`#1F3400`) | none |
| **Link-style** | transparent | `--forest-brand-medium`, underlined | none |

Rules (from the umbrella): **one primary per view**; danger is an intent layered on
emphasis; variants come from these tokens, not per-screen invention. The dark
text on lime is mandatory — lime text on green fails contrast (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />).

## Sizing

Padding scales with type so the text-to-edge ratio stays constant; the interactive
target stays **≥ 44px** even for small buttons (pad the hit area, don't shrink it).

| Size | Padding (block × inline) | Font | Min height |
|------|--------------------------|------|------------|
| Small | 6px × 12px | 0.83rem | 44px (padded hit area) |
| Medium | 10px × 18px | 1rem | 44px |
| Large | 14px × 24px | 1.06rem | 48px |

Use logical properties (`padding-inline` / `padding-block`). A full-width option
exists for mobile and stacked contexts. Icon-only buttons keep an accessible name
and the same target size.

## States

Flat throughout — feedback comes from fill/border/ring changes, not shadow.
Hover/press are in the *instant* band (~130ms); see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />.

| State | Primary | Secondary | Ghost |
|-------|---------|-----------|-------|
| **Default** | lime fill | deep-surface + border | transparent |
| **Hover** | fill → `--forest-brand-medium` | border → `--forest-brand`, fill slightly lighter | bg `color-mix(in oklch, var(--forest-brand) 12%, transparent)` |
| **Active/pressed** | fill darkened ~8% (`color-mix` toward `--forest-surface-deep`) | bg → `--forest-surface` | bg ~18% lime mix |
| **Focus** | 2px ring `--forest-brand-medium`, 2px offset | same ring | same ring |
| **Disabled** | fill `color-mix(in oklch, var(--forest-brand) 40%, var(--forest-surface))`, text 55% opacity, `cursor: not-allowed` | desaturated, reduced contrast (still readable) | text 45% opacity |
| **Loading** | inline spinner replaces label, **width held stable**, double-submit blocked | same | same |

Notes: distinguish **disabled** (can't act yet — surface a reason via tooltip)
from **loading** (acting now). Never suppress the focus ring; it must clear ≥ 3:1
(the lime-medium ring does). Don't rely on color alone for danger/disabled — pair
with icon/position (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).

## CSS tokens

```css
.forest-btn {
  --forest-btn-bg: var(--forest-brand);
  --forest-btn-fg: var(--forest-on-brand);
  --forest-btn-radius: var(--forest-radius-md);   /* 10px */
  --forest-btn-ring: var(--forest-brand-medium);

  background: var(--forest-btn-bg);
  color: var(--forest-btn-fg);
  border-radius: var(--forest-btn-radius);
  padding-block: 10px;
  padding-inline: 18px;
  border: 0;
  font-weight: 500;
  transition: background var(--forest-dur-fast) var(--forest-ease);
}
.forest-btn:hover { --forest-btn-bg: var(--forest-brand-medium); }
.forest-btn:focus-visible {
  outline: 2px solid var(--forest-btn-ring);
  outline-offset: 2px;
}
.forest-btn--secondary {
  --forest-btn-bg: var(--forest-surface-deep);
  --forest-btn-fg: var(--forest-heading);
  border: 1px solid var(--forest-border);
}
.forest-btn--ghost {
  --forest-btn-bg: transparent;
  --forest-btn-fg: var(--forest-brand-medium);
}
.forest-btn--danger {
  --forest-btn-bg: var(--forest-danger);
  --forest-btn-fg: var(--forest-danger-fg);
}
```

## Anti-patterns (Forest-specific)

- Lime *text* on a green button — fails contrast; lime is a fill, dark text rides
  on it.
- Adding a drop shadow or gradient to a button — breaks the flat language.
- More than one lime primary in a view — destroys hierarchy and dilutes the signal.
- A focus ring removed or in a low-contrast green — the keyboard user is lost.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/feedback.md" />
