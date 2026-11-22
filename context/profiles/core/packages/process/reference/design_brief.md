# Design Brief

Capturing intent before pixels — problem, solution, experience principles, target feel, tasks, constraints, inventory, and success criteria.

A design brief captures **intent before pixels**. It is the short, shared document
that records what is being built, for whom, what it must feel like, and how you'll
know it succeeded — so that every later decision (tokens, components, layout) can be
checked against it. Building without a brief is how a design drifts into generic
defaults: with no stated intent, every fork resolves to the safest, most templated
option.

This is a process artifact. Write it before
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/information_architecture.md" /> and before generating
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />.

## When to write one

- Starting a new product, page, feature, or flow.
- Reshaping an existing surface where the direction is unclear.
- Any time you notice yourself about to "just start building" a non-trivial UI.

## How to produce it

1. **Get a real description** — what is being built, who uses it, and any
   constraints or references the stakeholder already has.
2. **Explore the existing codebase / system** — current tokens, components, fonts,
   patterns. The brief should *extend* what exists, not ignore it. Treat existing
   components as the starting vocabulary.
3. **Interview relentlessly** — walk every branch of the decision tree, resolving
   dependencies one at a time, and offer a recommended answer for each question
   rather than just asking. Pin down anything left vague; if the brief doesn't name
   the subject, audience, and the page's single job, name them yourself and say so.
4. **Write the brief** using the structure below, then **review it against the
   defaults**: for any section that reads like the generic answer you'd give for
   *any* similar product, revise it into a choice made for *this* one, and note what
   you changed.

## What a brief captures

### Problem
The human friction, from the user's perspective — not a feature list, not business
metrics. What is hard right now?

### Solution
What this interface does about it, described as an *experience* rather than a spec.

### Experience principles (max 3)
Three guiding principles, each resolving a real tension (e.g. "progressive
disclosure over upfront power", "confidence over speed"). These are the tie-breakers
for every later decision; keep them few and sharp.

### Target feel (aesthetic direction)
- **Tone** — the emotional register (calm, urgent, playful, authoritative, warm,
  clinical). One word or two.
- **Aesthetic position** — a one-sentence anchor ("X meets Y") that eliminates
  whole classes of bad choices downstream.
- **Reference points** — products/sites/styles this should feel like.
- **Anti-references** — what it must *not* feel like (often more clarifying than
  the references). Explicitly rule out the generic-AI defaults if relevant.

This direction is what later feeds the brand profile's primitives (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />) and the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />.

### Brand constraints
Hard brand rules the design must respect: existing palette, required typefaces,
logo usage, voice/tone guidelines, legal/accessibility floors.

### Key user tasks (JTBD)
The jobs the user is hiring this interface to do, ranked by frequency. This drives
the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/information_architecture.md" /> and the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" /> (the most frequent
task gets the most prominence).

### Hard constraints
Devices, performance budget, accessibility requirements (target WCAG level —
contrast, keyboard, focus; see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />),
framework/platform limits.

### Content reality
What content is real vs. placeholder. Copy is design material; generic copy makes a
design feel as templated as generic visuals. Note who writes the real words.

### Component inventory
The components this needs, each marked *exists / modify / new*, mapped to the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" /> slots. Reuse
before inventing.

### Success criteria
How you'll know the design worked — observable outcomes ("a new user completes
setup without help", "the primary action is found in under N seconds"), not "looks
nice". These become the bar the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_review.md" /> measures against.

### Out of scope
What this brief explicitly does *not* cover. Naming this up front prevents scope
creep during the build.

## Quality bar for the brief

- It commits to specifics — a real subject, audience, tone, and references — not
  hedged generalities.
- Every section survives the "would I write this for any product?" test.
- It is short enough to actually be read before building.

The brief is the contract the whole design flow checks itself against: IA, tokens,
build, and review all refer back to it.
