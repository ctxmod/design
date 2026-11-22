# Medium Profile Charter

The contract every <medium> profile must satisfy — capability declaration, slot mapping, token translation, affordance adaptation, confidence note — so new media drop in without rewriting the umbrella.

This is the umbrella's **forward-compatibility contract**. It fixes exactly what
every `<medium>` profile must declare so that new media — `ios`,
`cli`, `latex`, `android`, `windows` — drop in by
filling a template, **never by rewriting the umbrella**.

The umbrella owns the *why* (principles, the semantic token contract, the
abstract component taxonomy). A medium owns the *how-here*: which principles its
runtime can honor, how the umbrella's slots map onto its primitives, how tokens
render in its format, and what affordances its input model supports. The charter
is the seam between the two. Get the charter right and the umbrella stays stable
while the family of media grows.

## The invariant set: ISO 9241-110

A medium may render the umbrella's principles very differently — a CLI has no
hover, LaTeX has no interactive states — but one set of obligations is
**medium-agnostic** and survives every translation: **ISO 9241-110:2020's seven
dialogue principles**.

1. **Suitability for the task** — the surface supports the user's actual goal
   with minimal extraneous steps.
2. **Self-descriptiveness** — at each point the user can tell what is happening
   and what to do next, from the surface itself.
3. **Conformity with user expectations** — behavior matches conventions the user
   already holds for this kind of surface.
4. **Suitability for learning** — the surface helps the user learn it.
5. **Suitability for individualization** — the user can adapt it to their needs
   and abilities.
6. **Error tolerance** — errors are prevented where possible, and recoverable
   when they occur.
7. **Controllability** — the user, not the system, sets the pace and direction
   of the interaction.

These apply to *any* human-facing system — web, CLI, native app, print. They are
the floor a medium may not drop below. Where a medium genuinely cannot express
one (a non-interactive LaTeX document has limited "controllability"), the medium
**declares** the limitation in its confidence note (§5) rather than ignoring it.
The seven principles are the medium-agnostic invariant; the five mandatory
sections below are how a medium proves it has reckoned with them.

## The reference model: Microsoft Fluent 2

The charter's whole premise — *same principles and tokens, different native
rendering per platform* — is not hypothetical. **Microsoft Fluent 2** is the
canonical proof: one design language with one semantic token contract, rendered
natively across Web, Windows, iOS, Android, and macOS. A Fluent button is the
same *contract* everywhere (purpose, variants, states, semantic colors) while its
*rendering* is a `<button>` on web, a `Button` control on Windows, a native
control on each mobile OS. Fluent does not rewrite its principles per platform;
it adds a rendering target. Each medium profile (`<medium>`) is the equivalent
of one Fluent platform binding, and this charter is the contract that binding must
satisfy.

This mirrors the token pipeline exactly: the umbrella's semantic contract is the
source of truth, and a medium is an **emission target**, not an authority (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />).

---

## The contract: five mandatory sections

Every `<medium>` profile MUST provide all five sections below. A medium
profile missing any of them is non-conforming and cannot be relied on by brands
or by lower tooling.

### 1. Capability declaration

Classify **each umbrella principle** against this medium as one of three:

- **supported** — the medium honors the principle as written; the principle's
  obligations apply unchanged.
- **adapted** — the medium honors the principle's *intent* but via a different
  mechanism; the profile states the substitution (e.g. web adapts "hover
  affordance" to pointer-hover + `:focus-visible` for keyboard).
- **dropped** — the medium cannot express the principle and does not pretend to.
  **Dropping is a first-class, declared outcome**, not a silent omission.

> The key move of the whole charter is making **not-applicable explicit**. A CLI
> has no motion and no hover, so `cli` *declares* motion and hover
> **dropped** — it does not leave them ambiguously unaddressed. LaTeX declares
> interactive states (hover/active/focus) **dropped** because a typeset document
> has no runtime interaction. A reviewer reading a medium profile must be able to
> see, for every principle, whether it is in force, substituted, or off the
> table — with the reason.

The same applies to the **universal interaction-state contract**
(default · hover · focus-visible · active/pressed · disabled · loading · error,
see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/states.md" />): a medium
declares which members it honors. Touch-only mediums drop `hover`; `cli`
drops `hover` and `focus-visible`; a static print medium drops all of them.

The ISO 9241-110 seven (above) are exempt from "dropped" wherever the surface is
interactive at all — a medium adapts them, but should not casually drop a
dialogue principle. Any unavoidable drop (e.g. controllability in a static
document) is justified in the confidence note (§5).

### 2. Slot mapping

Map **each slot** in the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />
to the medium's primitive, OR declare the slot **absent** for that medium.

| Slot | web | iOS | CLI | LaTeX |
|------|-----|-----|-----|-------|
| Button | `<button>` | `UIButton` | keybound action line | command / macro |
| Input | `<input>`/`<textarea>` | `UITextField` | prompt + readline | form field env (or absent) |
| Card | `<article>`/`<section>` | `UIView`/`UICollectionViewCell` | **absent** | `tcolorbox` / framed env |

- The mapping is to a **primitive**, not a styling — the slot names a
  responsibility; the medium names the runtime element that carries it.
- **"absent" is a legitimate mapping outcome**, parallel to "dropped" in §1: a
  CLI has no "card" slot, so `cli` declares the Card slot **absent**
  rather than inventing a forced analogue. Absence is declared, with the reason.
- Slots the medium *does* map inherit their Open UI name and APG role semantics
  from the taxonomy unchanged; the medium supplies only the rendering primitive.

### 3. Token translation

State how the umbrella's **primitive/semantic/component tokens render in this
medium's native format.** This is the medium's **transform group** in the
single-source → multi-target pipeline (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />): one
DTCG-compatible source, one named transform group per medium, one emitted
artifact.

| Medium | Token emission target |
|--------|-----------------------|
| Web | CSS custom properties (delivery owned by `shadcn` (typescript module)) |
| iOS | Swift constants — `UIColor` / asset-catalog color sets, `CGFloat` dimensions |
| Android | XML resources (`colors.xml`, `dimens.xml`) |
| CLI | ANSI escape sequences gated on terminal capability (truecolor / 256 / 16 / none) |
| LaTeX | lengths (`\newlength`) and colors (`\definecolor`) |

The medium profile must specify:

- the **format** each token type emits to (color, dimension, duration,
  typography);
- how **modes** (theme / density / locale — see design-tokens.md) re-resolve in
  this medium, or that a given mode axis is unsupported here (e.g. a CLI without
  truecolor collapses the theme axis to whatever the terminal palette allows);
- any **value coercion** the transform group performs (px → pt for LaTeX, hex →
  nearest ANSI index for a 256-color terminal).

The non-negotiable: **the semantic role names and meanings are fixed by the
umbrella.** Adding this medium is adding a transform group, never editing the
contract. A component referencing `color-text-danger` resolves correctly in every
medium because every medium's transform group teaches the pipeline to render that
*existing* role for one more target.

### 4. Affordance adaptation

Declare the medium's interaction reality:

- **Input model** — which of pointer / touch / keyboard / screen-reader /
  text-only the medium supports. (Web: pointer + keyboard + screen-reader. iOS:
  touch + VoiceOver. CLI: keyboard + text-only.) This drives which interaction
  states from §1 are live.
- **Target-size rules** — the minimum hit-target per the applicable WCAG success
  criterion, **calibrated for the medium's viewing distance**. Pointer/touch web
  uses the WCAG 2.2 SC 2.5.8 (Target Size, Minimum) 24×24 CSS-px floor and the
  44×44 best-practice target; a TV/10-foot medium scales targets up for distance;
  a text-only CLI has no pixel targets and instead specifies keystroke economy
  (the primary action reachable in the fewest keystrokes / earliest tab stop —
  the Fitts's-law restatement for non-pointer media, see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />).
- **Viewing distance** — arm's-length (desktop/phone) vs across-the-room (TV)
  vs page-in-hand (print). Distance scales type and target sizing.
- **Density default** — which density mode (compact / comfortable / spacious) the
  medium defaults to (a data-dense desktop tool vs a touch phone differ).

The perception/cognition laws are medium-agnostic and survive translation
unchanged (proximity, Fitts, working-memory limits hold on every surface — see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />); what
the medium adapts is the *units and mechanism* through which it satisfies them.

### 5. Confidence / evidence note (T8)

State, honestly, where this medium's guidance is **extrapolated** versus
**validated**:

- **extrapolated** — derived from the web evidence base + ISO 9241 invariants by
  analogy, not yet confirmed by medium-specific research. Flag it as such.
- **validated** — backed by medium-specific research, platform HIG, or measured
  studies for *this* medium.

The note is **honest, not paralyzing**: an extrapolated guideline is still
actionable; the flag tells a downstream agent how much to trust it and where
medium-specific validation would most improve the profile. Every medium profile
carries this note so no reader mistakes a confident-sounding extrapolation for
settled, medium-validated guidance.

---

## Acceptance test: `web` as a conforming instance

The charter is only credible if the highest-evidence medium we already have fits
it without contortion. Retro-fitting `web` to the five sections:

**1. Capability declaration.** Motion = **supported** (web has a full animation
runtime). Hover = **adapted** — pointer-hover for mice plus `:focus-visible` for
keyboard, so the affordance survives for non-pointer users. All seven interaction
states (default · hover · focus-visible · active · disabled · loading · error)
are **supported**. ISO 9241-110's seven are all supported/adapted (web is fully
interactive, so none is dropped).

**2. Slot mapping.** All seven taxonomy slots map to DOM primitives, none absent:
Button → `<button>`; Input → `<input>`/`<textarea>`/`<select>`; Card →
`<article>`/`<section>`; Layout containers → `<header>`/`<nav>`/`<dialog>` +
CSS layout; Navigation → `<nav>` + `<a>`/`<ul>`; Feedback → ARIA live regions +
`role="alert"`/`role="status"`; Data display → `<table>`/`<dl>`/`<ul>`. Each
inherits its APG role semantics unchanged.

**3. Token translation.** The web transform group emits **CSS custom
properties** (`--color-text-danger`), with delivery owned by `shadcn` (typescript module). Theme
mode re-resolves via `:root` / `[data-theme]` selector swaps; density and locale
re-resolve via the same selector mechanism. Coercion is minimal (the umbrella's
canonical units are already web-native).

**4. Affordances.** Input model = pointer + keyboard + screen-reader. Target size
= WCAG 2.2 SC 2.5.8 (24×24 CSS-px minimum, 44×44 best-practice). Viewing
distance = arm's-length. Density default = comfortable (responsive to compact on
data-dense desktop views).

**5. Confidence note.** Web is the **highest-evidence medium** — the umbrella's
principles were largely synthesized from web research, WCAG, and APG, so
`web` guidance is **validated**, not extrapolated. It is the calibration
baseline other media are measured against.

`web` fits the template cleanly. Therefore a future medium drops in by the
same five-section template — the umbrella does not change, only a new profile is
added.

### Proof sketch: `cli` by the same template

- **Capability:** motion = **dropped** (no animation runtime); hover and
  focus-visible = **dropped** (keyboard-only, no pointer); color/contrast =
  **adapted** to terminal capability; ISO 9241-110 seven = supported/adapted.
- **Slot mapping:** Button → keybound action line; Input → prompt + readline;
  Card → **absent**; Navigation → menu/list with key selection; Feedback →
  status line / colored prefix; Data display → aligned text table.
- **Token translation:** transform group emits **ANSI escape sequences**, gated
  on terminal capability (truecolor → 256 → 16 → none), with hex → nearest-index
  coercion; theme mode collapses to the terminal's available palette.
- **Affordances:** input model = keyboard + text-only; no pixel targets —
  keystroke economy replaces target size (primary action = fewest keystrokes);
  viewing distance = arm's-length; density default = compact.
- **Confidence note:** largely **extrapolated** from web + ISO 9241 by analogy;
  terminal-specific affordance research would most improve it — flagged as such.

Same template, completely different medium, **zero umbrella edits**. That is the
forward-compatibility guarantee the charter exists to provide.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
