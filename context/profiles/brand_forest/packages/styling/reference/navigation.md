# Forest — Navigation

Forest concrete navigation styling — clean deep-surface nav with lime active state via multi-channel marker, tabs with lime underline, breadcrumbs, pagination; states and mobile pattern.

Concrete Forest styling for the **navigation** slot. Fills the umbrella
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" /> — the active-state contract,
hierarchy, the family (primary nav, tabs, breadcrumbs, pagination, menus), the
state set — with Forest values. Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />.

Forest navigation is **clean, focused, and flat.** It sits on
`--forest-surface-deep`, uses `--forest-body` for resting items and reserves the
lime accent for the *current location*. The active marker is always **multi-channel**
(color + weight + indicator), never lime alone (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> — active state must not rely on color alone, and lime text on
green needs care).

## Surfaces & colors

| Part | Color |
|------|-------|
| Nav bar / sidebar fill | `--forest-surface-deep` (`#1F3400`) |
| Resting item text | `--forest-body` (`#C9D6B0`) |
| Hover item text | `--forest-heading` (`#F4FAE8`) |
| Active item text | `--forest-heading`, weight 600 |
| Active indicator | `--forest-brand` (`#A1DA02`) bar / underline |
| Divider / hairline | `--forest-border` |

## Primary nav

- Top bar or sidebar on `--forest-surface-deep`, consistent placement on every
  screen, shallow (few top-level items, noun labels).
- **Active item** = `--forest-heading` text + weight 600 + a 2–3px `--forest-brand`
  indicator (left bar in a sidebar, bottom bar in a top nav) + `aria-current="page"`.
  Three channels (color, weight, bar) satisfy the not-by-color-alone rule.
- Hover lifts text to `--forest-heading` with a faint lime-tint background
  (`color-mix(in oklch, var(--forest-brand) 8%, transparent)`).

## Tabs

- Switch views in the *same* context (not navigation). Resting tab `--forest-body`;
  **selected tab** `--forest-heading` + 2px `--forest-brand` underline + a faint
  lime-tint background; the underline animates in (~200ms ease-in-out).
- Exactly one selected tab; selection announced to assistive tech.

## Breadcrumbs

- `--forest-body` segments, `--forest-border` separators (`/` or chevron). The
  current (last) segment is `--forest-heading`, non-link. Only on genuinely nested
  hierarchies.

## Pagination

- Page numbers as pill controls (`--forest-radius-pill`); **current page** =
  `--forest-brand` fill with `--forest-on-brand` text; others are ghost. Disabled
  prev/next (boundaries) at reduced contrast, not focusable as actions.

## Menu / dropdown

- Panel on `--forest-surface-raised`, `--forest-radius-md`, hairline border, flat
  (no shadow). Items `--forest-body`, hover bg lime-tint, `--forest-heading` text.
  Open/close state visible and announced; focus managed on open, restored on close.

## States

| State | Treatment |
|-------|-----------|
| **Default** | `--forest-body` text |
| **Hover** | `--forest-heading` text + lime-tint bg |
| **Focus** | 2px `--forest-brand-medium` ring, visible, correct order |
| **Active (current)** | heading text + weight 600 + `--forest-brand` indicator + `aria-current` |
| **Pressed** | bg one step darker |
| **Disabled** | reduced contrast, not focusable as an action |
| **Expanded/collapsed** | chevron rotates (~130ms); state announced |

## Mobile pattern

A deliberate small-screen pattern exists — never a desktop bar left to overflow.
Forest favors a **drawer** sliding in from its edge (~280ms ease-out, see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />) on `--forest-surface-deep`, or bottom tabs for app-like
products. The breakpoint behavior is inherited from the medium tier.

## CSS tokens

```css
.forest-nav { background: var(--forest-surface-deep); }
.forest-nav__item {
  color: var(--forest-body);
  border-radius: var(--forest-radius-sm);
  padding-block: 8px;
  padding-inline: 12px;
  transition: color var(--forest-dur-fast) var(--forest-ease);
}
.forest-nav__item:hover {
  color: var(--forest-heading);
  background: color-mix(in oklch, var(--forest-brand) 8%, transparent);
}
.forest-nav__item:focus-visible {
  outline: 2px solid var(--forest-brand-medium);
  outline-offset: 2px;
}
.forest-nav__item[aria-current="page"] {
  color: var(--forest-heading);
  font-weight: 600;
  box-shadow: inset 3px 0 0 0 var(--forest-brand); /* indicator bar, not elevation */
}
```

## Anti-patterns (Forest-specific)

- Active state shown by lime **color alone** — pair it with weight + the indicator
  bar.
- Small lime text marking the current item on green — fails contrast; use the bar +
  heading-colored text.
- Tabs used to move between unrelated pages, or nav used to switch in-place views.
- A desktop nav bar left to wrap/overflow on mobile instead of a drawer.
- A dropdown panel with a drop shadow — keep it flat with a hairline.
