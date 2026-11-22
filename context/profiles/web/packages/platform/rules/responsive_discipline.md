---
paths:
  - "*.css"
  - "*/*.css"
  - "*/*/*.css"
  - "*/*/*/*.css"
  - "*/*/*/*/*.css"
  - "*.scss"
  - "*/*.scss"
  - "*/*/*.scss"
  - "*/*/*/*.scss"
  - "*/*/*/*/*.scss"
  - "*.tsx"
  - "*/*.tsx"
  - "*/*/*.tsx"
  - "*/*/*/*.tsx"
  - "*/*/*/*/*.tsx"
  - "*.jsx"
  - "*/*.jsx"
  - "*/*/*.jsx"
  - "*/*/*/*.jsx"
  - "*/*/*/*/*.jsx"
  - "*.vue"
  - "*/*.vue"
  - "*/*/*.vue"
  - "*/*/*/*.vue"
  - "*/*/*/*/*.vue"
  - "*.svelte"
  - "*/*.svelte"
  - "*/*/*.svelte"
  - "*/*/*/*.svelte"
  - "*/*/*/*/*.svelte"
  - "*.html"
  - "*/*.html"
  - "*/*/*.html"
  - "*/*/*/*.html"
  - "*/*/*/*/*.html"
---

# Responsive Discipline

A layout is not done when it looks right at the width you happened to design it. It is done when it holds up across the viewport range it will actually meet. These are the non-negotiables behind <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/responsive_layout.md" />.

- **Works across the whole range.** Every layout must be usable from small phones to ultrawide — no layout is sign-off-ready until it has been checked at the extremes, not just the design width.
- **Test at the extremes.** Verify at **320px** (small phone) and at a very wide viewport (ultrawide) — most responsive bugs (overflow, cramped rows, lines that run the full width of a 27-inch monitor) only appear at the ends.
- **Breakpoints are a named scale.** Use a small, reused set of breakpoints chosen where *content* breaks, not at device dimensions — don't sprinkle one-off pixel queries; add a breakpoint only when a layout visibly stops working.
- **Fluid type via `clamp()`.** Headings and large type scale smoothly between a legible `min` and a sensible `max`, with `rem`-based terms so zoom still works — not fixed sizes that jump only at breakpoints.
- **No horizontal scroll.** The page must never scroll sideways at any width — constrain wide content, wrap or scroll-contain overflowing elements (tables, code blocks) deliberately, and watch for fixed widths and unbroken strings.
- **Responsive images by default.** Every image declares its box (`aspect-ratio` or width/height) to prevent layout shift, and serves appropriately-sized sources (`srcset`/`sizes` or `<picture>`) — no desktop-weight images shipped to phones.
- **Reflow, don't shrink.** As space narrows, multi-column layouts reorganize (columns stack, side-by-side becomes sequential) while preserving reading order — they do not merely scale down until everything is tiny.

- fluid sizing, container vs media queries, the breakpoint scale, and layout shift, plus the full rule text and its rationale — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/responsive_layout.md" />
