# Internationalization

Internationalization is token-level — language affects typography/density tokens; RTL is spatial rethinking, not mirroring. Locale is one of three orthogonal token modes.

Internationalization (i18n) is routinely treated as a content problem — extract
the strings, send them to translation, swap them back in. That is the smallest
part of it. **i18n is a token-level concern**: changing the locale changes the
*resolved values* of the design system itself, not just the words rendered into
it. A system that only translates strings and leaves its typography and spacing
fixed to Latin assumptions is not internationalized; it is a Latin design that
happens to display foreign text, usually badly.

## What + why: language drives tokens, not just content

Two token categories re-resolve per locale.

**Typography tokens.** Type metrics that read as neutral defaults are in fact
Latin defaults. Other scripts have different metric requirements that must be
expressed as locale-resolved typography tokens, not patched per component:

- **Family** — the body and display faces differ per script. A Latin face has no
  CJK, Arabic, Devanagari, or Thai coverage; the locale selects the face stack.
- **Weight** — many CJK faces ship a single weight and lack a true bold. The
  emphasis that Latin gets "for free" from `font-weight-bold` must be supplied by
  a **weight override** (a heavier face, or a non-weight emphasis treatment) at
  the token tier, so `font-weight-emphasis` still means *emphasis* in that locale.
- **Line-height** — CJK glyphs are dense, full-height, and have no descenders to
  separate lines; they need a **larger line-height** than Latin body copy to stay
  legible. The body leading token resolves looser for CJK.
- **Letter-spacing** — Arabic is cursive and connected; positive tracking that
  helps a Latin all-caps label *breaks* Arabic by pulling joined glyphs apart.
  The tracking token resolves to a different (often zero or negative) value, and
  some locales disable tracking entirely.

**Density tokens.** Text length is locale-dependent. German runs ~30–40% longer
than English; many CJK strings are shorter but taller. Layouts pinned to
English-width assumptions clip, wrap unpredictably, or leave dead space. Spacing
and sizing tokens (`space-component-pad`, min-widths, label columns) must **flex
per locale** rather than encode one language's string lengths as fixed geometry.

## RTL is spatial rethinking, not mirroring

Right-to-left and bidirectional layout is not `direction: rtl` bolted on at the
end. Switching to a RTL locale **reorders spatial relationships**, and several of
those reorderings are semantic decisions a stylesheet flag cannot make:

- **Reading flow reverses** — the start edge moves to the right; content,
  alignment, and the natural eye-path along a row all flip.
- **Navigation mirrors** — back/forward, breadcrumbs, progress, and primary
  navigation reverse, because "next" follows the reading direction.
- **Directional icons flip** — arrows, chevrons, send, and undo point the other
  way. But **non-directional icons must not flip**: a clock, a checkmark, a
  logo, or a media play-button stays as it is. Blanket mirroring is a bug.
- **Numerals, charts, and progress** keep their own conventions — digits and most
  data visualizations are not mirrored even inside RTL text.

Treating RTL as an afterthought produces interfaces that are technically reversed
but spatially wrong: flipped clocks, backwards play buttons, charts reading the
wrong way. RTL is a layout pass, not a CSS property.

## Boundary decision (Theme 13 / T)

The split between what locale changes is **token-tier** and what it changes is
**medium-tier**:

- **Locale-aware typography lives at the TOKEN tier.** The family / weight /
  line-height / letter-spacing overrides above are typography *tokens* that
  resolve per locale (locale is a token mode — see below). The locale picks the
  resolved value; call sites still reference the same semantic role
  (`font-weight-emphasis`, `line-height-body`) and change nothing.
- **RTL / bidi layout lives at the MEDIUM tier.** Direction is a spatial
  rendering concern the medium owns: on the **web**, CSS **logical properties**
  (`margin-inline-start`, `inset-inline`, `text-align: start`) plus the `dir`
  attribute and `:dir()` for the directional-icon exceptions; on **native**, the
  platform's layout-direction APIs. The token system does not encode left/right;
  it encodes *start/end*, and the medium resolves which is which.

State it plainly: **typography → tokens, direction → medium.** A token file that
hardcodes `left`/`right` has leaked a medium concern; a medium that hardcodes
Latin type metrics has leaked a token concern.

## Orthogonal modes

Locale is the third of the design system's three **token modes**, alongside
theme and density (see the Modes section of
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />). The three are
**orthogonal axes** — any theme combines with any density combines with any
locale:

- **theme** (light / dark) re-resolves semantic *color* tokens.
- **density** (compact / comfortable / spacious) re-resolves semantic *spacing /
  sizing* tokens.
- **locale** (language / region) re-resolves semantic *typography* tokens.

The critical property they share: **a mode is not a new layer.** All three
re-resolve the **semantic → primitive** mapping over the *same role names*. A
component referencing `font-weight-emphasis` works in dark + compact + Arabic
without knowing any of those modes exist. Locale changing typography adds no
layer and no component branching, exactly as theme changing color does not.

## Obligations

- Express script-dependent type metrics (family, weight, line-height,
  letter-spacing) as **typography tokens that resolve per locale**, never as
  per-component overrides.
- Provide a **weight / emphasis override** for locales whose faces lack a bold;
  `font-weight-emphasis` must still produce emphasis in every locale.
- Let **density tokens flex per locale** so longer (German) and taller (CJK) text
  fits without clipping or hardcoded English widths.
- Author layout with **start/end logical properties**, never `left`/`right`, so
  the medium can resolve direction.
- **Flip only directional icons** under RTL; leave non-directional glyphs,
  numerals, and most charts unmirrored.
- Keep locale **orthogonal** to theme and density — no mode may assume another's
  value, and none may introduce a new layer.

## How to verify

- Switch the system to a **CJK locale** and confirm typography tokens resolve:
  body line-height loosens, emphasis renders as real emphasis despite no bold
  weight, and no Latin metric leaks through.
- Switch to an **RTL locale** (e.g. Arabic) and confirm the layout *reorders* —
  start edge on the right, navigation mirrored, directional icons flipped,
  clocks / play buttons / logos *not* flipped — and that this came from logical
  properties + `dir`, not a one-off reversed stylesheet.
- Render the **longest** locale (German) in the tightest density and confirm
  spacing tokens flex rather than clip or overflow.
- Combine all three modes (dark + compact + Arabic) and confirm components are
  unchanged — they reference the same semantic roles in every combination.

## Anti-patterns

- **String-only i18n** — translating copy while leaving typography and spacing
  fixed to Latin metrics; the result reads as a Latin design wearing foreign text.
- **Hardcoding Latin metrics** — baking English line-height, Latin tracking, or
  an assumed bold weight into base styles so other scripts inherit wrong metrics.
- **`direction: rtl` as the whole RTL story** — flipping text direction without
  reordering navigation, fixing directional icons, or sparing non-directional
  ones; produces backwards clocks and play buttons.
- **Blanket icon mirroring** — reversing *every* icon in RTL instead of only the
  directional ones.
- **`left` / `right` in tokens or layout** — encoding physical sides instead of
  `start` / `end`, which prevents the medium from resolving direction.
- **Locale as a new layer or a component branch** — adding per-locale components
  or layers instead of re-resolving the semantic → primitive typography mapping,
  the way theme and density already do.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
