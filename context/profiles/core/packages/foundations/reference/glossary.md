# Design Glossary

Load-bearing vocabulary for the design profile family — terms defined exactly once so all profiles share a precise language.

This glossary is the single source of truth for terminology across the design
profile family. When a term appears in a principle or rule, it carries the
meaning defined here.

## Terms

**medium** — The surface/runtime a profile targets (web, iOS, CLI, LaTeX,
Android, Windows). The medium determines available affordances and how abstract
tokens translate into concrete platform values.

**brand** — A named visual identity that extends a medium profile and supplies
concrete token values plus per-component styling. A brand is the *only* tier
that owns raw primitive values; a medium is the runtime, a brand is the look.

**slot** — A named, platform-agnostic component contract (button, input, card,
…). A medium maps each slot onto a platform primitive; a brand specializes the
slot's appearance. The slot itself names a responsibility, not an
implementation.

**principle** — A medium-agnostic design rule stated as an abstract name plus a
set of testable obligations. A principle says *what must hold*, never *how a
given medium achieves it*.

**focal point** — The single element a view directs attention to. A view has
exactly one focal point and at most one primary action; competing focal points
mean no focal point.

**density** — Information-per-area, expressed as a tunable mode
(compact/comfortable/spacious) matched to user expertise and the medium.
Density is a setting, not a fixed property of a layout.

**elevation** — The perceived layering / z-order of a surface. It is *perceived*
depth, expressed via shadow, surface-step, or border depending on medium and
mode — not a literal z-index value.

**token** — An abstract, named design decision: a value paired with a role. A
token is the decision, not its encoding; a CSS variable is one *implementation*
of a token, not the token itself.

**primitive / semantic / component token** — The three token layers. Primitives
are raw values owned by the *brand*. Semantic tokens are role names owned by the
*umbrella contract* and resolve to primitives. Component tokens are slot-bound
values that resolve to semantic tokens. Resolution flows component → semantic →
primitive; ownership never inverts.

**mode** — An orthogonal axis (theme, density, locale) over which semantic →
primitive mappings re-resolve. A mode re-points existing layers; it is *not* a
fourth token layer.

**obligation** — A testable, imperative statement a reviewer can check
(pass/fail). Obligations are the checkable half of a principle and follow the
principle-formulation convention (C2).

**affordance** — How a user acts on a surface
(pointer / touch / keyboard / screen-reader / text). Affordances are declared
per medium, because each medium offers a different action repertoire.

**capability declaration** — A medium profile's per-principle classification of
each umbrella invariant as *supported*, *adapted*, or *dropped*. It records how
faithfully the medium can honor each principle.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/medium_charter.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />
