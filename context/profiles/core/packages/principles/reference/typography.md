# Typography

Typography for readability and identity — modular type scale, font pairing, weight, optical sizing, leading, measure, and variable fonts.

Typography is the most load-bearing decision in UI design. It carries the bulk of
the content, sets the largest share of the page's personality, and determines
whether the interface is comfortable to read. Type does two jobs at once —
**readability** (can the user absorb the content with ease?) and **identity**
(does the type treatment feel like this product?) — and a good system serves both
without sacrificing either.

The implementation details (loading fonts, `font-display`, variable-font axes in
CSS) belong to the medium tier. This document is about the principles.

Readability is not a matter of taste. Reading speed, comprehension, and fixation
recovery respond to measurable parameters — body size, measure, leading, and the
metric properties of the face itself. The obligations below state those as
empirical **targets with rationale**, not soft preferences.

> **Media calibrate the numbers.** Every threshold here is a web/print default
> tuned for screen reading at arm's length (~50–70 cm). A different medium shifts
> them: a terminal renders fixed-pitch cells where "measure" is a column count and
> "size" is a font-cell choice; print at reading distance tolerates slightly
> smaller body copy; signage at distance demands far larger type and looser
> tracking. Treat the figures as the umbrella default and let a medium-tier
> profile (e.g. a CLI/terminal profile) restate them in its own units.

## The type scale

A type scale is a fixed, ordered set of sizes used everywhere. Arbitrary,
one-off sizes are the typographic equivalent of magic numbers (see the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/rules/token_usage.md" />).

- Build the scale from a **modular ratio**: each step is the previous size
  multiplied by a constant. Common ratios:

| Ratio | Name | Feel |
|-------|------|------|
| 1.125 | Major second | Tight, dense, utilitarian (data-heavy UIs) |
| 1.200 | Minor third | Balanced, general-purpose |
| 1.250 | Major third | Comfortable, editorial |
| 1.333 | Perfect fourth | Dramatic, marketing/landing |
| 1.500 | Perfect fifth | Bold display contrast |

- A larger ratio yields **more dramatic contrast** between heading and body; a
  smaller ratio yields a calmer, denser hierarchy. Pick the ratio from the design
  language, not per-screen.
- Map scale steps to roles: display, h1–h4, body, small, caption, overline. Use
  the role, never the raw size, at call sites.
- For real **hierarchy**, jumps must be perceptible. A 16px body next to an 18px
  heading reads as a mistake; the heading needs a clear step up (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />).

## Body size floor

Body copy has a hard floor: **≥ 16px (1rem)**. This is the screen-reading default,
not a maximum — long-form reading often benefits from 17–18px. Below roughly **8pt
(~11px)** reading speed measurably degrades and fixation duration climbs; small UI
text (captions, labels) may drop toward ~13–14px but body running text should not.
The floor is an *apparent*-size floor, not a nominal one: a face with a small
x-height needs to be set larger to clear the same legibility bar (see
[x-height and apparent size](#x-height-and-apparent-size)).

## Font pairing

A common, durable pattern is a **display face** for headings paired with a
**body face** for text, optionally a **utility/mono face** for data and captions.

- **Contrast pairs well.** A characterful display (high-contrast serif, geometric
  sans, condensed grotesque) against a quiet, highly-legible body sans creates
  interest without compromising reading.
- **One family for everything is safe but flat.** It reads as undesigned. If you
  use a single superfamily, exploit its weights and optical sizes to manufacture
  contrast.
- **Avoid invisible defaults.** Generic system stacks (the usual ubiquitous sans)
  carry no identity. Choose deliberately; the choice is a major part of the
  voice (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />).
- **Body faces must be workhorses.** A display face used for body text is a
  legibility error. Reserve characterful faces for short, large text.

### Judge a body face on metrics, not taste

"Pick a good font" is not actionable, and the stakes are real: typeface choice
alone moves silent-reading speed by **roughly 30–70 WPM** across common screen
faces (ACM CHI 2022, *Towards Individuated Reading Experiences*). Specify the
*metrics* the choice is judged on, so the decision is reviewable:

- **x-height fraction** — taller x-height reads smaller text better (see below).
- **Aperture** — open apertures (the gap in `c`, `e`, `a`, `s`) resist closing up
  at small sizes and low resolution; closed apertures blur into one another.
- **Weight / stroke contrast** — low, even stroke contrast holds up at body sizes;
  high-contrast (thick/thin) faces thin out and shimmer when small.
- **Letterfit and disambiguation** — generous spacing and distinct `I l 1 / O 0`
  forms reduce misreads, which matters most in data and code.

Identity is chosen on top of these floors, not instead of them.

## x-height and apparent size

Two faces set at the same nominal px can look noticeably different in size because
**apparent size is driven by x-height**, not the em. A high x-height face (x-height
~52–55% of the em or more) reads larger and stays legible smaller; a low x-height
face (~45% or less) looks small and needs to be set larger to match. Size body
text by *apparent* size — set two candidate faces side by side at the same px and
match their lowercase height, then choose the actual px from there — rather than
trusting the nominal value.

## Weight and optical sizing

- Use **weight for hierarchy**, not for ambient emphasis. Reserve bold for things
  that are genuinely more important; bolding everything erases hierarchy.
- For drama, use the **extremes** of a family (e.g. 300 vs. 700) rather than
  adjacent weights (400 vs. 500), which barely differ.
- **Optical sizing**: display type wants tighter letterspacing and tighter
  leading; body type wants looser tracking and more leading. Faces with an
  optical-size axis adjust contrast and spacing automatically across sizes — use
  it.

## Line height (leading)

Leading is the vertical space a line occupies relative to its size, expressed as a
unitless ratio (`line-height / font-size`). Target **1.4–1.6 for body text**;
display and large headings go tighter (down to ~1.0–1.2) because big type needs
little leading and loose leading fragments a headline. Wider measures and lighter
weights want the upper end of the body band; dense data tables sit just below it.

| Role | Line height | Why |
|------|-------------|-----|
| Display / large headings | 1.0–1.2 | Big type needs little leading; loose leading fragments a headline |
| Subheadings | 1.2–1.3 | |
| Body text | 1.4–1.6 | The comfortable reading band; too tight crowds descenders, too loose disconnects lines |
| Dense UI / data | 1.3–1.45 | Tighter for scanning rows |

Leading and the type scale are linked to the spacing scale — vertical rhythm comes
from aligning line boxes and gaps to a shared base unit (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />).

## Measure (line length)

The **measure** is the number of characters per line (CPL), counting letters and
spaces. For sustained reading, target **50–75 CPL** (66 is the classic optimum);
**45–75** is the acceptable band. Below ~45 the eye returns to a new line too
often and the rhythm breaks; above ~75 the return sweep overshoots and the eye
loses its place. Constrain reading columns with a `max-width` tied to the measure
(roughly `60ch`–`75ch`), not to the viewport.

## Variable fonts

Variable fonts expose continuous axes (weight, width, optical size, slant) in a
single file. They let a system:

- Use precisely-tuned weights instead of the coarse 100-step ladder.
- Animate weight or width for emphasis and state changes (sparingly — see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).
- Reduce loaded font files, improving the readability of the *first paint* (no
  fallback-flash reflow). Delivery specifics belong to the medium tier.

## How to verify

Each obligation above is checkable against a rendered page or token set. Run these
at the medium's own units (for screen, computed CSS px / ratios; for terminal,
cell counts / font-cell size):

| Check | Method | Flag when |
|-------|--------|-----------|
| Body size floor | Read the smallest *running-body* computed size | `< 16px` for body; `< ~13px` for captions/labels |
| Measure | Count characters on a full line at the content `max-width` (≈ content-width-px ÷ avg-glyph-advance) | outside `45–75` CPL; ideally outside `50–75` |
| Line-height | Compute `line-height ÷ font-size` for body | outside `1.4–1.6` for body; headings outside their row band |
| Apparent size | Set the two candidate faces at the same px, compare lowercase x-height | the chosen face's x-height clears the legibility bar only when set ≥ floor |
| Face metrics | Confirm the body face was chosen on x-height / aperture / weight-contrast, not taste | selection rationale cites none of these metrics |

These are the web/print defaults. A medium profile restates the thresholds in its
units — a terminal profile, for instance, replaces "≥16px body" with a minimum
font-cell and "50–75 CPL" with a target column width in cells — and overrides this
table rather than ignoring it.

## Readability + identity together

The two jobs are not in tension if you assign them to the right places:

- **Identity lives in the large, short text** — the display headings, the brand
  wordmark moments, the one signature treatment. Spend personality here.
- **Readability lives in the long, small text** — body copy, form labels, table
  cells. Keep these quiet, legible, and conventional.

A page that puts personality into its body font and neutrality into its headings
has it backwards: it is both hard to read and forgettable. Put the boldness where
it is read briefly and the calm where it is read at length.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
