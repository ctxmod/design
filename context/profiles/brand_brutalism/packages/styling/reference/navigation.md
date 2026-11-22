# Brutalism — Navigation

Brutalism navigation — exposed list nav with thick dividers, active = filled terracotta block or border swap, heavy uppercase labels, thick underlines for tabs.

Concrete styling for the umbrella's
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />, in the Brutalism brand.
Navigation is an **exposed list** — items are heavy uppercase labels separated by
real, visible dividers, and the current location is marked by a **filled block or
a bold border swap**, never by color alone. Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/brand.md" />.

## Primary / secondary nav

A bordered bar or rail; items are blocks divided by thick rules. The structure of
the nav is itself on display.

```css
.bb-nav {
  display: flex;
  border: var(--bb-border-w) solid var(--bb-border);
  border-radius: 0;
  background: var(--bb-surface);
}
.bb-nav__item {
  font-family: var(--bb-font);
  font-weight: var(--bb-w-heavy);
  text-transform: uppercase;
  letter-spacing: var(--bb-track-wide);
  color: var(--bb-text);
  padding: 0.75rem 1.25rem;
  min-block-size: 44px;
  border-inline-end: var(--bb-border-w) solid var(--bb-border);  /* exposed divider */
}
.bb-nav__item:last-child { border-inline-end: none; }
```

## The active-state contract

The current item is marked through **more than one channel** — a terracotta block
fill *and* a weight/border change — so it survives color-blindness (umbrella
contract). Exactly one active item per group, and it is announced to assistive
tech with `aria-current`.

```css
.bb-nav__item:hover            { background: var(--bb-concrete); }   /* flat, no glow */
.bb-nav__item:focus-visible    { outline: none; border: var(--bb-border-w-bold) solid var(--bb-terracotta); }
.bb-nav__item[aria-current]    { background: var(--bb-terracotta); color: var(--bb-text); }
```

## Tabs

Tabs switch views in place. The selected tab carries a **thick terracotta
underline** (a 4px block bar), not a soft accent line.

```css
.bb-tab {
  font-weight: var(--bb-w-heavy);
  text-transform: uppercase;
  padding: 0.6rem 1rem;
  border-block-end: var(--bb-border-w-bold) solid transparent;
}
.bb-tab[aria-selected="true"] { border-block-end-color: var(--bb-terracotta);
                                color: var(--bb-text); }
```

## Breadcrumbs, pagination, menus

- **Breadcrumbs** — heavy uppercase crumbs joined by a hard `/` glyph; the current
  crumb is non-link and carries `aria-current="page"`.
- **Pagination** — square bordered number blocks; the current page is a filled
  terracotta block, boundary "prev/next" disabled with visible-but-inert borders.
- **Menu / dropdown** — a bordered block panel with thick dividers between items;
  open/closed is a hard cut (no slide-fade), announced via `aria-expanded`.

```css
.bb-page__num { border: var(--bb-border-w) solid var(--bb-border); border-radius: 0;
                min-inline-size: 44px; min-block-size: 44px; display: grid; place-items: center; }
.bb-page__num[aria-current="page"] { background: var(--bb-terracotta); }
```

## States

| State | Brutalist expression |
|-------|----------------------|
| **Default** | Bordered/divided item, heavy label. |
| **Hover** | Flat concrete fill — no animation. |
| **Focus** | Bold terracotta border, no ring. |
| **Active (current)** | Filled terracotta block + `aria-current`. |
| **Pressed** | Brief darken (hard). |
| **Disabled** | Concrete fill, border visible, inert (e.g. pagination boundary). |
| **Expanded/collapsed** | Hard show/hide; state announced. |

## Responsibilities

- Always answer **"where am I"** via the dual-channel active state.
- Reflect the real IA; keep primary nav shallow.
- **Full keyboard support** — items reachable, menus open/arrow-navigate, focus
  managed on open and restored on close.
- A deliberate **mobile pattern** (bordered drawer or disclosure), never a desktop
  bar left to overflow — `web` supplies the breakpoint behavior.

## Anti-patterns

- Active state by color alone, or no current-location marker.
- Tabs used to navigate between unrelated pages.
- Soft sliding/fading menu reveals — Brutalism cuts.
- Rounded pagination chips or a borderless nav bar.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
