# Color

Principles of color in UI — identity vs. signal, OKLCH reasoning, semantic vs. brand tokens, surface steps, and WCAG contrast.

Color in UI does two jobs: it carries **identity** (this product looks like
itself) and it carries **signal** (this thing is an action, that thing is an
error). Good color systems keep these jobs distinct and use color with
discipline. The most common failure is treating color as decoration —
distributing many hues evenly until nothing means anything.

This document covers the *principles* of color. The delivery mechanism (CSS
custom properties, Tailwind tokens, shadcn theme variables) belongs to the
`shadcn` (typescript module) profile — see the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />
for the layering model.

## Perceptual color spaces (use OKLCH)

Reason about color in a *perceptually uniform* space rather than sRGB hex.
OKLCH approximates perceptual uniformity per the OKLab model (Ottosson) — equal
numeric steps map to equal *perceived* steps in lightness and chroma, which is
the warrant for the consequences below: a generated scale built on even numbers
looks even to the eye. In OKLCH (Lightness, Chroma, Hue):

- **Equal lightness steps look equally different.** A ramp built by stepping `L`
  evenly produces visually even tints/shades; the same in HSL does not.
- **Changing hue at constant L and C does not change perceived brightness.** This
  is what makes accessible, swappable palettes tractable: you can re-hue a brand
  while preserving contrast.
- **Chroma is independent of lightness**, so you can desaturate toward neutrals
  predictably.

Practical rule: define surface and text ramps as evenly-spaced lightness steps at
low chroma, and define accents as a hue at controlled chroma. Convert to the
delivery format (hex/`oklch()`/RGB — `oklch()` is specified in
[CSS Color 4 §9.2](https://www.w3.org/TR/css-color-4/#the-oklch-notation)) at the
token layer, not in your head.

Evenly-spaced lightness steps are the sensible **default**. When you need
*guaranteed* WCAG compliance across a ramp, a more rigorous **option** is to
generate each step from a target contrast ratio against its intended
background rather than from an even lightness interval — Adobe Spectrum derives
its color scales this way. This is an option to reach for when contrast must be
provably correct, not a mandate; the even-step default is fine for most ramps.

## Semantic vs. brand tokens

Separate two layers of meaning (this mirrors the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />):

- **Brand / primitive colors** — the raw palette ("brand-600", "teal-400"). These
  belong to a brand profile. They have no inherent meaning.
- **Semantic colors** — roles the UI assigns: `bg-surface`, `text-primary`,
  `text-muted`, `border`, `accent`, `accent-foreground`, plus status roles
  `success`, `warning`, `danger`, `info`. The umbrella owns this *contract*;
  brands wire primitives into it.

Components reference **semantic** tokens only. A button uses `accent`, never
`teal-400`. This is what lets a brand swap without touching components, and what
keeps light/dark themes coherent (the role is stable, the value changes).

## Color as signal, used sparingly

Treat saturated color as a scarce resource:

- Most of a well-designed screen is **neutral** — a small set of surface and text
  steps. Color appears where it carries meaning.
- A **dominant** neutral ground with **sharp** accent moments outperforms a
  palette where five colors each claim 20% of the screen. Restraint creates the
  contrast that makes the accent legible (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />).
- **Status colors are reserved.** Red means danger/error everywhere, or it means
  nothing. Do not use the danger hue decoratively.
- Avoid the AI-default purple-to-blue gradient on white. It signals "generic,"
  not "designed."

## Surface steps (light and dark)

Build a small ladder of surface levels rather than one background:

| Role | Light | Dark |
|------|-------|------|
| Base background | Off-white / warm neutral (not pure `#fff`) | Near-black / warm charcoal (not pure `#000`) |
| Raised surface (cards) | Slightly lighter or with a hairline border | Slightly *lighter* than base (light recedes in dark UIs) |
| Sunken surface (wells, inputs) | Slightly darker | Slightly darker still |
| Overlay (modals) | Base + scrim behind | Base + scrim behind |

Key asymmetry: in light mode, elevation is suggested by **shadow**; in dark mode,
shadows barely read, so elevation is suggested by making raised surfaces
**lighter** and using borders. Do not reuse light-mode shadows in dark mode.

Dark mode is **role-remapping with different contrast targets**, not value
inversion. The semantic role stays stable (`bg-surface`, `text-primary`,
`accent`) while its value is re-chosen for a dark ground — you do not flip the
light palette's numbers. Two things shift specifically: contrast targets are met
against a dark background (so an accent that cleared 4.5:1 on white usually needs
a lightness nudge to clear it on charcoal), and elevation cues invert (lighter
surfaces plus borders instead of shadows, per the asymmetry above). The fuller
dark-mode treatment lives in its own dark-mode reference; this paragraph is the
color-system view of it.

Pure black text on pure white is harsh; soften both ends (near-black text, warm
off-white ground) for readability without losing contrast.

## Contrast and WCAG

Contrast is non-negotiable because it is the difference between readable and
unreadable for a large fraction of users. Target the WCAG ratios:

| Content | Minimum (AA) | Enhanced (AAA) |
|---------|--------------|----------------|
| Body text (< 18 pt ≈ 24px / < 14 pt ≈ 18.66px bold) | 4.5 : 1 | 7 : 1 |
| Large text (≥ 18 pt ≈ 24px / ≥ 14 pt ≈ 18.66px bold) | 3 : 1 | 4.5 : 1 |
| UI components & graphical objects (borders, icons, focus rings) | 3 : 1 | — |

Notes:

- These ratios are the normative success criteria **SC 1.4.3** (AA body/large
  text), **SC 1.4.6** (AAA), and **SC 1.4.11** (AA non-text/UI components);
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" /> is the canonical home
  for the criterion numbers and the AA-floor / AAA-stretch conformance position.
- **Contrast is against the actual background**, including overlays and images.
  Text on a photo needs a scrim.
- **Do not encode meaning in hue alone.** Color-blind users must still perceive
  error vs. success — pair color with an icon, label, or shape (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
- Accent colors often need a lightness nudge between light and dark themes to keep
  the 4.5:1 ratio against their changed background.
- **The WCAG 2 ratio is still the conformance test.** APCA and other perceptual
  contrast models are research inputs to the WCAG 3 drafts, not a requirement of
  any Recommendation; use them, if at all, as an extra design signal alongside
  the 2.x ratios, never instead of them.
- **Platform auto-contrast is a fallback, not a guarantee.** CSS
  `contrast-color()` (Baseline newly available 2026-04) picks white or black for
  text on a solid background with a UA-defined algorithm, and the spec only asks
  the result to meet the AA *large-text* bar (3 : 1). Body text chosen this way
  still owes a 4.5 : 1 check against the real background.

## Color in context

Perceived color is relative — a swatch shifts depending on what surrounds it
(simultaneous contrast). Consequences:

- Judge colors in situ, in the real layout, not on an isolated swatch board.
- The same accent reads differently on a card vs. on the base background; verify
  contrast for each context it actually appears in.
- A neutral with a faint hue bias (warm grey, cool grey) unifies a palette;
  perfectly neutral greys can feel sterile. Pick a bias and apply it
  consistently, tying it to the design language (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />).

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />

## Sources

- https://www.w3.org/TR/WCAG22/ — WCAG 2.2 "large scale" definition (18 pt, or 14 pt bold) and SC 1.4.3 / 1.4.6 / 1.4.11 ratios, edition 2024-12-12; accessed 2026-11-23
- https://drafts.csswg.org/css-color-5/#contrast-color — CSS Color 5 `contrast-color()`: white/black only, UA-defined algorithm, result should meet AA large text; Editor's Draft; accessed 2026-11-23
- https://api.webstatus.dev/v1/features/contrast-color — web-features Baseline status: newly available 2026-04-10 (Chrome 147, Firefox 146, Safari 26); accessed 2026-11-23
