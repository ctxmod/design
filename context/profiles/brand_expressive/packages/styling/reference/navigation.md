# Expressive — Navigation

Expressive navigation — IBM Plex Mono nav, active state as a solid pink or blue color block plus weight, playful spring transitions, multi-channel active marker, full state and mobile contract.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" /> for
Expressive. Nav is mono, and "you are here" is unmistakable: the active item is a
solid **color block** (pink or blue) backed by a weight bump and an indicator —
multi-channel, never color alone. Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/brand.md" />; semantic nav
landmarks per <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />.

## Primary nav

```css
.be-nav        { display: flex; gap: 4px; font-family: var(--be-font); }
.be-nav__item  {
  padding: 10px 16px;
  font: var(--be-weight-body) var(--be-text-body)/1 var(--be-font);
  color: var(--be-ink);
  border: 2px solid transparent;
  border-radius: var(--be-radius, 14px);
  transition: background-color var(--be-dur-fast) var(--be-ease-out),
              transform var(--be-dur-instant) var(--be-ease-spring);
}
```

## The active-state contract

Active = a **filled accent block** + **weight bump** + the live-region marker. Three
channels, so it survives color-blindness and low contrast (umbrella rule).

```css
.be-nav__item[aria-current="page"] {
  background: var(--be-pink);              /* color block */
  color: #fff;
  font-weight: var(--be-weight-strong);   /* weight channel */
  border-color: var(--be-border);
  box-shadow: 3px 3px 0 var(--be-ink);
}
.be-nav--blue .be-nav__item[aria-current="page"] { background: var(--be-blue); }
```

Exactly one active item per group; mark it with `aria-current` so assistive tech
announces it. In nested nav the active sub-item implies its parent section is active.
Use pink for primary nav and blue for secondary nav so the two levels stay visually
distinct (umbrella levels-are-distinct rule).

## States

```css
.be-nav__item:hover         { background: var(--be-pink-soft); transform: translateY(-1px); }
.be-nav--blue .be-nav__item:hover { background: var(--be-blue-soft); }
.be-nav__item:focus-visible { outline: 3px solid var(--be-blue); outline-offset: 2px; }
.be-nav__item:active        { transform: translateY(1px); }
.be-nav__item[aria-disabled="true"] { color: #9ca3af; pointer-events: none; }
```

State set: **default** (reachable), **hover** (soft accent tint + tiny lift),
**focus** (3px ring, correct order), **active/current** (the color block above),
**pressed**, **disabled** (e.g. pagination "next" on last page),
**expanded/collapsed** for menus (announced via `aria-expanded`).

## Tabs, breadcrumbs, pagination, menus

- **Tabs** — switch views in place (not navigation). Active tab is an underline bar
  in the accent plus weight bump: `border-bottom: 3px solid var(--be-pink); font-weight: var(--be-weight-strong);`.
- **Breadcrumbs** — mono, `/` separators (the monospace voice loves a slash), current
  crumb in `--be-weight-strong`.
- **Pagination** — current page as a small pink color block; disabled boundaries
  greyed; targets ≥ 44px.
- **Menu / dropdown** — opens with a spring `pop` entrance from its anchor; focus
  moves in on open and restores on close.

## Playful transitions

Menus and drawers enter with `--be-dur-pop var(--be-ease-spring)` from their spatial
origin; the active color block animates its position when the route changes (a sliding
highlight) rather than hard-cutting — continuity, not decoration. Reduced-motion drops
the slide to an instant swap.

## Mobile

Below the medium tier's breakpoint the bar becomes a deliberate pattern — a slide-in
drawer or bottom tab bar — never a desktop bar left to overflow (umbrella mobile
rule). Drawer slides from its edge with the spring ease.

## Anti-patterns

- Active state by color alone — always pair the block with weight + `aria-current`.
- More than one current item per group.
- Tabs used to navigate between unrelated pages.
- Desktop nav bar overflowing on mobile.
- Inconsistent nav placement between screens.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/buttons.md" />
