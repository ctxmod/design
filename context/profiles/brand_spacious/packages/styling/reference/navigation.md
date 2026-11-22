# Spacious — Navigation

Spacious navigation styling — spaced-out items, subtle blue-violet active state via multiple channels, generous padding, calm interactions.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" /> for
Spacious. The slot owns the active-state contract, the hierarchy rules, and the
state set; this file supplies the look. The Spacious signature on navigation is
**air between items** — generously spaced, calm, with an unmistakable but subtle
blue-violet "you are here."

## Foundations

Nav items draw from the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/brand.md" />: generous padding from the 8pt
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />, the accent reserved for the active marker,
and quiet motion.

```css
.nav {
  display: flex;
  gap: var(--space-5);                 /* 32px between items — spaced out */
  font-family: var(--font-body);
}
.nav__item {
  padding-block: var(--space-3);       /* 16px */
  padding-inline: var(--space-3);
  min-block-size: 44px;
  color: var(--color-text-muted);
  border-radius: var(--radius);
  transition: color var(--dur-fast) var(--ease-standard),
              background-color var(--dur-fast) var(--ease-standard);
}
```

## The active-state contract

Per the umbrella, the current location is marked via **more than one channel** —
never color alone. Spacious combines an accent color, a weight bump, and a thin
indicator bar, all quietly.

```css
.nav__item[aria-current="page"] {
  color: var(--color-accent);          /* channel 1: color */
  font-weight: 600;                    /* channel 2: weight */
  box-shadow: inset 0 -2px 0 var(--color-accent); /* channel 3: indicator bar */
}
```

The active state is announced via `aria-current`; exactly one active item per nav
group. In nested nav, the active sub-item implies its parent section is active.

## States

| State | Treatment |
|-------|-----------|
| **Default** | Muted text, no fill — recedes into the white ground |
| **Hover** | Text darkens to `--color-text`, faint sunken-neutral fill |
| **Focus** | Visible accent ring, correct order |
| **Active (current)** | Accent color + 600 weight + indicator bar (above) |
| **Pressed** | Brief deepen of the hover fill |
| **Disabled** | Muted, `not-allowed` (e.g. pagination boundary) |
| **Expanded/collapsed** | Disclosure state visible and announced |

```css
.nav__item:hover         { color: var(--color-text); background: var(--color-surface-sunken); }
.nav__item:focus-visible { outline: none; box-shadow: 0 0 0 3px rgba(59,130,246,.4); }

@media (prefers-reduced-motion: reduce) { .nav__item { transition-duration: 1ms; } }
```

## Patterns

- **Primary nav** stays shallow and consistently placed; its generous gaps make the
  small set of destinations feel deliberate, not crowded (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />).
- **Tabs** switch views in place and add a selected panel; the same accent
  indicator bar marks the selected tab.
- **Sidebar nav** stacks items with `--space-2` (8px) vertical gaps and `--space-4`
  (24px) inset padding — roomy rows, not a dense list.
- **Mobile** adopts a deliberate pattern (drawer / disclosure), never an overflowing
  desktop bar. The breakpoint behavior is the medium tier's concern; the slot
  requires that a small-screen pattern exists.

See <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" /> for the CSS
carriers (`aria-current`, `:focus-visible`, custom properties).

## Anti-patterns (brand-specific)

- Packing nav items with tight gaps — Spacious nav is airy; let it breathe.
- A loud, filled "pill" on the active item — Spacious marks active subtly with
  color + weight + a thin bar.
- Active state by color alone — fails the multi-channel contract.
- A desktop bar left to overflow on mobile.
