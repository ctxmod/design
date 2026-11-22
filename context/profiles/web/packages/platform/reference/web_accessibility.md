# Web Accessibility

Web accessibility concretized — semantic HTML as the foundation, WCAG contrast, ARIA (and when not to), focus management, keyboard nav, target size, and color-scheme/forced-colors.

This is the web realization of <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />.
The umbrella's frame holds: accessibility is a measure of design quality, not a
compliance pass. This document gives that frame the web's concrete mechanics — the
HTML, ARIA, WCAG numbers, and focus model the design must be authored to express
correctly.

## Semantic HTML is the foundation

The single highest-leverage accessibility decision on the web is using the right
element. Native elements come with roles, states, keyboard behavior, and focus for
free; reconstructing them from `<div>`s means rebuilding all of that by hand, and
the rebuild is almost always worse.

- A `<button>` is focusable, activates on Enter/Space, and announces as a button.
  A `<div onclick>` does none of that until you add `tabindex`, key handlers, and a
  role — at which point you have reimplemented `<button>` badly.
- Use `<a href>` for navigation, `<button>` for actions, `<label>`-associated
  controls for inputs, `<nav>/<main>/<header>/<footer>` for landmarks, real
  headings (`<h1>`–`<h6>`) for hierarchy, `<ul>/<ol>` for lists, `<table>` for
  tabular data.
- The umbrella's "structure as a design lever" becomes literal here: the heading
  outline you *design* must be the heading elements the page *ships*. One `<h1>`,
  nested `<h2>/<h3>` in order, no levels skipped for visual size — restyle with CSS,
  don't renumber the semantics.

## ARIA: the first rule is don't

ARIA can label, describe, and announce state for things HTML can't express on its
own. But broken ARIA is worse than none — it lies to assistive tech.

- **No ARIA is better than bad ARIA.** Reach for a native element before an ARIA
  role. Don't put `role="button"` on a `<div>` when `<button>` exists.
- Use ARIA where there's a genuine gap: `aria-label`/`aria-labelledby` for controls
  whose visible text is insufficient (an icon-only button), `aria-describedby` to
  tie a field to its helper/error text, `aria-live` for async status messages
  (toasts, validation — see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />),
  `aria-expanded`/`aria-current`/`aria-selected` for states native HTML lacks.
- These map directly onto the umbrella's "states must be perceivable": every
  designed state (expanded, selected, disabled, busy) needs both a visible
  treatment and the matching announced state.
- Never use ARIA to *remove* semantics that the design needs (`aria-hidden` on
  focusable content traps keyboard users).

## Contrast (WCAG)

Apply the umbrella's contrast targets with the web's exact thresholds, verified
against the *rendered* background (including overlays, gradients, and images):

- Body text **4.5:1** (AA); large text (≥24px, or ≥18.66px bold) **3:1**.
- Non-text UI — icons, control borders, focus rings, chart strokes — **3:1**.
- Test the real composite, not the token in isolation: white text on a brand color
  over a photo can fail even when the swatch passes.
- Don't rely on placeholder text to carry meaning; placeholders routinely fail
  contrast and vanish on input. Use real, persistent labels
  (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />).

`color-mix()` and OKLCH (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />) make it
easy to generate tints that *look* fine but fail — verify generated colors, don't
assume.

## Focus: visible and managed

A keyboard or switch user navigates entirely by focus; the web makes this concrete:

- **Visible focus, always.** Use `:focus-visible` to show a clear indicator for
  keyboard users (and suppress it for mouse clicks where appropriate), with **≥3:1**
  contrast against adjacent colors. Never `outline: none` without a stronger
  replacement.
- **Logical order.** DOM order is tab order. Keep the DOM in reading order so the
  tab sequence matches the visual hierarchy the umbrella designed; avoid positive
  `tabindex`.
- **Manage focus on dynamic change.** When a modal/drawer opens, move focus into it
  and trap it there; on close, return focus to the trigger. When a route changes in
  a single-page app, move focus to the new view's heading. Orphaned focus (left on a
  now-hidden element) silently breaks keyboard nav.
- **Skip links** to bypass repeated navigation, and a focus order that lets a
  keyboard user reach everything a mouse user can.

## Keyboard operability

Everything operable by pointer must be operable by keyboard:

- Native controls bring their key behavior for free — another reason to use them.
- Custom widgets must implement the expected keys (Esc closes overlays and menus;
  arrow keys move within composite widgets like menus, tabs, and listboxes; Enter
  /Space activate). Follow the established interaction patterns rather than
  inventing keys.
- No keyboard traps: focus must always be able to move on.

## Target size

The umbrella's 44×44px comfortable target becomes a CSS obligation: an icon button
with a 16px glyph needs padding (or a hit-area pseudo-element) to reach the target
box, even when the visual remains small. Maintain spacing between adjacent targets
so users don't mis-tap. WCAG's 24px is the floor; 44px is the bar.

## Respect system preferences

The browser exposes the user's environment; honor it:

- **`prefers-color-scheme`** — support both light and dark; design tokens for both
  rather than inverting at the end (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />).
- **`forced-colors`** (Windows High Contrast) — don't fight it; ensure borders and
  focus survive when the user's palette replaces yours, and use `forced-colors`
  /`system colors` where you must intervene.
- **`prefers-reduced-motion`** — covered in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />; meaning
  must never live in motion alone.
- **`prefers-reduced-data`** — treat heavy media as a cost.

## The web quality floor

The umbrella's "build to a quality floor, quietly" is, on the web, a concrete and
testable checklist that is part of *done*: responsive to small screens; visible
`:focus-visible` on every interactive element; reduced motion respected; contrast
verified at AA against the real background; semantic landmarks and heading outline;
real labels on every control; every designed state both visible and announced. A
beautiful page that misses this floor is not finished.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/rules/responsive_discipline.md" />
