# Forest — Feedback

Forest concrete feedback styling — flat toasts/alerts/banners with severity (lime success, amber warning, warm-red error, deep-surface info), icon+label always, progress and empty states.

Concrete Forest styling for the **feedback** slot. Fills the umbrella
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" /> — the family (toast, alert, banner,
inline validation, loading/progress, empty state), the severity contract,
dismissibility, the voice of failure — with Forest values. Tokens from
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />.

Feedback is where Forest's palette earns its discipline: because **success is the
brand lime and the surface is green**, severity must *never* rely on color alone —
every message carries an **icon and label** so it survives color-blindness and the
green ground (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> and
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />). All feedback surfaces
are flat (no shadow).

## The severity contract

| Severity | Accent | Surface | Icon |
|----------|--------|---------|------|
| **Info** | `--forest-brand-medium` edge | `--forest-surface-deep` | ℹ info |
| **Success** | `--forest-success` (`#A1DA02`, the brand lime) | lime-tinted deep surface | ✓ check |
| **Warning** | `--forest-warning` (`#F2B705`, amber) | amber-tinted deep surface | ⚠ triangle |
| **Error / danger** | `--forest-danger` (`#FF5C49`, warm red) | red-tinted deep surface | ✕ / alert |

- **Success is lime** (affirming, on-brand) — but because lime is also the brand
  accent, success messages always lead with the check icon and "Success"/affirming
  copy so they don't read as a generic highlight.
- **Warning (amber) is deliberately not lime** so it's distinguishable from
  success on a green ground.
- **Error is a warm red** that cuts through both the green ground and the lime
  accent — the one hue Forest reserves strictly for failure (never decorative).
- Severity is consistent everywhere; prominence scales with severity (errors
  interrupt more than info).

Tinted surfaces derive from the accent via `color-mix`, e.g.
`color-mix(in oklch, var(--forest-danger) 14%, var(--forest-surface-deep))`, with a
left accent border in the full accent color.

## The family

- **Toast / snackbar** — transient confirmation ("Saved"), auto-dismiss after a
  few seconds (longer for more text), bottom or top corner on
  `--forest-surface-raised`, `--forest-radius-md`, flat. Never stack a wall of
  toasts — queue or collapse. Never auto-dismiss errors.
- **Alert** — inline, tied to a region; tinted surface + accent left border + icon
  + message; manual dismiss; persists until resolved.
- **Banner** — page/app-level; full-width tinted strip with icon, message, and an
  action; persistent until addressed.
- **Inline validation** — field-level (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/inputs.md" />); `--forest-danger`
  border + icon + fix-it message.
- **Loading / progress** — see below.
- **Empty state** — see below.

## Loading & progress

- **Indeterminate** — calm continuous spinner (`--forest-brand`, linear, no
  acceleration) when duration is unknown.
- **Determinate** — progress bar/ring: track `--forest-surface-deep`, fill
  `--forest-brand`; show real progress, never a fake crawl.
- **Skeletons** — for content loading into a known layout, matching the final shape
  (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/cards.md" />); blocks in a muted green mix.
- Loading animation is calm; provide the reduced-motion fallback (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

## Empty states

Not a blank green box — an invitation. Show a muted icon, explain *why* it's empty
(first use? filtered to nothing?), and offer the primary action (a lime button) to
create the first item or clear the filter. Distinguish "no results for this search"
from "nothing created yet."

## Voice

Shared with <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/inputs.md" /> validation: errors **explain and direct** (what
went wrong + how to fix), don't apologize or blame, never vague ("Something went
wrong" with no recourse is a failure). Confirmations are brief and consistent
("Publish" → "Published"). Warnings state the consequence honestly.

## CSS tokens

```css
.forest-alert {
  --forest-fb-accent: var(--forest-brand-medium);            /* info default */
  --forest-fb-surface: var(--forest-surface-deep);

  background: var(--forest-fb-surface);
  border-inline-start: 3px solid var(--forest-fb-accent);
  border-radius: var(--forest-radius-md);
  color: var(--forest-body);
  padding: 12px 16px;
  /* flat — no shadow */
}
.forest-alert--success {
  --forest-fb-accent: var(--forest-success);
  --forest-fb-surface: color-mix(in oklch, var(--forest-success) 14%, var(--forest-surface-deep));
}
.forest-alert--warning {
  --forest-fb-accent: var(--forest-warning);
  --forest-fb-surface: color-mix(in oklch, var(--forest-warning) 14%, var(--forest-surface-deep));
}
.forest-alert--error {
  --forest-fb-accent: var(--forest-danger);
  --forest-fb-surface: color-mix(in oklch, var(--forest-danger) 14%, var(--forest-surface-deep));
}
.forest-progress__fill { background: var(--forest-brand); }
.forest-progress__track { background: var(--forest-surface-deep); }
```

## Anti-patterns (Forest-specific)

- Severity by color alone — fatal here, since success (lime) and the brand accent
  share a hue family; always icon + label.
- Using the lime brand for a warning or error (it reads as success/highlight).
- A drop shadow on a toast or banner — keep feedback flat.
- Auto-dismissing an error or required-action message before the user can act.
- A blank green empty state with no explanation or next step.
- Stacking toasts into an unreadable green pile.
