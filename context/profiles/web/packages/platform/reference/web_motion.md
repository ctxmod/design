# Web Motion

Motion on the web — CSS transitions/animations, the View Transitions API, scroll-driven animation, prefers-reduced-motion (mandatory), and the layout/paint/composite distinction.

This is the web realization of the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />
principles. The umbrella decides *whether* and *why* to animate — feedback,
continuity, wayfinding, status, attention — and sets the easing and duration
bands. This document decides *how* to express that on the web, with the platform's
real APIs and the browser's real constraints, and it makes one umbrella promise
concrete and **mandatory**: reduced motion is honored.

## The web's motion toolbox

Pick the smallest tool that does the job:

| Tool | Use for | Notes |
|------|---------|-------|
| **CSS transitions** | State changes between two values (hover, open/close, focus) | The default. Declarative, interruptible, cheap. |
| **CSS `@keyframes` animations** | Multi-step or looping motion (spinners, attention pulses) | Use `animation-play-state` and finite `iteration-count` deliberately. |
| **View Transitions API** | Continuity across a DOM/route change (a list item growing into a detail view) | The platform's answer to shared-element transitions; see below. |
| **Scroll-driven animations** | Motion tied to scroll position (progress bars, reveal-on-scroll) | Prefer CSS `animation-timeline: scroll()/view()` over JS scroll listeners. |
| **JS / Web Animations API** | Physics, gesture-following, orchestration the above can't express | Reach for it last; most UI motion is a CSS transition. |

Reserve JavaScript animation libraries for genuinely dynamic motion (spring physics,
drag-follow, FLIP that the View Transitions API can't cover). A hover state or a
dropdown opening is a CSS transition, not a library.

## Animate on the compositor, not the layout

The single most important web-motion rule, because it determines whether motion is
smooth or janky: **animate only `transform` and `opacity`.**

- `transform` (translate, scale, rotate) and `opacity` are handled by the
  compositor and can run at 60–120fps off the main thread.
- Animating `width`, `height`, `top`/`left`, `margin`, or anything that changes the
  box triggers **layout** (reflow) every frame; animating `color`,
  `background`, `box-shadow`, `border-radius` triggers **paint**. Both fight the
  main thread and drop frames.
- To move something, `translate` it. To resize a reveal, animate `transform:
  scaleY()` (and counter-scale children if needed) or use `clip-path`, not
  `height`. To fade, use `opacity`.

The layout → paint → composite hierarchy is detailed in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/rendering_performance.md" />; for motion the rule collapses
to: *stay on the composite layer.* Use `will-change` sparingly to hint a layer
just before an animation, and remove it after — it is a scalpel, not a default.

## Duration and easing on the web

Apply the umbrella's <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />
directly; the web specifics:

- Express the band as a CSS `transition-duration` (e.g. `150ms` for most UI,
  `250–400ms` for modals/drawers). Keep the values in custom properties so a brand
  can retune them in one place (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />).
- Use `cubic-bezier()` for the named curves rather than the keyword `ease` (whose
  symmetric curve feels sluggish on entry). Ease-out for entrances/responses,
  ease-in for exits, ease-in-out for in-view repositioning — encode each as a named
  custom property.
- Hover and focus transitions should be in the *instant* band (≤100ms); a slow
  hover feels broken. Tap/active feedback should be immediate.
- Exits may be a touch faster than entrances — the user has already moved on.

## View Transitions for continuity

When the DOM changes between two states — a route navigation, a filter that
reorders a grid, a thumbnail opening into a lightbox — the View Transitions API
animates between the old and new snapshots and can morph shared elements:

- It is the web-native way to deliver the umbrella's **continuity** purpose
  (preserving object identity across a change) without hand-rolled FLIP.
- Tag the persistent element with `view-transition-name` so the browser animates it
  from its old box to its new one instead of cross-fading.
- It degrades cleanly: where unsupported, the change simply happens without the
  transition. Author the experience so the transition is enhancement, never a
  prerequisite for the navigation working.

## Scroll-driven motion, used with restraint

Scroll-linked reveals and progress indicators belong to the umbrella's *attention*
and *status* purposes. On the web:

- Prefer CSS `animation-timeline: view()` / `scroll()` to JavaScript scroll
  handlers — it runs off the main thread and stays smooth.
- Scroll-jacking (overriding the natural scroll to drive a cinematic sequence)
  fights the user's primary navigation gesture and disproportionately harms
  motion-sensitive and assistive-tech users. Treat it as almost always wrong.
- A subtle fade/translate-in as content enters the viewport is fine; firing it on
  *every* element turns the page into noise (the umbrella's "don't scatter
  micro-interactions").

## `prefers-reduced-motion` is mandatory

The umbrella states that every animation must have a calm fallback. On the web this
is not optional and not aspirational — it is the medium's hard contract:

```css
@media (prefers-reduced-motion: reduce) {
  *, ::before, ::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

- The above is a safety net. Better is to author the reduced path *intentionally*:
  replace a slide with an instant state change or a simple opacity fade, keep the
  *meaning* (the thing still appears/changes), drop only the travel.
- Reduced motion must never remove function — a View Transition that's suppressed
  must still navigate; a reveal that's suppressed must still show its content.
- Pair this with the umbrella's "don't encode meaning in motion alone" (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_accessibility.md" />): anything a user learns from an
  animation must also be readable when the animation is gone.
- Respect `prefers-reduced-data` and slow connections the same way — heavy ambient
  motion is a cost, not just a preference.

The umbrella's test still governs: *remove the animation.* If the interface is now
broken or confusing, the motion was load-bearing — keep it (and give it a reduced
fallback). If it's merely less flashy, leave it removed.
