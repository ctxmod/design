# Design stack

The design module's `core` profile is the umbrella tier of the user-facing-surface
design stack: framework-agnostic design principles, visual language, and an
abstract component taxonomy that medium profiles (`web`, `documents`, and future
ones such as `ios` or `cli`) and brand profiles specialize. This profile defines
the *why* of good visual design — its principles, its visual language, and an
abstract, platform-agnostic component taxonomy — without committing to any
framework, platform, or brand.

It is deliberately upstream of plumbing. Framework wiring (React, Tailwind,
shadcn, CSS variables) belongs to the frontend-framework modules (`github.com/ctxmod/typescript/context`). Concrete pixels, breakpoints,
and platform affordances belong to *medium* profiles (`web`, `ios`,
…). Concrete palettes, type, and motion belong to *brand* profiles. This profile
gives all of them a shared vocabulary and a quality bar.

## Three-tier architecture

```
core                   ← this profile: principles + abstract component taxonomy
  └── web               ← medium: web-specific concretization (DOM, CSS, breakpoints)
        └── brand_<b>   ← brand: concrete palette, type, motion, signature
```

Each tier specializes the one above it. A brand profile fills the abstract
component *slots* defined here (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />)
with concrete styling; a medium profile maps the slots onto a platform's
primitives.

Token delivery is single-source → multi-target: the semantic contract emits to
each medium via transform groups (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />).

## What lives here

- **Principles** (the `principles` package) —
  visual hierarchy, color, typography, spacing, motion, composition, design
  language, and accessibility-as-quality. The reasoning a designer applies.
- **Component taxonomy** (the `components` package) —
  named, platform-agnostic component contracts (buttons, inputs, cards,
  navigation, feedback, data-display, layout-containers) with their variants,
  states, and responsibilities. Lower tiers reference these by path.
- **Procedures** (the `process` package) —
  process: design review, the token model, design briefs, information
  architecture, and the medium charter.
- **Rules** (`aesthetic_discipline` in `principles`, `token_usage` in
  `process`) — short guardrails on aesthetic discipline and token usage.
- **Foundations** (the `foundations` package) — this stack description and
  the glossary.

## What does NOT live here

- CSS variables, Tailwind config, shadcn registry — see the `shadcn` profile of `github.com/ctxmod/typescript/context`.
- Breakpoints, viewport units, DOM semantics — see `web`.
- Concrete hex palettes, chosen typefaces, motion timings — see brand profiles.

## Principle formulation

Every principle file in the `principles` package follows one shape so that any two agents (or humans) interpret a principle identically:

1. **Abstract name** — medium-neutral noun(s), no platform references.
2. **What + why** — one paragraph; name the perceptual/cognitive mechanism where known (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />).
3. **Testable obligations** — imperative bullets a reviewer can check as met/not-met.
4. **How to verify** — one concrete check per obligation (a named test, a threshold, a spec section).
5. **Anti-patterns** — concrete violations.

Where a principle is genuinely a continuum (density, containment), add a sixth **tunable dimension** section naming the poles. Most principles are binary and should omit it.

## Foundation: ISO 9241-110

The umbrella's medium-agnostic invariants are **ISO 9241-110:2020's seven dialogue principles**: suitability for the task, self-descriptiveness, conformity with user expectations, suitability for learning, suitability for individualization, error tolerance, and controllability. These apply to *any* human-facing interactive system — web, CLI, native app, print — and the design principles in this profile concretize them for visual/aesthetic surface design. Every principle file should be traceable to one or more of these invariants.

## Medium Profile Charter

Every `<medium>` profile (`web`, `ios`, `cli`,
`latex`, …) **must conform** to the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/medium_charter.md" />. The
charter fixes the five sections a medium must declare — capability declaration,
slot mapping, token translation, affordance adaptation, and a confidence note —
so a new medium drops in by filling the template rather than rewriting this
umbrella. `web` is validated as a conforming instance in the charter's
acceptance test.

## Glossary

Load-bearing terms are defined once in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />. Profiles reuse that vocabulary without redefining.

### Known omissions / deferred

- **Privacy** is intentionally out of scope for now — surfaced only by Diehl et al. (2022) on a low evidence base, it is a deferral, not a gap to fill.
- **Emotional component** is likewise intentionally omitted for now — also raised only by Diehl et al. (2022) on a low evidence base, so it is deferred rather than treated as missing.
