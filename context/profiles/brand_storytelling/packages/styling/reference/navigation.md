# Storytelling — Navigation

Concrete Storytelling styling for the navigation slots — unobtrusive story-pace nav, subtle active state, and a chapter progress indicator answering "where am I in the story.".

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" /> for
Storytelling. Navigation is **unobtrusive** — it frames the story without
competing with it. The active state is subtle but unambiguous, and a long-form
page may carry a **chapter progress indicator** that reads as "where am I in the
story." Inter throughout; the display face never appears in nav.

## Primary nav

A quiet bar with generous margins (the page-as-book frame, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />). Labels are nouns the user recognizes.

```css
.nav {
  display: flex;
  gap: 2rem;                       /* airy, paced spacing */
  padding-block: 1.25rem;
  font-family: var(--bs-font-body);
  font-size: var(--bs-text-body);
  border-block-end: 1px solid var(--color-border); /* hairline, restrained */
}

.nav__item { color: var(--color-muted); text-decoration: none; transition: color var(--bs-dur-page) var(--bs-ease-page); }
.nav__item:hover { color: var(--color-text); }
```

## The active-state contract

Always show where the user is, via **more than one channel** — never color alone
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />).

```css
.nav__item[aria-current="page"] {
  color: var(--color-text);        /* channel 1: ink, not muted */
  font-weight: 600;                /* channel 2: weight */
  position: relative;
}
.nav__item[aria-current="page"]::after {  /* channel 3: indicator bar */
  content: "";
  position: absolute; inset-inline: 0; inset-block-end: -1.3rem;
  block-size: 2px; background: var(--color-accent);
}
```

Exactly one active item per group, announced via `aria-current` (not merely
styled). In nested nav the active sub-item implies its parent section is active.

## Chapter progress indicator

The Storytelling signature for long-form pages: a slim marker of narrative
position — which act/chapter the reader is in. It reads as wayfinding through the
story, not just a scroll bar.

```css
.chapter-progress { display: flex; gap: 0.5rem; }
.chapter-progress__step {
  flex: 1; block-size: 3px; border-radius: 2px;
  background: var(--color-border);
  transition: background-color var(--bs-dur-page) var(--bs-ease-page);
}
.chapter-progress__step[data-state="done"]    { background: var(--color-muted); }
.chapter-progress__step[data-state="current"] { background: var(--color-accent); } /* the act you're reading */
```

Pair each step with an accessible label ("Chapter 2 of 4 — current") so the
position is announced, not just shown.

## States

`Default / hover / focus / active(current) / pressed / disabled`, plus
expanded/collapsed for menus. The focus ring is always visible:

```css
.nav__item:focus-visible { outline: 3px solid color-mix(in oklch, var(--color-accent) 60%, transparent); outline-offset: 3px; }
```

On small screens, primary nav adopts a deliberate **drawer/disclosure** pattern
(the breakpoint mechanics are inherited from `web`) — never a desktop bar
left to overflow or wrap.

## Anti-patterns

- No visible "current location" / active-chapter indicator.
- Active state shown by color alone.
- A loud, chrome-heavy nav that competes with the story.
- Tabs used to navigate between unrelated pages.
- A progress indicator on a flat page that has no narrative sequence to show.
- A desktop nav bar overflowing on mobile.
</content>

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/brand.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
