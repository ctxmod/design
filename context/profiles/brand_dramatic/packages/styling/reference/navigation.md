# Dramatic — Navigation

Dramatic navigation — minimal dark nav, active item lit by a violet glow underline and 900 weight, inactive 400, multi-channel active state, mobile drawer.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />
for Dramatic. Navigation is **minimal and dark** — the bar recedes into the stage
so the lit, active destination stands out. Tokens are in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/brand.md" />.

## The bar

A near-black bar (`--bd-surface` or `--bd-surface-raised`) with no heavy chrome —
a hairline `--bd-border` below it at most. Items are quiet until active.

```css
.bd-nav {
  background: var(--bd-surface);
  border-block-end: 1px solid var(--bd-border);
  font-family: var(--bd-font);
}
.bd-nav__item {
  font-weight: var(--bd-weight-body); /* 400 — inactive whisper */
  color: var(--bd-text-muted);
  padding-block: 0.75rem;
  padding-inline: 1rem;
  min-block-size: 2.75rem;
  transition: color var(--bd-dur-fast) var(--bd-ease-out);
}
```

## The active-state contract — the spotlight

The active item is the lit one. Per the slot, the active state uses **more than one
channel**: a **weight jump to 900**, a color lift to `--bd-text`, *and* a violet
glow underline (or a violet fill). Never color alone.

```css
.bd-nav__item[aria-current="page"] {
  font-weight: var(--bd-weight-display); /* 900 — active shout */
  color: var(--bd-text);
}
.bd-nav__item[aria-current="page"]::after { /* glow underline */
  content: "";
  display: block;
  block-size: 2px;
  background: var(--bd-accent);
  box-shadow: 0 0 12px var(--bd-accent);
  margin-block-start: 0.375rem;
}
```

- The active state is **announced** (`aria-current="page"` / selected tab), not
  just styled.
- Exactly one active item per group; in nested nav the active sub-item implies its
  parent section.

## The family

| Slot | Treatment |
|------|-----------|
| **Primary nav** | The dark bar above; 900 active with glow underline. |
| **Secondary nav** | Quieter; active = violet text + 900, no glow underline (keeps levels distinct). |
| **Tabs** | Selected tab gets the glow underline; switches views in place. |
| **Breadcrumbs** | 400 `--bd-text-muted`, violet current crumb. |
| **Pagination** | Current page = violet fill + 900; disabled boundaries dimmed. |
| **Menu / dropdown** | Dark `--bd-surface-raised` panel, hairline border, subtle entrance from its anchor. |

Levels are visually differentiated (primary uses the glow underline; secondary
uses weight+color only) so users sense which level they are operating at.

## States

| State | Treatment |
|-------|-----------|
| **Default** | 400, `--bd-text-muted` — a reachable, quiet destination. |
| **Hover** | Color lifts to `--bd-text`; faint underline preview. |
| **Focus** | Visible violet ring (`box-shadow: 0 0 0 3px var(--bd-border-glow)`), correct order. |
| **Active (current)** | 900 + glow underline — you are here. |
| **Pressed** | Underline tightens. |
| **Disabled** | `--bd-text-subtle`, no hover (e.g. pagination "next" on last page). |
| **Expanded/collapsed** | Menu open/closed state visible and announced. |

```css
.bd-nav__item:hover { color: var(--bd-text); }
.bd-nav__item:focus-visible { outline: none; box-shadow: 0 0 0 3px var(--bd-border-glow); }
@media (prefers-reduced-motion: reduce) { .bd-nav__item { transition: none; } }
```

## Mobile pattern

On small screens, primary nav becomes a **dark drawer** sliding from the edge it
lives on (not an overflowing bar) — fade + slide on the moderate band, glow
underline preserved for the active item, with a reduced-motion fade fallback. The
breakpoint mechanics are inherited from
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/responsive_layout.md" />.

## Responsibilities

- Always answer "where am I" via the multi-channel active state (900 + color +
  glow), announced to assistive tech.
- Reflect the real IA; keep primary nav shallow.
- Full keyboard support — items reachable/operable, menus arrow-navigate, focus
  managed on open and restored on close.
- Adequate targets (≥44px) for items and pagination controls.

## Anti-patterns

- No visible current-location indicator on the dark bar.
- Active state shown by violet color alone (must add 900 weight + underline).
- A middle-weight active item — active is 900, inactive is 400.
- Tabs used to navigate between unrelated pages.
- A desktop bar left to overflow on mobile instead of the drawer.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_accessibility.md" />
