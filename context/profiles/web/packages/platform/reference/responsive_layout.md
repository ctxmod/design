# Responsive Layout

The web's multi-viewport reality — fluid layout, intrinsic vs extrinsic sizing, container vs media queries, fluid type, mobile-first, breakpoints as a scale, and CLS as a design failure.

The web has no canvas. A design is rendered into an unknown rectangle on a device
you did not choose, at a zoom level and font size the user may have overridden,
beside a scrollbar that may or may not take space. Responsive layout is the
discipline of designing the *family* of arrangements that holds up across that
entire range — not a fixed composition that happens to also fit a phone.

This is the web concretization of <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />'s
"responsive composition (abstract)" section. The umbrella says *reflow, don't just
shrink* and *preserve reading order*; here we name the mechanics that make that
true on the web.

## Fluid by default, fixed by exception

The web's native behavior is fluid: block elements fill their container, text
wraps, content flows. Fighting that — pinning fixed pixel widths everywhere — is
what produces layouts that break off the edge of the viewport.

- **Let content size itself** unless there is a reason not to. A `max-width` plus
  auto margins gives a constrained measure that still collapses gracefully on
  narrow screens; a fixed `width` does not.
- **Constrain the measure, not the page.** Reading content wants 45–75 characters
  per line (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_accessibility.md" />); cap it with `max-width:
  65ch` on the text column, not on the whole layout.
- **Reach for fixed sizing only for things that are genuinely fixed** — a 1px
  hairline, an icon's intrinsic box, an avatar. Everything structural should be
  expressed in relative or intrinsic terms.

## Intrinsic vs extrinsic sizing

Two ways to decide an element's size, and choosing the right one is most of
responsive layout:

- **Extrinsic** — the *container* dictates size (percentages, `fr` units in grid,
  `flex-grow`). The element takes what it's given. Use for structural regions:
  columns, panels, the main content area.
- **Intrinsic** — the *content* dictates size (`min-content`, `max-content`,
  `fit-content`, `auto`). The element is as big as it needs to be. Use for things
  whose natural size matters: a button hugging its label, a sidebar sized to its
  longest nav item.

The strongest layouts combine them: `grid-template-columns: fit-content(20rem)
1fr` gives a sidebar that's intrinsic up to a cap and a main column that's
extrinsic. Modern CSS (`minmax()`, `clamp()`, `min()`, `max()`) lets a single
declaration express "intrinsic within these bounds," which often removes the need
for a breakpoint entirely.

## Container queries vs media queries

The most important shift in web responsive design: components should usually react
to **the space they occupy**, not to the viewport.

- **Media queries** ask about the *viewport* (`@media (min-width: 48rem)`). Correct
  for page-level decisions: how many columns the page shell has, whether the global
  nav is a bar or a drawer.
- **Container queries** ask about the *element's container*
  (`@container (min-width: 24rem)`). Correct for component-level decisions: a card
  that switches from stacked to side-by-side based on whether it's in a wide main
  column or a narrow sidebar — regardless of viewport width.

Prefer container queries for reusable components. A card laid out by viewport
breaks when reused in a different-width slot; a card laid out by container is
portable. Reserve media queries for the page-level shell and for things genuinely
tied to the device (coarse pointer, reduced data). This is enforced by the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/rules/responsive_discipline.md" />.

## Fluid type and space with `clamp()`

Stepping type and spacing only at breakpoints leaves awkward dead zones (text
that's too big at 600px because it won't step down until 768px). `clamp(min, fluid,
max)` interpolates smoothly between bounds:

```css
/* between 1.5rem and 2.5rem, scaling with the viewport */
h1 { font-size: clamp(1.5rem, 1rem + 2.5vw, 2.5rem); }
```

- Always supply real `min`/`max` bounds so the value never becomes illegibly small
  or absurdly large, and so a user's zoom still works (use `rem`-based terms in the
  fluid middle, not pure `vw`, to keep zoom functional).
- Apply the same idea to section padding and gaps for layouts that breathe with the
  viewport instead of jumping. Use it as a *complement* to breakpoints, not a
  replacement: clamp handles smooth scaling, breakpoints handle structural reflow.

## Mobile-first vs desktop-first

Author **mobile-first**: the base styles describe the smallest, simplest layout,
and `min-width` queries progressively add complexity as space appears.

- Mobile-first matches the cascade's grain — you add capability, you don't subtract
  it — which produces less CSS and fewer override fights.
- It also matches priority discipline: the single-column mobile layout forces you
  to commit to the reading order the umbrella demands
  (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />), and the desktop layout elaborates on
  that order rather than inventing a different one.
- Desktop-first (`max-width` queries) is occasionally right for data-dense tools
  whose reason to exist is the wide view, but it is the exception and should be a
  conscious choice.

## Breakpoints are a scale, not a set of magic numbers

Do not chase device dimensions (there is no "the iPhone width"). Define a small,
named **scale** of breakpoints and place each break where *the content* stops
working, not where some device happens to be.

- A handful of named steps (e.g. `sm` `md` `lg` `xl`) drawn from one scale, reused
  everywhere — the same discipline the umbrella applies to spacing.
- Add a breakpoint when a layout visibly breaks (a row gets too cramped, a measure
  gets too long), and choose it by resizing until it breaks, not by copying a
  device chart.
- Fewer, well-chosen breakpoints beat many ad-hoc ones. With `clamp()` and
  intrinsic sizing doing the in-between work, most layouts need only two or three
  structural breaks.

## Layout shift (CLS) is a design failure

When content jumps after load — an image popping in, a web font reflowing text, an
ad pushing the article down — the user loses their place and may mis-tap. Cumulative
Layout Shift is graded by the browser, but it is *designed in or out*, not just
engineered:

- **Reserve space for media.** Every image and video must declare its
  aspect ratio (`aspect-ratio`, or width/height attributes) so the box exists
  before the bytes arrive.
- **Reserve space for async content.** Skeletons and placeholders for late-loading
  regions should occupy the same box the real content will (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" /> loading states).
- **Avoid font-swap reflow.** Pair the web font with a metric-compatible fallback
  so the swap doesn't change line counts (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/rendering_performance.md" />).
- **Never insert content above what the user is looking at** after the fact.

A layout that settles instantly and never jumps is part of the quality floor, the
same way visible focus and respected reduced-motion are.

## Rule Companion: Responsive Discipline — Full Rule and Rationale

*Companion to the `responsive_discipline` rule: its full rule set, worked examples and rationale.*

### The rules

- **Works across the whole range.** Every layout must be usable from small phones
  to ultrawide. No layout is sign-off-ready until it has been checked at the
  extremes, not just the design width.
- **Test at the extremes.** Verify at **320px** (small phone) and at a very wide
  viewport (ultrawide). Most responsive bugs — overflow, cramped rows, lines that
  run the full width of a 27-inch monitor — only appear at the ends.
- **Breakpoints are a named scale.** Use a small, reused set of breakpoints chosen
  where *content* breaks, not at device dimensions. Don't sprinkle one-off pixel
  queries; add a breakpoint only when a layout visibly stops working.
- **Fluid type via `clamp()`.** Headings and large type scale smoothly between a
  legible `min` and a sensible `max`, with `rem`-based terms so zoom still works —
  not fixed sizes that jump only at breakpoints.
- **No horizontal scroll.** The page must never scroll sideways at any width.
  Constrain wide content, wrap or scroll-contain overflowing elements (tables, code
  blocks) deliberately, and watch for fixed widths and unbroken strings.
- **Responsive images by default.** Every image declares its box
  (`aspect-ratio` or width/height) to prevent layout shift, and serves
  appropriately-sized sources (`srcset`/`sizes` or `<picture>`). No desktop-weight
  images shipped to phones.
- **Reflow, don't shrink.** As space narrows, multi-column layouts reorganize
  (columns stack, side-by-side becomes sequential) while preserving reading order —
  they do not merely scale down until everything is tiny.

### Why

The viewport is not yours to choose, and the failure modes cluster at the edges no
one checks. A layout that overflows at 320px or sprawls unreadably at 2560px is
broken for real users even when the design-width screenshot is flawless. Treating
the full range — and testing its extremes — as part of *done* is what separates a
responsive design from one that merely has a few breakpoints.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" />
