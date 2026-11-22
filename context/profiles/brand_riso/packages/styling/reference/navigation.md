# Riso — Navigation

Riso navigation styling — blue ink wayfinding on paper, pink active state with a pink indicator bar, blue underlines/borders, full state set across nav/tabs/breadcrumbs/pagination/menus.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" /> for Riso. Wayfinding
is blue ink on the paper sheet; the **active "you are here" marker is pink** — the
one place navigation borrows the interaction color, because being the current
location *is* a kind of selection. Space Grotesk labels, blue dividers and
underlines for structure.

## The active-state contract

The most important navigation job: **always show where the user is**, via *more
than one channel* (never color alone — see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />).

- Active item: text → `--ink-pink`, weight bumps 500 → 700, **plus** a 3px pink
  indicator bar. Two channels beyond color satisfy accessibility.
- Exactly one active item per group; the active state is announced to assistive
  tech (`aria-current`), not merely styled.
- In nested nav the active sub-item implies its active parent section.

```css
.nav-item { font-family: var(--font-sans); font-weight: 500;
  color: var(--ink-blue); padding-block: 10px; padding-inline: 14px;
  min-block-size: 44px;
  transition: color var(--dur-fast) var(--ease-out); }

.nav-item[aria-current] { color: var(--ink-pink); font-weight: 700;
  box-shadow: inset 0 -3px 0 var(--ink-pink); }   /* pink indicator bar */
```

## States

| State | Treatment |
|-------|-----------|
| **Default** | `--ink-blue` label on paper |
| **Hover** | label → darker blue, optional inset blue underline `inset 0 -2px 0 --ink-blue` |
| **Focus** | pink `:focus-visible` ring, correct order |
| **Active (current)** | pink label + weight 700 + pink indicator bar; `aria-current` |
| **Pressed** | brief registration shift on the item |
| **Disabled** | muted blue (e.g. pagination "next" on last page), not focusable |
| **Expanded/collapsed** | menu/disclosure open-state visible + announced (chevron rotate) |

```css
.nav-item:hover { box-shadow: inset 0 -2px 0 var(--ink-blue); }
.nav-item:focus-visible { outline: 3px solid var(--ink-pink); outline-offset: 2px; }
```

## Per-slot notes

- **Primary nav** — blue items in a consistent position on every screen (a fixed
  reference point); shallow depth. Sits on paper with a blue bottom divider, never
  a different background band.
- **Secondary nav** — visually lighter (smaller, less weight) so the level is
  distinct from primary.
- **Tabs** — switch views in place; the **selected tab** carries the pink active
  treatment + indicator bar; the inactive tabs are flat blue.
- **Breadcrumbs** — blue labels with `/` or `›` dividers in muted blue; the last
  crumb (current page) is pink and non-link.
- **Pagination** — blue page numbers; **current page** pink with the indicator;
  disabled boundary controls muted blue.
- **Menu / dropdown** — paper panel with a 2px blue outline and `--print-shadow-sm`;
  items blue, hovered item `--paper-deep`, focus pink ring; chevron rotates on
  expand (`--dur-fast`).

## Responsibilities & anti-patterns

- Always answer "where am I" via the pink-plus-bar active contract; reflect the
  real IA; full keyboard support (reach, operate, arrow-navigate menus, manage and
  restore focus).
- A deliberate **mobile pattern** (drawer / bottom tabs / disclosure) on small
  screens — never a desktop bar left to overflow (breakpoint behavior is inherited
  from the `web` profile; the slot's contract is that a small-screen pattern exists).
- Adequate targets (≥44px).
- Don't mark active by color alone; don't use tabs to navigate between unrelated
  pages or nav to switch in-place views; don't place primary nav inconsistently
  between screens; don't bury primary content in deep menus.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/brand.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/feedback.md" />
