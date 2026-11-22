# Token Translation

Charter section 3 for the paginated-print medium — the LaTeX transform group. Spacing to mm/pt/em, type scale to point sizes against base-font-size, color to a print-safe gamut, elevation to rules and whitespace, and the mode axes that collapse.

This is **section 3 of the five the medium charter makes mandatory**. It states
how the umbrella's primitive, semantic, and component tokens render in this
medium's native format — the medium's **transform group** in the single-source
→ multi-target token pipeline
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />).

The charter's own emission table already names this medium's target: **LaTeX —
lengths (`\newlength`) and colors (`\definecolor`)**. This profile adopts it.
The transform group runs at typeset time; there is no runtime re-resolution,
which is what makes the mode analysis below so short.

**The non-negotiable:** the semantic role names and their meanings are fixed by
the umbrella. Adding this medium is **adding a transform group, never editing
the contract**. A component referencing `color-text-danger` resolves correctly
here because this transform group teaches the pipeline to render that
*existing* role for one more target — it does not rename, re-scope, or
re-define the role.

## Emission format per token type

| Token type | Emits to | Form |
|---|---|---|
| **Dimension** | LaTeX length | `\newlength` / `\setlength` in `mm`, `pt`, or `em` |
| **Color** | LaTeX color | `\definecolor` in a print-safe model (see below) |
| **Typography** | Point size + face selection | A resolved `pt` size plus the family/weight the style names |
| **Duration** | **nothing — discarded** | The medium has no time axis; see [value coercion](#value-coercion) |

## Spacing scale → `mm` / `pt` / `em`

The umbrella's spacing scale survives as a scale; only its units change. The
transform group resolves each step to one of three units, chosen by what the
step is measuring:

- **`mm`** for page-level geometry — margins, gutter, header and footer
  separation, trim-relative offsets. These are physical distances on a physical
  sheet and are most legible to an author in millimetres.
- **`pt`** for typographic geometry — rule thickness, baseline-adjacent gaps,
  float separation. A point is the unit the type is already measured in, so
  these values stay commensurable with leading.
- **`em`** for type-relative spacing — space before and after a heading, indent
  depth, inline gaps. An `em` step scales with whatever size the surrounding
  role resolved to, which keeps the rhythm intact across roles without a second
  scale.

The page margins become the largest step in the scale. This is a real
difference from the web, where the outermost gutter is elastic: here it is a
fixed subtraction from a fixed sheet, and every other spacing decision spends
what it leaves behind.

## Type scale → point sizes against `base-font-size`

The umbrella's modular type scale resolves to absolute point sizes. The
resolution is two-factor and comes from the rendering style:

```
resolved_pt(role) = base-font-size × styles.<role>.size
```

A style declares `typography.base-font-size` (typical values are `10.0`,
`11.0`, and `11.04`) and a per-role `size:` multiplier under
`typography.styles`. A style with `base-font-size: 11.0` and `body.size: 1.0`
resolves body to **11pt**; the same style's `h1.size: 1.3` resolves to
**14.3pt**; its `footnote.size: 0.82` resolves to **9.02pt**.

Two consequences the transform group must preserve:

- **The multiplier is the scale; the base is the calibration.** Changing
  `base-font-size` moves the whole document without disturbing the ratios
  between roles. Hard-coding an absolute `pt` at a call site breaks that and is
  the print form of the umbrella's magic-number prohibition.
- **The umbrella's `≥ 16px` body floor does not transfer.** It is a screen
  figure at screen viewing distance. The print floor is derived from reading
  distance instead — see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/affordance_adaptation.md" />.

## Color → a print-safe subset

The umbrella's semantic color roles survive; the gamut does not.

- **Subtractive, not emissive.** Ink absorbs light on a reflective substrate.
  There is no backlight, so no color can exceed the substrate's brightness, and
  the practical contrast ceiling is the paper's white point against the
  densest ink — well below a screen's.
- **sRGB → CMYK-safe.** Saturated sRGB values outside the process gamut —
  notably vivid cyans, oranges, and greens — do not survive conversion. The
  transform group maps them to the nearest in-gamut value; a role whose whole
  signal was its saturation loses that signal silently.
- **Total ink coverage is bounded.** Stacked dark values that a screen renders
  as a rich near-black exceed a press's coverage limit and produce set-off,
  show-through, and a muddy result. Deep neutrals resolve to a controlled
  build, not to four-channel maximum.
- **No backlit-contrast assumptions.** A contrast ratio computed against a
  luminous white is not the ratio the reader experiences under ambient light on
  paper. Print contrast decisions are made against the substrate, not against
  `#ffffff`.

Semantic roles are preserved through all of this. `color-text-danger` still
means danger here; it resolves to a print-safe value that stays distinguishable
from the neutral text role **at reading distance, in ink**, and it carries a
non-color redundancy (weight, rule, label) because a document may be
photocopied or printed monochrome.

## Elevation → rules and whitespace, not shadow

This is the medium's most notable substitution. **Print has no z-axis.** There
is one sheet, one plane, and nothing sits above anything.

The umbrella's elevation tokens therefore do not resolve to a shadow. They
resolve to the two separation mechanisms the plane does have:

- **Rules** — a hairline or heavier stroke that declares a boundary. Increasing
  elevation maps to a more assertive rule (thin → heavy → double), or to a
  filled tint block where the boundary should read as a surface.
- **Whitespace** — increased separation from surrounding content. The higher
  the notional elevation, the more the region is isolated by space.

A drop shadow rendered in ink is a grey smear. It does not communicate depth on
paper; it communicates that a screen design was exported without a transform.

## Mode re-resolution

The umbrella defines three orthogonal token modes. Here is how each behaves.

| Mode axis | Status | Behavior |
|---|---|---|
| **Theme** | **unsupported — collapses** | The medium has one surface. There is no selector, no runtime, and no second contrast target, so the theme axis collapses to a single resolution at typeset time. Consistent with `dark-mode.md` being **dropped** in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/capability_declaration.md" />. |
| **Density** | **supported** | Re-resolves through page margins and leading rather than through padding. A denser mode narrows margins and tightens leading and float separation; a looser mode widens them. The mechanism differs from the web's; the axis is intact. |
| **Locale** | **supported** | Re-resolves normally, and reaches further than on the web: locale drives the typographic defaults (leading, measure, face selection for the script) *and* the page-level mirroring for RTL — gutter side, folio position, running-head alignment, and the recto/verso relationship. |

## Value coercion

The transform group performs these coercions. Each is lossy in a way the author
should know about.

| From | To | Rule |
|---|---|---|
| `px` | `pt` | `1px = 0.75pt` at the 96dpi CSS reference. Applied to any dimension token authored in web units. |
| `hex` / sRGB | print-safe value | Clamp to the process gamut; enforce the total-ink-coverage bound on dark builds. |
| Duration | **discarded** | There is no time axis. A duration token has no emission and produces no output; it is dropped rather than coerced to zero, because a coerced zero would imply an instant transition where there is no transition at all. |
| Shadow / elevation | rule or whitespace | Resolved per [elevation](#elevation--rules-and-whitespace-not-shadow); never emitted as a blur. |

## Testable obligations

- **Every dimension on the page traces to a scale step**, resolved in `mm`,
  `pt`, or `em`. No one-off measurement.
- **Every type size traces to `base-font-size × size`.** No absolute `pt` at a
  call site.
- **No color depends on saturation alone to carry its role.** Each semantic
  color carries a non-color redundancy so the role survives a monochrome print.
- **No visual separation is expressed as a shadow.** Regions are separated by a
  rule, a tint, or whitespace.
- **No duration token has any rendered consequence.** If removing every
  duration token changes the output, the transform group is not discarding
  them.
- **Semantic role names are unchanged from the umbrella.** This profile renames
  nothing.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Dimensions trace to the scale | Measure repeated gaps on the page image; check they cluster on scale steps | A gap sits between two steps with no other instance of that value |
| Type sizes trace to the scale | Divide each measured role size by the style's `base-font-size` | The quotient is not a declared `size:` multiplier |
| Color redundancy | Convert the page image to greyscale | A semantic distinction disappears entirely |
| Ink contrast | Compare the role's ink density against the substrate, not against `#ffffff` | The distinction is only legible under a backlit assumption |
| No shadow | Inspect region boundaries at high zoom | A soft gradient edge appears where a rule or gap belongs |
| Durations discarded | Search the emitted preamble for a duration-derived length | Any exists |

## Anti-patterns

- Emitting a drop shadow as a grey gradient because the source token said
  `elevation-2`. It reads as a printing defect.
- Hard-coding `11pt` at a call site instead of resolving `base-font-size ×
  size`. The document then no longer scales with its style, and the modular
  ratios silently break the first time the base changes.
- Carrying an sRGB accent straight into print and discovering the "distinct"
  status colors are indistinguishable in ink.
- Renaming a semantic role to something print-flavoured
  (`color-ink-danger`). The role contract is the umbrella's; this medium adds a
  transform, not a vocabulary.
- Coercing durations to `0` rather than discarding them, which leaves a
  meaningless zero-length in the emitted preamble and implies a transition axis
  the medium does not have.
- Treating "density" as unsupported because print has no padding token. The
  axis re-resolves through margins and leading; declaring it unsupported
  removes a real capability.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />
