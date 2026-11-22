# Forest — Brand

Forest brand identity card — essence, full dark-green/lime palette with OKLCH and contrast notes, technical type pairing, calm motion vocabulary, flat rounded shape system, and do/don't.

The identity card for **Forest**: a sustainability-inspired design system that is
dark-green by default. This file owns the concrete values — palette, type, motion,
shape — that the component files build on. It specializes the umbrella
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" /> for one brand; it does not restate
color, typography, or motion *theory* (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

## Essence

Forest feels **grounded, ecological, technical, and modern**. The references are
deep forest canopy and fresh new growth — not decorative leaf illustrations, but
the *colors* of a living system: dark green ground, a single high-energy lime that
reads like sunlight or a charged signal. The result is serious but optimistic:
trustworthy enough for a finance dashboard, fresh enough for a climate-tech
landing page.

It is **dark-green by default and intentionally focused.** Depth comes from
stepping between green surfaces and from contrast, not from theme switching or
ornament. Use Forest for sustainability and climate-tech products, energy
platforms, ecological-toned dashboards, modern nonprofits, outdoor brands, and
SaaS that wants a calm green identity. Reach for a different brand when the product
needs a light, airy, neutral canvas or a playful, high-chroma multi-color
personality — Forest is committed to its dark green and uses color as scarce
signal (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).

## Color palette

The base is a deep green ladder; the brand energy is one lime accent used
sparingly. OKLCH values are given for reasoning about contrast and for deriving
tints with `color-mix()` (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />); ship the hex.

| Token | Value | OKLCH (approx) | Purpose |
|-------|-------|----------------|---------|
| `--forest-surface` | `#345401` | `0.50 0.13 128` | Primary green page / section background |
| `--forest-surface-deep` | `#1F3400` | `0.36 0.10 130` | Secondary panels, darker layout areas, wells/inputs |
| `--forest-surface-raised` | `#3E6402` | `0.57 0.14 128` | Cards / raised surfaces (one step lighter than base) |
| `--forest-brand` | `#A1DA02` | `0.83 0.21 127` | Primary actions, highlights, active states, brand moments |
| `--forest-brand-medium` | `#C6ED6B` | `0.90 0.17 122` | Bright supporting accents, focus rings, hover lift |
| `--forest-heading` | `#F4FAE8` | `0.97 0.03 120` | High-contrast headings on green |
| `--forest-body` | `#C9D6B0` | `0.84 0.06 121` | Paragraphs, labels, supporting UI copy |
| `--forest-border` | `#4C7A05` | `0.62 0.15 128` | Hairline borders, dividers, input outlines |
| `--forest-on-brand` | `#16270A` | `0.28 0.06 128` | Text/icons placed *on* the lime brand fill |

Semantic status tokens, chosen to read clearly against deep green (greens read as
brand, so success leans on the lime family while error/warning take warm hues that
cut through the green ground):

| Token | Value | Purpose |
|-------|-------|---------|
| `--forest-success` | `#A1DA02` | Success — the brand lime doubles as success (affirming, on-brand) |
| `--forest-success-fg` | `#16270A` | Text on a lime success fill |
| `--forest-warning` | `#F2B705` | Warning — warm amber, distinct from lime, visible on green |
| `--forest-danger` | `#FF5C49` | Error / destructive — warm red, high contrast on green |
| `--forest-danger-fg` | `#1F3400` | Text on a red danger fill |
| `--forest-info` | `#1F3400` | Info — neutral deep-surface tint (calm, no hue claim) |

### Contrast considerations

- **Lime accent on green is the headline risk.** `--forest-brand` (`L≈0.83`) on
  `--forest-surface` (`L≈0.50`) clears ~3:1 — fine for large text, UI borders, and
  focus rings, but **not** for small body text. Never set small lime text on a
  green surface; use it as fill, icon, indicator, or large display only (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> contrast table).
- **Use lime as a fill, dark text on top.** Primary buttons are lime fill with
  `--forest-on-brand` dark text — that pairing clears AA comfortably and keeps the
  lime legible. Lime text on green never does.
- **Success vs. error must differ by more than hue.** Because success is lime
  (green family) and error is warm red, always pair both with an icon and label
  (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/feedback.md" />) so the distinction survives color-blindness.
- Verify each accent **in situ** — the same lime reads differently on
  `--forest-surface` vs `--forest-surface-deep` (simultaneous contrast).

## Typography

Forest's voice is **technical and modern** — confident headings, calm body. The
lime accent carries the energy, so type stays grounded and direct (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />).

- **Headings — geometric / grotesque sans.** A clean geometric sans (e.g. *Space
  Grotesk*, *Söhne*, *Inter Display*) at tighter tracking. Confident, structural,
  not decorative.
- **Body — a quiet workhorse sans.** A highly legible neutral sans (e.g. *Inter*,
  *IBM Plex Sans*) for paragraphs, labels, and form copy in `--forest-body`.
- **Data / mono — a humanist mono** (e.g. *JetBrains Mono*, *IBM Plex Mono*) for
  metrics, code, and tabular figures — fitting the ecological-technical register.

Type scale — **minor third (1.200)**, a balanced general-purpose ratio that keeps
dense dashboards readable while still giving headings a clear step up:

| Role | Size | Line height | Weight |
|------|------|-------------|--------|
| Display | 3.05rem | 1.1 | 600 |
| H1 | 2.44rem | 1.15 | 600 |
| H2 | 2.03rem | 1.2 | 600 |
| H3 | 1.69rem | 1.25 | 600 |
| H4 | 1.41rem | 1.3 | 500 |
| Body | 1rem | 1.6 | 400 |
| Small | 0.83rem | 1.5 | 400 |
| Caption / overline | 0.69rem | 1.4 | 500 |

Put identity in the large, short text (headings in `--forest-heading`); keep body
quiet and legible. Reserve weight for genuine hierarchy.

## Motion vocabulary

Forest moves like a natural system: **calm, grounded, subtle.** Nothing bounces.

- **Easing** — organic `ease-in-out` for movement within view, `ease-out` for
  entrances, `ease-in` for exits (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />). **No spring /
  overshoot** — playfulness would undercut the trustworthy register.
- **Duration** — favor the *fast* and *moderate* bands: micro-feedback at
  100–150ms, transitions at 200ms, larger surfaces (drawers, modals) at ~280ms.
  Avoid anything that feels languid.
- **Restraint** — motion confirms and orients, it does not decorate. No scattered
  micro-interactions. One calm staggered reveal beats many flourishes.
- **Reduced motion** — every animation degrades to an instant state change or a
  simple opacity fade; this is implemented at the medium tier via
  `prefers-reduced-motion` (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />) — author so removing motion
  loses delight, never function.

Suggested tokens: `--forest-dur-fast: 130ms; --forest-dur: 200ms;
--forest-dur-lg: 280ms; --forest-ease: cubic-bezier(0.4, 0, 0.2, 1);`.

## Shape & surface

Forest is **flat and rounded**. Separation comes from green surface steps,
hairline borders, and spacing — never from drop shadows.

- **Flat by default** — no drop shadows on cards, buttons, inputs, badges, or
  panels. Elevation is communicated by stepping to a *lighter* green
  (`--forest-surface-raised`) and/or a `--forest-border` hairline.
- **Generously rounded** — corner-radius scale:

| Token | Value | Use |
|-------|-------|-----|
| `--forest-radius-sm` | 6px | Inputs, badges, small controls |
| `--forest-radius-md` | 10px | Buttons |
| `--forest-radius-lg` | 16px | Cards, panels |
| `--forest-radius-xl` | 24px | Large containers, hero panels |
| `--forest-radius-pill` | 9999px | Pills, toggles, chips |

- **Spacing** — 8px rhythm (inherited spacing scale), equal section spacing,
  ~1152px max content width, breathable layouts.
- **Borders** — 1px `--forest-border` hairlines; lift to `--forest-brand` only for
  focus/active signal.

## Do / Don't

**Do**

- Keep surfaces deep green; build depth from surface steps and borders.
- Use lime as scarce **signal** — primary actions, active states, focus, key
  highlights.
- Put dark text (`--forest-on-brand`) on lime fills for legible primary buttons.
- Keep components flat; rely on green contrast and hairlines for separation.
- Generously round cards and containers.

**Don't**

- Don't add gradients or drop shadows — they break the flat, grounded feel.
- Don't set small lime text on a green surface (fails contrast).
- Don't spread lime across the screen — it stops being a signal.
- Don't switch to a light theme; Forest's identity is its dark green.
- Don't let success (lime) and error (red) rely on hue alone — always icon+label.
- Don't add bouncy/springy motion — keep it calm and natural.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/navigation.md" />
