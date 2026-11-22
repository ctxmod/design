# Buttons

The action-invocation slot — buttons vs. links, emphasis/intent variants, sizing contract, full state set, and responsibilities.

The **action-invocation slot**. A button triggers an operation: submit a form,
open a dialog, delete a record, advance a flow. Its entire job is to be findable as
an action and to communicate, at every moment, whether it is available, being
pressed, or working. Part of the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

**Canonical name:** Open UI [`button`](https://open-ui.org/components/button.research/);
role/state/keyboard semantics follow the ARIA APG [button pattern](https://www.w3.org/WAI/ARIA/apg/patterns/button/)
(see canonical vocabulary (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />, section `#canonical-vocabulary`)).

## Buttons vs. links

These are different slots and must not be confused:

- A **button** performs an *action* — it changes state, submits, or triggers
  something. It is the right slot when "what happens" is an operation.
- A **link** performs *navigation* — it takes the user somewhere. It is the right
  slot when "what happens" is a location change, and it should behave like a
  destination (openable in a new tab, has an address).

Styling one as the other (a link that looks like a button is fine; a link that
*acts* like an action, or a button used purely to navigate) breaks expectations
and accessibility. Choose the slot by behavior, then style to taste.

## Variants

Variants are by **emphasis** (how much visual weight) and **intent** (what kind of
action). They are semantic, not arbitrary skins.

| Variant | Emphasis | Use |
|---------|----------|-----|
| **Primary** | Highest | The single most important action in a context. One per view (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />) |
| **Secondary** | Medium | Important but not the main action; sits beside primary |
| **Ghost / tertiary** | Low | Low-stakes or repeated actions; minimal visual weight |
| **Danger / destructive** | Intent override | Irreversible or harmful actions; carries the danger semantic color (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />) |
| **Link-style** | Lowest | An action that should read as inline text |

Rules:

- **One primary per context.** Multiple primaries destroy hierarchy; demote all
  but the true main action.
- **Danger is an intent, layerable on emphasis.** A destructive action is usually
  styled as danger regardless of where it sits; high-stakes destructive actions
  also warrant a confirmation step (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />).
- Variants come from the design system, not per-screen invention.

## Sizing contract

A button supports a small set of sizes (e.g. small / medium / large). The contract:

- Sizes scale **padding and type together** so the text-to-edge proportion stays
  constant across sizes (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />).
- The interactive target stays **≥ 44px** even for visually small buttons — pad the
  hit area, don't shrink it (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
- Icon-only buttons must carry an accessible name and meet the same target size.
- A full-width sizing option exists for mobile and stacked contexts.

## States

Every button must visually express its full state set. A button missing states is
incomplete.

| State | Must communicate |
|-------|------------------|
| **Default** | This is an action, available now |
| **Hover** | This is interactive (pointer devices) — subtle, instant feedback |
| **Focus** | Keyboard focus — a clearly visible focus ring (≥ 3:1 contrast). Never suppressed |
| **Active / pressed** | The press registered — immediate, tactile feedback |
| **Disabled** | Not available now, and *why* should be discoverable (tooltip/helper). Not focusable as an action, but reduced contrast must not make it invisible |
| **Loading** | The action is in progress — replace or augment the label with a spinner, keep the button's width stable, and prevent double-submit |

Notes:

- **Distinguish disabled from loading.** Disabled = can't act yet; loading = acting
  now. They look and behave differently.
- Hover and active feedback should be **fast** (instant band) — a sluggish press
  feels broken (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).
- Don't rely on color alone for disabled/danger; pair with shape, position, or icon
  (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).

## Responsibilities

Any button implementation must guarantee:

- **A clear, action-named label** — say what happens ("Save changes", "Delete",
  "Publish"), not "Submit" or "OK". The label stays consistent through the flow
  (the "Publish" button yields a "Published" confirmation).
- **Immediate feedback** on every interaction (hover/press/focus) and on the
  *result* (loading → success/error via <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />).
- **Keyboard operability** — activatable by keyboard, with visible focus and
  correct focus order.
- **Stable layout** — the button does not resize when its label changes to a
  loading or success state.

## Anti-patterns

- Several "primary" buttons competing in one view.
- Disabled buttons with no explanation of how to enable them.
- A button that navigates, or a link that performs a destructive action.
- Tiny tap targets; relying on a 16px glyph as the whole hit area.
- A press with no feedback, or a destructive action with no confirmation.
- Decorative hover animations that delay the actual response.
