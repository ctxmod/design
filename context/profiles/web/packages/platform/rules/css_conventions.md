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

# CSS Conventions

Web CSS hygiene that keeps a design portable, themeable, and free of the specificity wars that make stylesheets rot. These are the concrete habits behind <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />.

- **Tokens are custom properties.** Every color, space, radius, font, shadow, and duration is a `--custom-property`, referenced via `var()` — never a hard-coded literal scattered through rules; a brand retunes the system by changing variables, not by hunting for hex values.
- **Order the cascade with `@layer`.** Declare an explicit layer order (`@layer reset, base, tokens, components, utilities`) so later layers win by position, not specificity — keep almost all CSS inside a layer.
- **Prefer logical properties.** Use `padding-inline`, `margin-block`, `inset`, `border-inline` over physical `left`/`right`/`top`/`bottom` for anything directional, so RTL and vertical writing modes work without mirrored overrides.
- **Mobile-first media queries.** Base styles describe the smallest layout; `min-width` queries add complexity upward — avoid `max-width`-first authoring except for deliberately desktop-centric tools.
- **Container queries for components.** A reusable component should react to its *container* (`@container`), not the viewport — reserve media queries for the page-level shell and device-level concerns (pointer type, color scheme, reduced motion).
- **No `!important`.** If a rule needs `!important` to win, the cascade is mis-layered — fix the `@layer` order or selector instead; the only tolerated use is the `prefers-reduced-motion` safety-net reset.
- **Unit discipline.** `rem` for type and spacing (honors user zoom), `%`/`fr`/`ch` for fluid layout and measure, `clamp()` for fluid scaling; reserve `px` for things that are genuinely fixed — borders, hairlines, 1px offsets — and avoid raw `vw`/`vh` for type (breaks zoom), pairing with `rem` inside `clamp()`.

- the platform basis for each habit (custom properties, `@layer`, logical properties, modern color), plus the full rule text and why these conventions keep a stylesheet survivable under growth and theming — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
