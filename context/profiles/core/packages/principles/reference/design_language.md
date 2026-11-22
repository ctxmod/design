# Design Language

The grammar of consistent, repeated decisions that make an interface feel like one thing — voice, intentional contrast, coherence, and tokens.

A design language is the set of repeated, consistent decisions that make an
interface feel like one thing made by one mind. It is not a logo, a color, or a
font in isolation — it is the *grammar* by which those choices combine. When the
grammar is consistent, a new screen the user has never seen still feels familiar;
when it is inconsistent, even a polished screen feels untrustworthy.

The goal of this profile is to make that grammar explicit so that media and brand
profiles can specialize it without losing coherence.

## A voice emerges from consistency, not decoration

A recognizable design voice is the cumulative effect of applying the same small
set of rules everywhere:

- The **spacing scale** is always drawn from one set of steps (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />).
- The **type scale** uses one ratio and a fixed set of weights (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />).
- **Color** maps meaning to a fixed palette, used the same way every time (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).
- **Motion** uses the same easing and duration bands for the same intents (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).
- **Composition** aligns to the same grid and grouping logic (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />).

Decoration — gradients, shadows, ornament, illustration — is the *least*
durable source of voice. It dates quickly, fights legibility, and is the first
thing an AI reaches for to seem distinctive. A strong voice can survive having
all decoration stripped away because it lives in the systematic choices, not the
surface. Reach for decoration last, and only when it encodes something true about
the subject.

## Consistency vs. intentional contrast

Consistency is the default; contrast is a deliberate exception that earns
attention precisely because everything around it is consistent.

| Situation | Choose |
|-----------|--------|
| Two elements do the same kind of job (two secondary buttons) | Consistency — identical treatment |
| An element must be found first (the primary action) | Contrast — break from the surrounding pattern |
| A region changes meaning (a danger zone, a celebration) | Contrast — but from the *semantic* palette, not an ad-hoc color |
| Repeated list/grid items | Consistency — rhythm makes them scannable |
| The one signature moment of a page | Contrast — spend boldness here, once |

The discipline is: **be consistent by default, and make every break from
consistency a decision you can justify.** Contrast that is everywhere is just
noise; the page has no focal point and the voice dissolves.

## Coherence across surfaces

A design language must hold across many screens, states, and densities, not just
the hero shot:

- **Across screens** — a button on the settings page is the same button as on the
  landing page. Components are contracts (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />), not per-screen reinventions.
- **Across states** — empty, loading, error, and success states share the voice.
  A polished happy path with a generic error screen breaks coherence (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />).
- **Across themes** — light and dark are two expressions of one language, not an
  inversion. The same semantic roles carry the same meaning in both (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).
- **Across densities** — a comfortable form and a dense data table still read as
  the same product because they draw from the same scales.

## The role of tokens

Tokens are how a design language becomes portable. Instead of repeating literal
values, every component references a named step in a scale (`space-4`,
`text-lg`, `color-accent`). This makes the language:

- **Consistent** — there is exactly one source for each value.
- **Themable** — swapping the token values reskins the whole system.
- **Brand-swappable** — a brand profile populates primitives while the umbrella
  defines the semantic contract (see the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />).

The umbrella profile owns the *semantic* layer of the design language (what a
token means: "this is the accent action color"); brand profiles own the
*primitive* layer (which exact value it resolves to). See the rule on
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/rules/token_usage.md" />.

## Principles over decoration — the through-line

Every other document in this folder is an application of one idea: **a design
language is principled.** Hierarchy, color, type, spacing, motion, and
composition are not independent aesthetic preferences; they are levers a designer
pulls in service of clarity and identity. When uncertain, restrain (see the rule
on <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/rules/aesthetic_discipline.md" />). The
system's coherence beats any local cleverness.

## Rule Companion: Aesthetic Discipline — Full Rule Set and Rationale

*Companion to the `aesthetic_discipline` rule: its full rule set, worked examples and rationale.*

### The rules

- **Hierarchy over decoration.** A clear order of importance does more for a design
  than any gradient, shadow, or ornament. Solve hierarchy first; reach for
  decoration last, and only when it encodes something true (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />).
- **One focal point per view.** Decide the single most important element and give
  it the most contrast; pull contrast *out* of everything else to make room.
  Multiple "primary" things cancel each other out.
- **Spend boldness once.** Let one signature element be the memorable thing and
  keep everything around it quiet. Boldness everywhere is just noise.
- **Reduce before adding.** Before shipping, remove one element — a divider, a
  color, a weight, an animation. If nothing breaks, it wasn't earning its place.
- **Consistency beats local cleverness.** A clever one-off that breaks the system's
  patterns weakens the whole. The coherence of the design language is worth more
  than any single screen's flourish.
- **Match complexity to the vision, then execute fully.** Minimal directions need
  precision in spacing, type, and detail; maximal directions need complete
  execution. Elegance is doing the chosen thing well — not adding more.

### Why

Restraint is what makes a design read as *intentional* rather than assembled or
auto-generated. Every element that doesn't carry meaning competes with the ones
that do, flattening hierarchy and diluting the voice. Cutting is the most reliable
way to improve a design, and the hardest discipline to keep.

When the call is genuinely unclear, choose the quieter option. You can always add;
removing after the fact is rarer and harder.

### Why this is a usability lever, not vanity

Aesthetic discipline is an engineering decision, not decoration. The evidence:

- **Aesthetic-usability effect** (Kurosu & Kashimura, 1995). Users perceive
  attractive interfaces as more usable — even when two interfaces are functionally
  identical. Perceived usability tracks craft, not just function.
- **Processing fluency** (CHI 2023). Interfaces that are easier to process visually
  are judged more trustworthy and more usable. Fluency is driven by consistency,
  clarity, and low extraneous load — exactly the levers above.

Craft and consistency improve both *perceived* and *actual* usability. Treat them
as part of the product's function, not as a coat of paint applied at the end.

### Quality = consistency + constraint

- The discipline is **not "add polish."** It is "hold a system of consistent
  constraints" (Stripe). Polish that violates the system is regression, not quality.
- Treat every aesthetic decision as a **reviewable engineering decision** (Vercel
  design-engineer culture): it has a stated rationale, and it is reversible and
  tracked. If you cannot say *why* a value is what it is, it is not yet a decision.

### Over-systematization guard (T10)

This guard is load-bearing. Abstraction that is not used or enforced is cost, not
value.

> Introduce a token layer, principle, or abstraction only when you can document AND
> maintain it. Before adding a new token, principle, or layer, answer three
> questions: (1) Who owns it? (2) How is it verified? (3) What anti-pattern does it
> prevent? If you cannot answer all three, do not add it.

- A token system can be a liability: **5,000 tokens covering 2% of the CSS surface**
  is granular enough to slow delivery while enforcing nothing.
- Prefer fewer constraints that are enforced over many that are aspirational.
- When in doubt, do not abstract. Inline the value and wait for the third
  repetition before extracting a token or principle.
