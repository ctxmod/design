# Rendering Performance

Visual decisions have performance consequences — the layout/paint/composite pipeline, avoiding layout thrash, image and font strategy, compositor-only animation, content-visibility, and keeping the main thread free.

Performance is usually framed as an engineering concern, but on the web most of it
is decided at design time. The shape of a layout, the weight of an image, the
choice of a web font, the property an animation touches — each is a *visual*
decision with a *rendering* cost. This document frames performance as a design
responsibility: a design that is slow or janky has failed, however good it looks in
a static mock.

## The rendering pipeline (and why it ranks costs)

The browser turns CSS changes into pixels through a pipeline. Where in the pipeline
a change lands determines how expensive it is:

```
style → LAYOUT (reflow) → PAINT → COMPOSITE
            ↑ most costly              ↑ cheapest
```

- **Layout / reflow** — recomputing geometry. Triggered by changing size, position,
  or anything that moves boxes (`width`, `height`, `top`, `margin`, font size,
  adding/removing nodes). The most expensive step; can cascade across the subtree.
- **Paint** — filling pixels for a layer. Triggered by `color`, `background`,
  `box-shadow`, `border-radius`, `outline`. Cheaper than layout, still main-thread.
- **Composite** — assembling already-painted layers. Triggered by `transform` and
  `opacity`. Runs off the main thread; nearly free.

The design takeaway: anything that animates or updates frequently should live as
low in this pipeline as possible. This is the same rule <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />
states for animation (`transform`/`opacity` only); here it's the general principle
behind it.

## Avoid layout thrash

Layout thrash is forcing the browser to recompute geometry repeatedly within a
frame — typically by interleaving reads of layout properties
(`offsetWidth`, `getBoundingClientRect`) with writes. The design-side levers:

- **Don't animate layout-triggering properties.** Animate `transform`, not
  `width`/`left` (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />).
- **Prefer transforms for movement and reveals**; counter-scale or use `clip-path`
  for size reveals instead of animating `height`.
- **Contain expensive subtrees.** `contain: layout` / `contain: content` tells the
  browser a subtree's layout can't affect the outside, so changes inside don't
  reflow the whole page. Design self-contained regions (cards, panels) so they're
  containable.

## Image strategy

Images are the heaviest part of most pages and a top source of layout shift; the
design decisions:

- **Right format.** AVIF/WebP for photos, SVG for icons and flat illustration (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />), and avoid shipping a 4000px JPEG
  into a 400px slot.
- **Right size, responsively.** Provide `srcset`/`sizes` (or `<picture>`) so each
  viewport downloads an appropriately-sized asset; serving desktop-resolution
  images to phones wastes bandwidth and battery.
- **Reserve the box.** Always set `width`/`height` attributes or `aspect-ratio` so
  the layout doesn't shift when the image arrives — this is the CLS rule from
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/responsive_layout.md" />.
- **Lazy-load below the fold** (`loading="lazy"`) and prioritize the hero
  (`fetchpriority="high"`); don't lazy-load the LCP image.

## Font strategy

Type carries the design's personality (see the umbrella's typography work and the
premium-UI font pairings), but web fonts have a real cost in bytes and in flashes:

- **FOIT vs FOUT.** A blocking font causes a Flash Of Invisible Text (blank until
  the font loads); a swapped font causes a Flash Of Unstyled Text (fallback, then
  reflow). FOUT is almost always preferable — text is readable immediately.
- **`font-display: swap`** (or `optional` for non-critical faces) to control this
  deliberately rather than leaving it to defaults.
- **Metric-compatible fallbacks.** Pair each web font with a system fallback of
  similar metrics, tuned with `size-adjust`/`ascent-override`, so the swap doesn't
  reflow line counts (the font side of the CLS rule).
- **Subset and limit weights.** Ship only the weights and glyph ranges the design
  uses; `preload` the critical face. Two well-chosen families beat five, in design
  *and* in performance.

## Compositor-only animation

Restating the pipeline rule as a design constraint on motion: an animation that
moves boxes or repaints every frame will drop frames on mid-range hardware no matter
how elegant it looks on a fast laptop. Author motion on `transform`/`opacity`, hint
layers with `will-change` only for the duration of the animation, and treat smooth
60fps as part of the design, not a later optimization. Details in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />.

## Render less: `content-visibility`

Long pages pay to lay out and paint content the user can't see. `content-visibility:
auto` (with `contain-intrinsic-size` to reserve space) lets the browser skip
rendering off-screen sections until they're near the viewport — a large,
design-friendly win for long articles, feeds, and dashboards. Design in
self-contained sections so this can be applied without breaking layout.

## Keep the main thread free

Everything the user feels as responsiveness — scrolling, tapping, typing — runs on
the main thread. Design choices that crowd it (heavy synchronous work on scroll,
oversized DOM, animating layout) make the whole UI feel sticky:

- Prefer CSS and compositor-driven effects over JavaScript-driven ones (CSS
  scroll-driven animations over scroll listeners; CSS transitions over JS tweening).
- Keep the DOM lean — thousands of nodes cost layout and memory; virtualize long
  lists.
- The fastest interaction is the one with nothing blocking it. A design that stays
  off the main thread feels instant; that feeling is itself a design quality, on par
  with hierarchy and contrast.
