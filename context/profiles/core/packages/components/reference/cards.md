# Cards

The container/grouping slot — header/body/footer contract, interactive vs. static, states, density variants, and responsibilities.

The **container / grouping slot**. A card bundles related content into a single,
bounded unit so the eye reads it as one thing. It is the workhorse of grouping in
modern UI — a way to apply the Gestalt principle of *common region* (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />) to make a collection of disparate pieces (a
title, an image, some text, an action) cohere. Part of the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

**Canonical name:** a card is a *pattern over a grouping element, not a primitive*
— Open UI has no single `card` component. Its role semantics come from a grouping
container: ARIA [`group`](https://www.w3.org/WAI/ARIA/apg/) or a `section` with an
accessible name (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />).

## Purpose and when to use

Use a card when a set of elements belong together and should be perceived,
scanned, and possibly acted on as a unit — a product, an article preview, a
setting group, a dashboard metric.

Do *not* reach for a card by reflex. Cards are over-used: wrapping every region in
a bordered box creates visual noise and competing boundaries. Often **whitespace
alone** groups things more elegantly than a card border (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />). Use a card when the grouping needs a hard
boundary or the unit is repeated in a collection; otherwise prefer space.

## The header / body / footer contract

A card is a compositional contract with up to three regions, each optional:

- **Header** — identity of the card: a title, optional eyebrow/category, optional
  media (image/icon), optional header-level action (overflow menu). Establishes
  what the card *is*.
- **Body** — the primary content: text, stats, fields, a chart. The reason the card
  exists.
- **Footer** — actions and metadata: buttons (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />),
  timestamps, status. The "what can I do / what should I know" region.

The contract is *which regions exist and in what order*, not their styling. A
collection of cards must use the regions **consistently** — every card in a grid
places its title, media, and actions in the same slots so the collection scans as a
rhythm (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />).

## Interactive vs. static

A fundamental fork that changes the card's responsibilities:

- **Static card** — a presentation container. It groups content but isn't itself
  clickable. Actions inside it (buttons, links) are the interactive parts.
- **Interactive card** — the *whole card* is a target (clicking it navigates or
  selects). This card must behave like a control:
  - It needs hover, focus, active, and (if selectable) selected states.
  - It needs a visible focus indicator and keyboard operability (see
    <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
  - **Nested-action conflict**: when a whole-card target *also* contains buttons or
    links, the inner controls must remain independently operable and the click
    targets must not overlap ambiguously. This is the classic card pitfall —
    resolve it deliberately (a primary card action plus clearly separated inner
    controls), don't nest a button inside a clickable card by accident.

Make the interactive-vs-static choice explicit; an ambiguous card (looks
clickable, isn't — or vice versa) frustrates users.

## States

| State | Applies to | Communicates |
|-------|-----------|--------------|
| **Default** | all | Resting presentation |
| **Hover** | interactive | The card is a target (subtle lift/highlight) |
| **Focus** | interactive | Keyboard focus, visible ring |
| **Active/pressed** | interactive | The click registered |
| **Selected** | selectable | This card is chosen (in a multi/single-select set) |
| **Loading / skeleton** | collections | Content is arriving — show a skeleton matching the card's shape |
| **Empty** | data cards | No content yet — a meaningful empty state, not a blank box (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />) |
| **Disabled** | interactive | Not selectable now |

Skeleton states matter for card grids: a skeleton that matches the final layout
prevents jarring reflow when data loads (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

## Density variants

Cards support density levels to suit context (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />):

- **Comfortable** — generous padding; for spacious, focused layouts and marketing.
- **Compact** — reduced padding; for dense dashboards and lists of many cards.

Density is a systematic token swap, not per-card tweaking. Within one collection,
all cards share a density.

## Responsibilities

- **Group genuinely related content** — a card asserts "these belong together"; the
  assertion must be true.
- **Consistent region usage** across a collection.
- **One clear action hierarchy** inside the card — a single primary action at most
  (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />).
- **Resolve the interactive/static choice** and, if interactive, provide the full
  control state set and keyboard support.
- **Boundaries earn their keep** — a border/shadow is justified only if it groups
  something space cannot; otherwise drop it.

## Anti-patterns

- Wrapping everything in cards until the page is a grid of boxes with no hierarchy.
- A clickable card that swallows or conflicts with its inner buttons/links.
- Cards in a collection that place title/media/actions inconsistently.
- A card with two competing primary actions.
- A loading state that pops content in and reflows the grid (use a matching
  skeleton).
- A heavy border/shadow used where whitespace alone would group better.
