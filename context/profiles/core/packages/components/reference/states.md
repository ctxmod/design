# Component States

Universal interaction-state contract for components and the five content states every data surface must design.

Two state contracts run across the whole <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />. The
first governs every *interactive* slot — the moment-to-moment conditions a control
must express as the user touches it. The second governs every *data surface* — the
content conditions a display must design for, not just the one where data exists.
Both are normative: they apply to slots that don't name them individually, and a
slot is incomplete until the applicable states are designed.

## Part A — The universal interaction-state contract

Every interactive slot — buttons, inputs, links, tabs, menu items, interactive
cards, controls of any kind — must define this state set:

| State | Must communicate |
|-------|------------------|
| **Default** | This is interactive and available now |
| **Hover** | This responds to a pointer — subtle, instant feedback (pointer devices only) |
| **Focus-visible** | Keyboard focus — a clearly visible focus ring (≥ 3:1 contrast), never suppressed |
| **Active / pressed** | The interaction registered — immediate, tactile feedback |
| **Disabled** | Not available now, and *why* should be discoverable; reduced contrast must not make it invisible |
| **Loading** | An operation is in progress — show it, keep layout stable, prevent double-activation |
| **Error** | This control or its value is in a failed/invalid condition and needs correction |

**The obligation is normative, not implicit.** A slot is not "complete" because its
happy path is drawn — it is complete when every *applicable* state in this set is
designed. The slot detail files (e.g. <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />)
restate this set in their own terms; this contract is the source they draw from, so
a control type not yet given its own file still owes these states.

### Which states are medium-conditional

Not every state exists on every medium. The set above is the *maximum*; a medium
declares which members it can honor in its capability declaration (see the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/medium_charter.md" />):

- **Hover** is absent on touch-only mediums — there is no pointer to hover. A slot
  must not hide essential affordance or information behind hover, because a hover
  state may never fire (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />).
- **Focus-visible** is essential on keyboard-driven mediums and pointer mediums
  alike; it is the keyboard user's only positional feedback.
- **cli** (a text/terminal medium) drops **hover** and **focus-visible** as
  pixel-ring concepts and re-expresses the remaining states with text affordances
  (inverse/dim/marker), per its capability declaration.

Designing a state the medium cannot render is wasted; *failing* to design a state
the medium can render is an incomplete slot. The capability declaration is where
that boundary is drawn, per medium.

## Part B — The five content states

Every data surface — tables, lists, feeds, dashboards, search results, any region
whose content is fetched or accumulated — must design all five content states, not
just the populated one:

| State | Means | Must provide |
|-------|-------|--------------|
| **Blank / empty** | No data exists yet (first use, cleared, or filtered to nothing) | Explanation of *why* and the next action — never a bare blank |
| **Loading** | Data is being fetched | A calm indicator or skeleton matching the final shape |
| **Partial** | Some data present, more loading or paginating | The visible data plus an honest "more coming" affordance |
| **Error** | The fetch or operation failed | What failed, and how to recover (retry, contact, adjust) |
| **Ideal** | Data is present and populated | The designed, content-rich happy path |

**Empty and error are designed states, never default-blank.** The populated view is
the easy one; the quality of a data surface is judged by the four states around it.
Specifically:

- The **empty** state explains the cause (first use vs. filtered-to-nothing vs.
  cleared), offers the next action (create the first item, broaden the filter), and
  carries an inviting voice — an illustration is appropriate where it adds warmth,
  never required (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" /> for the empty-state voice contract).
- The **error** state explains specifically what went wrong and gives a path back;
  "Something went wrong" with no recourse is a non-state.

This is a **cross-component** obligation. It is not satisfied by the existence of an
empty-state slot in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />; it is owed by *every* data surface in
the taxonomy — a table, a card grid, and a dashboard each design their own five
states. The feedback empty-state slot is the *vocabulary*; this principle is the
*requirement to use it everywhere data is shown*.

## Anti-patterns

- An interactive slot with a focus ring stripped off "for cleanliness" — a
  keyboard user is now lost (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />).
- Essential affordance gated behind hover on a touch medium, so it never appears.
- Treating disabled and loading as the same look — the user can't tell "can't yet"
  from "working now".
- An empty grid or table shown with no explanation, no cause, and no next action —
  the user can't tell broken from genuinely empty.
- A data surface that designs only the ideal state and silently shows a blank on
  empty, a frozen view on loading, and nothing on error.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
