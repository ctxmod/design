# Platform Primitives

The web's native design primitives — CSS custom properties as token carriers, @layer and @property, modern selectors, logical properties, OKLCH/color-mix, and SVG/Canvas — atop which Tailwind is one delivery mechanism.

The umbrella defines a <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" /> and a token
model in the abstract. This document names the **web's native carriers** for those
abstractions — the CSS, SVG, and Canvas primitives a brand profile ultimately
writes its values into. It is the cross-reference partner to the Tailwind
architecture doc (`v4/reference/architecture.md` in `github.com/ctxmod/typescript/context`, profile
`tailwind`): Tailwind is *one delivery mechanism* layered on top of these
primitives, not a
replacement for them. Knowing the primitives keeps a design portable across — and
independent of — any framework.

## CSS custom properties: the token carrier

Custom properties (`--name`) are the web's native home for design tokens. A token
defined once and referenced everywhere is exactly the umbrella's design-language
discipline, made literal:

```css
:root {
  --color-accent: oklch(0.72 0.15 160);
  --space-4: 1rem;
  --radius-card: 1.25rem;
  --dur-fast: 150ms;
}
.card { border-radius: var(--radius-card); }
```

- They **cascade and inherit**, so a token can be overridden per-subtree (theming a
  region, a dark island in a light page) without touching the component.
- They are **live at runtime** — readable and settable from JS, switchable by media
  query — which is what makes `prefers-color-scheme` theming and runtime brand
  switching possible.
- Group tokens by role (color, space, radius, type, motion) the way the umbrella's
  token model prescribes; a brand profile fills these values, the medium and
  framework just consume them. (Tailwind v4's `@theme` generates exactly such
  custom properties — see the Tailwind architecture reference in the `typescript` module — but the variables are the
  source of truth either way.)

## `@layer`: managing the cascade

`@layer` gives explicit, author-defined ordering to the cascade so specificity wars
disappear:

```css
@layer reset, base, tokens, components, utilities;
```

- Later layers win over earlier ones *regardless of selector specificity*, so a
  low-specificity utility can override a high-specificity component without
  `!important`.
- A predictable layer order (reset → base → tokens → components → utilities) is the
  structural antidote to the "CSS selectors cancelling each other out" failure the
  frontend-design guidance warns about.
- Unlayered styles beat layered ones, so keep almost everything in a layer and
  reserve unlayered CSS for deliberate final overrides.

## `@property`: typed custom properties

Plain custom properties are untyped strings, so they can't be animated or
validated. `@property` registers a type:

```css
@property --angle { syntax: "<angle>"; inherits: false; initial-value: 0deg; }
```

This makes a custom property **animatable** (e.g. an animated conic gradient angle
or a transitioning length) and gives it a guaranteed initial value — enabling
token-driven motion that would otherwise be impossible.

## Modern selectors

The web now expresses relationships that once required JS or extra classes:

- **`:has()`** — the long-missing parent/sibling selector. Style a card that
  *contains* an image, a label whose input is invalid, a form that has an error —
  reactive styling without state classes.
- **`:is()` / `:where()`** — group selectors; `:where()` contributes **zero
  specificity**, ideal inside `@layer`-ed component styles to keep overrides easy.
- **`:focus-visible`** — keyboard-only focus, the basis of the
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_accessibility.md" /> focus rule.
- **`:focus-within`**, **`:placeholder-shown`**, **`:user-invalid`** — state-driven
  styling that maps onto the umbrella's component states with no JavaScript.
- **`@scope (.card) to (.card__slot)`** — limits a block of rules to a component
  subtree (with an optional lower boundary), giving proximity-based styling
  without BEM-style naming; Baseline newly available since 2026-03.

## Logical properties

Logical properties describe layout by *flow* (block/inline, start/end) instead of
physical (top/left/right/bottom):

```css
.card { padding-inline: var(--space-4); margin-block-end: var(--space-6); }
```

- They adapt automatically to writing mode and direction (LTR/RTL), so a single
  rule works in left-to-right and right-to-left without mirrored overrides — an
  internationalization and accessibility win.
- Prefer `padding-inline`/`margin-block`/`inset`/`border-inline` over their physical
  equivalents for everything directional. (Enforced by the
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/rules/css_conventions.md" />.)

## Modern color: OKLCH, color-mix, relative colors

CSS color has caught up with how designers actually think about color (see the
umbrella's color principle):

- **OKLCH** — perceptually-uniform lightness/chroma/hue. Equal lightness steps look
  equally bright, so a tonal scale built in OKLCH is even where the same steps in
  HSL/hex are lumpy. The natural space to *define* a palette.
- **`color-mix()`** — derive tints, shades, and overlays from base tokens
  (`color-mix(in oklch, var(--accent) 12%, transparent)` for a badge background),
  so a brand defines a few anchors and the system computes the rest.
- **Relative color syntax** — transform a color in place (`oklch(from var(--accent)
  l c h / 0.5)`) to derive a variant from a token.
- Generated colors still owe the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_accessibility.md" /> thresholds —
  verify them; a perceptually-even ramp is not automatically an accessible one.

## Baseline: deciding what a design may depend on

"Supported" is not a yes/no. Use the cross-browser **Baseline** status from the
web-features data set (shown on MDN, caniuse and webstatus.dev) to decide how a
design may lean on a feature:

- **Widely available** (in every core browser for 30 months) — depend on it
  freely.
- **Newly available** (just reached every core browser) — use it, but the
  experience must still work for users on older engines: guard with
  `@supports` or let it fail soft.
- **Limited availability** — progressive enhancement only; the design must be
  complete without it.

Status as of 2026-11 for the primitives this profile leans on:

| Feature | Baseline (2026-11) | Design consequence |
|---|---|---|
| Cascade layers, container size queries, `color-mix()`, OKLab/OKLCH | Widely available | Default tools; no fallback needed |
| `:has()` | Widely available (2026-06) | Reactive parent/state styling without classes |
| `light-dark()`, `text-wrap: balance` | Widely available (2026-11) | Theme tokens in one declaration; balanced headings |
| Relative color syntax, `@starting-style`, `transition-behavior` | Newly available (2024) | Derived tints; entry/exit transitions for `display` and top-layer elements |
| Popover API | Newly available (2025-01) | Declarative top-layer menus, toggletips, non-modal overlays |
| `@scope` | Newly available (2026-03) | Component-scoped styles without naming conventions |
| `contrast-color()` | Newly available (2026-04) | Auto white/black text; still verify body-text contrast (see the color principle) |
| Anchor positioning | Limited | Tether popovers/tooltips to their trigger as enhancement; keep a non-anchored fallback position |
| Customizable `<select>` (`appearance: base-select`), `interpolate-size`, `if()` | Limited | Enhancement only |

Re-check the status before a design hard-depends on a Newly or Limited feature —
the data moves monthly.

### Theme tokens with `light-dark()`

With `color-scheme: light dark` on `:root`, a semantic token can carry both
theme values in one place — `--color-surface: light-dark(oklch(0.98 0.01 90),
oklch(0.22 0.01 90));` — so the theme mode re-resolves the role without a
duplicate selector block (the token model's "modes re-resolve, components don't
change").

### Top-layer primitives: `<dialog>`, popover, anchors

Native top-layer elements replace most hand-rolled overlay code and bring
focus, Esc and stacking behaviour with them:

- **`<dialog>` with `showModal()`** for modal dialogs (inert background, focus
  moved into the dialog).
- **The `popover` attribute** (`popovertarget` on the trigger) for menus,
  pickers and toggletips — light dismiss and top-layer stacking without
  `z-index` wars.
- **Anchor positioning** (`anchor-name` / `position-anchor` / `position-area`,
  with `position-try-fallbacks`) to keep a popover tethered to its trigger;
  limited availability, so the popover must still be usable where it falls back.
- Animate their entry and exit with `@starting-style` and
  `transition-behavior: allow-discrete`, and keep the reduced-motion contract
  from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />.

## SVG for icons and illustration

SVG is the web's vector primitive — resolution-independent, stylable, scriptable:

- Icons and flat illustration as SVG scale crisply at any size and zoom, stay sharp
  on every DPI, and reserve their box for free (no CLS).
- Inline SVG inherits `currentColor` and is styleable/animatable with CSS, so an
  icon recolors with its text and theme automatically — the token system reaches
  into the graphic.
- SVG is also a small-payload way to deliver patterns, gradients, masks, and the
  noise textures premium UI uses, without raster weight.

## Canvas / WebGL for generative visuals

When the visual is *generated* rather than drawn — particle fields, data-driven
graphics, fluid/shader backgrounds, real-time visualization — Canvas 2D and WebGL
are the primitives:

- Reach for them only when SVG/CSS genuinely can't express the effect; they cost
  main-thread or GPU work and are opaque to assistive tech, so provide an accessible
  alternative and a <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />/static fallback.
- Keep them inside the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/rendering_performance.md" />: a heavy
  generative background that drops frames undermines the design it was meant to
  elevate.

## Tailwind is a delivery mechanism, not the primitive

Everything above is the platform. Tailwind (and shadcn, CSS-in-JS, vanilla CSS) are
ways to *author* against these primitives — Tailwind v4 in particular compiles to
custom properties, `@layer`, and `@property`, as the
`v4/reference/architecture.md` in `github.com/ctxmod/typescript/context` (profile `tailwind`) doc describes. A
`web` design should be expressible in plain CSS using these primitives;
the framework chosen to ship it is a frontend-framework concern (the `typescript` module), not a medium one.
Build on the primitive, and the brand survives a change of framework.

## Rule Companion: CSS Conventions — Full Rule and Rationale

*Companion to the `css_conventions` rule: its full rule set, worked examples and rationale.*

### The rules

- **Tokens are custom properties.** Every color, space, radius, font, shadow, and
  duration is a `--custom-property`, referenced via `var()` — never a hard-coded
  literal scattered through rules. A brand retunes the system by changing variables,
  not by hunting for hex values.
- **Order the cascade with `@layer`.** Declare an explicit layer order
  (`@layer reset, base, tokens, components, utilities`) so later layers win by
  position, not specificity. Keep almost all CSS inside a layer.
- **Prefer logical properties.** Use `padding-inline`, `margin-block`, `inset`,
  `border-inline` over physical `left`/`right`/`top`/`bottom` for anything
  directional, so RTL and vertical writing modes work without mirrored overrides.
- **Mobile-first media queries.** Base styles describe the smallest layout;
  `min-width` queries add complexity upward. Avoid `max-width`-first authoring
  except for deliberately desktop-centric tools.
- **Container queries for components.** A reusable component should react to its
  *container* (`@container`), not the viewport. Reserve media queries for the
  page-level shell and device-level concerns (pointer type, color scheme, reduced
  motion).
- **No `!important`.** If a rule needs `!important` to win, the cascade is
  mis-layered — fix the `@layer` order or selector instead. The only tolerated use
  is the `prefers-reduced-motion` safety-net reset.
- **Gate features on Baseline.** Widely-available features are the default; a
  Newly-available feature needs a working experience without it (`@supports` or
  fail-soft); a Limited-availability one is enhancement only. Check the current
  status (see "Baseline" above) rather than assuming it.
- **Unit discipline.** `rem` for type and spacing (honors user zoom), `%`/`fr`/`ch`
  for fluid layout and measure, `clamp()` for fluid scaling. Reserve `px` for things
  that are genuinely fixed — borders, hairlines, 1px offsets. Avoid raw `vw`/`vh` for
  type (breaks zoom); pair with `rem` inside `clamp()`.

### Why

These conventions are what make a stylesheet survive growth and theming. Custom
properties and `@layer` turn "override the third declaration and pray" into
predictable, low-specificity changes; logical properties and `rem` make the design
work for users and locales you didn't test; container queries make components
genuinely reusable. The discipline is invisible when it works and the source of
every "why won't this style apply" bug when it's skipped.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/responsive_layout.md" />

## Sources

- https://web.dev/baseline — Baseline definitions (Widely / Newly / Limited availability); accessed 2026-11-23
- https://api.webstatus.dev/v1/features/ — web-features Baseline status per feature id (`cascade-layers`, `container-queries`, `has`, `oklab`, `color-mix`, `light-dark`, `text-wrap-balance`, `relative-color`, `starting-style`, `transition-behavior`, `popover`, `scope`, `contrast-color`, `anchor-positioning`, `customizable-select`, `interpolate-size`, `if`); queried 2026-11-23
- https://drafts.csswg.org/css-color-5/ — CSS Color 5: `color-mix()`, relative color, `light-dark()`, `contrast-color()`; Editor's Draft; accessed 2026-11-23
