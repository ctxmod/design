# Component Taxonomy

Index of the abstract component taxonomy — the slot concept, the three-tier indirection, how to read a slot file, and the relationship to the principles.

This is the index of the abstract component taxonomy — the named, platform-agnostic
component *contracts* that make up a user-facing surface. It is the map; each entry
links to a detail file that specifies that component's purpose, variants, states,
and responsibilities.

## The slot concept

A **slot** is a named component contract defined independently of any platform or
brand. It specifies *what a component is for* and *what it must support* — its
variants, its states, its responsibilities — but not how it looks or how it is
built.

```
slot (here)            →  medium (web)               →  brand
"a button is the           "rendered as <button>,         "primary = teal accent,
 action-invocation          focus ring via :focus-         radius 8px, 150ms press,
 component with these        visible, ≥44px target"         shadow on hover"
 variants and states"
```

This indirection is the whole point of the three-tier architecture:

- The **umbrella** (this folder) owns the *contract*: a button has a primary
  variant; an input has an error state; a toast has a severity. These are
  invariant across platforms and brands.
- A **medium** profile maps each slot onto a platform's primitives and
  affordances.
- A **brand** profile fills the contract with concrete styling: which color the
  primary variant is, what the radius is, how the press feels.

Because the contract is stable, a brand profile can reference
`components/buttons.md` (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />) by path and know exactly which variants and
states it must provide a look for — and a medium profile can map the same set onto
its platform. Get the slot definitions precise and complete, and the lower tiers
have an unambiguous target.

## Three layers

The seven slots below are the **component layer**. They sit between two adjacent
layers that this profile does not own but must be positioned against — naming
them resolves the recurring atomic-vs-compound boundary debate.

- **Headless primitives (below)** — behavior and accessibility with no styling:
  roles, states, keyboard semantics, focus management. This is the layer
  [Open UI](https://open-ui.org/) and the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/)
  own. The taxonomy *references* this layer for the underlying interaction
  semantics of a slot; it does not re-define it here.
- **Component layer (this profile — the seven slots)** — the named,
  platform-agnostic component *contracts*: buttons, inputs, cards, navigation,
  feedback, data-display, layout-containers, each with its variants, states, and
  responsibilities. This is the layer brands specialize and mediums map. It is
  the only layer this umbrella owns.
- **Patterns / compositions (above)** — recurring assemblies built *from* slots:
  forms, master-detail, data-table-with-filters, page templates and shells. These
  are not new slots; they are arrangements of existing ones. The umbrella names
  the *concept* of a pattern, but the concrete patterns are composed from slots
  and typically live at the **medium** tier (a medium knows which slots its
  platform offers and how they assemble).

Ownership, stated plainly: the umbrella owns the **component-layer contract**;
primitives are **referenced** (APG / Open UI), not specified here; patterns are
**composed** from slots and generally belong to the medium tier. A slot is the
unit of contract — anything smaller is a referenced primitive, anything larger is
a composition.

## Canonical vocabulary

Within the component layer, slot names and role semantics are anchored to two
external registries so brand and medium agents inherit settled vocabulary instead
of improvising it:

- **[Open UI](https://open-ui.org/) is the canonical component-*name* registry.**
  When a concept has competing synonyms (accordion / collapsible / disclosure;
  dropdown / select / combobox), Open UI's component name is the single term this
  taxonomy adopts, resolving the "what is this thing called" ambiguity.
- **The [ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/patterns/)
  is the normative role / state / property / keyboard contract** per pattern. When
  a slot asks "what *is* a button, where is its boundary, what must it announce,"
  the matching APG pattern is the authority — its role, required states, and
  keyboard interaction model are inherited, not re-derived.

Per slot, brand and medium agents inherit the canonical Open UI name plus the APG
pattern for that slot's role semantics rather than inventing either. This keeps
slots **platform-agnostic**: Open UI and APG supply *names and role semantics*;
the medium tier supplies rendering. Each slot file names its canonical term and
links its APG pattern near the top.

## How to read a slot file

Each component file follows the same shape:

- **Purpose** — the one job this component does, and how it differs from adjacent
  slots.
- **Variants** — the meaningful kinds of the component (semantic, not stylistic).
- **States** — the conditions the component must visually express.
- **Responsibilities / contract** — what any implementation must guarantee
  (accessibility, feedback, content rules).
- **Anti-patterns** — common ways the slot is misused.

States and accessibility are not optional sections — a slot is only "complete"
when every state is designed (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).

### Universal interaction-state contract

"Every state is designed" is not left to each slot's discretion. Every
*interactive* slot draws from one normative interaction-state set:

**default · hover · focus-visible · active/pressed · disabled · loading · error**

A slot is incomplete until every *applicable* member of this set is designed.
Some members are medium-conditional — hover is absent on touch-only mediums, and
the cli medium drops hover/focus-visible — so a medium declares which it honors in its
capability declaration. The full contract, the medium-conditional rules, and the
parallel **five content states** (blank/empty · loading · partial · error · ideal)
every data surface must design live in component states (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/states.md" />).

## The slots

### Action & input

- **Buttons (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />)** — the action-invocation slot. Triggers an operation.
  Variants by emphasis and intent; full interaction-state contract.
- **Inputs (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />)** — the data-entry slots. Text, textarea, select,
  checkbox, radio, slider. Label / helper / error contract and validation
  feedback.

### Structure & grouping

- **Cards (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" />)** — the container/grouping slot. Bundles related content
  into a unit with an optional header/body/footer contract; static or interactive.
- **Layout containers (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" />)** — the structural slots. Page
  shells, sidebars, headers, modals, drawers, content-width regions. The skeleton
  everything else sits in.

### Wayfinding

- **Navigation (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />)** — the wayfinding slots. Primary nav, tabs,
  breadcrumbs, pagination, menus. Active-state and hierarchy contract.

### Communication

- **Feedback (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />)** — the status/communication slots. Toasts, alerts,
  banners, inline validation, loading/progress, empty states. Severity,
  dismissibility, and persistence contract.

### Reading

- **Data display (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />)** — the read-heavy slots. Tables, lists,
  key-value/description pairs, badges/tags, avatars. Density, sorting/filtering,
  and empty/loading contract.

## Relationship to the principles

Components are where the principles become concrete:

- Their variants and states are an exercise in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />
  and <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> (one primary action; semantic status colors).
- Their spacing and sizing draw from the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />.
- Their transitions follow <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" /> (feedback, not decoration).
- Every state and label is an <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />
  obligation.

A brand may add components beyond this taxonomy, but every component here is a slot
it is expected to be able to fill.
