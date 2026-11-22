# Slot Mapping

Charter section 2 for the paginated-print medium — each umbrella component slot mapped to a document primitive (page, column, float, sidenote, table, figure, TOC, folio, framed environment) or declared absent with a reason.

This is **section 2 of the five the medium charter makes mandatory**. It maps
each slot in the umbrella's abstract component taxonomy
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />)
onto a paginated-print primitive, **or declares the slot absent with a reason**.

A slot names a responsibility; the medium names the primitive that carries it.
The mapping is to a primitive, never to a styling. Slots that map inherit their
Open UI name and role semantics from the taxonomy unchanged — this profile
supplies only the rendering.

**Absence is a declared outcome, not an omission.** The charter is explicit
that silently dropping a slot is a conformance failure while stating "absent
because the medium has no interaction" is conformance. Four slots are absent
here, and each carries its reason below.

## The mapping

| Slot | Document primitive | Notes |
|---|---|---|
| **Layout containers** | page · column · float · sidenote | The page is the outermost container and the only one with fixed, known geometry. Columns partition the text block. A float (figure, table, listing) is a container the typesetter may relocate to a nearby page position; a sidenote or margin note is a container in the margin, spatially bound to a point in the main text. Modals, drawers, and popovers are absent — they are overlay primitives with no print analogue. |
| **Data display** | table · figure · caption · listing | The medium's core slot. A table is a ruled or unruled aligned grid; a figure is a placed graphic; a caption is the label bound to either; a listing is a set-off verbatim block. Every one carries a number and a caption when it is cross-referenced. |
| **Navigation** | TOC · running head · folio · cross-reference | The static wayfinding apparatus. The TOC is the document-level map; the running head is the per-page "where am I"; the folio is the per-page address; a cross-reference is the static link between two addresses. This slot is **mapped, not absent** — see the ADAPTED classification in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/capability_declaration.md" />. |
| **Cards** | framed environment · callout box · pull-quote panel | The container/grouping contract survives as a visually set-off region: a bordered or tinted box, an admonition, a sidebar panel, a pull-quote. The header/body/footer contract maps onto title/content/attribution. Only the *static* card variant maps; the interactive card variant is absent with the Buttons slot's reason. |
| **Buttons** | **absent** | The slot's single responsibility is **action invocation**, and a static document invokes nothing. There is no target to press and no system to respond. Unlike Navigation — which has a real static analogue in the TOC and cross-reference — a button has none: a rendered button shape on paper is an image of a control, not a control. Inventing a forced analogue is exactly what the charter tells a medium not to do. |
| **Inputs** | **absent** | The slot's responsibility is **data entry**, and the medium accepts no input. A ruled blank on a printed form is not an input primitive: it holds no value, performs no validation, has no error affordance, and has no label/helper/error contract to satisfy. The reader's pen is outside the medium. |
| **Feedback** | **absent** | The slot's responsibility is **runtime status communication** — toasts, alerts, progress, inline validation. All of these presuppose a system responding *in time* to something the user just did. A document has no time axis and no operation in flight, so there is no status to communicate. Note the boundary: a *printed* warning notice is content the author wrote, carried by the Cards slot as a callout; it is not a Feedback-slot instance. |
| **States** | **absent** | The slot's responsibility is the universal interaction-state contract plus the five content states. The capability declaration records that this medium honors **none** of the seven interaction states and that the five content states presuppose a fetch that can be pending or fail. With no live members on either half, the slot has nothing to map. |

## Testable obligations

- **Every mapped slot's role semantics are inherited unchanged.** A table in a
  document owes the same header, alignment, and density obligations the
  taxonomy's data-display slot states; the medium changed the rendering, not
  the contract.
- **Every float carries a caption and a number when it is cross-referenced.** A
  figure or table referred to from the text as "see Figure 3" must be labelled
  "Figure 3" at its own position, and the number must resolve.
- **A sidenote or margin note stays on the same page as its anchor.** A note
  whose anchor is on page 4 and whose body is on page 5 has broken the spatial
  binding that is the primitive's whole reason to exist.
- **The navigation apparatus is present at the scale the document demands.** A
  multi-section document carries a TOC; every body page carries a folio;
  running heads name the section the page is actually in.
- **No absent slot is reported as missing or as unstyled.** Buttons, Inputs,
  Feedback, and States are declared absent above; a finding against any of them
  is out of scope.
- **A content warning is not a Feedback instance.** An author-written notice is
  evaluated as a Cards-slot callout — for framing, contrast, and placement —
  not for severity, dismissibility, or persistence.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Mapped slots inherit taxonomy semantics | Read the primitive against its taxonomy slot file | The primitive drops an obligation the slot file states and the medium can express |
| Floats numbered and captioned | Scan the page image for each figure/table; match against in-text references | A referenced float has no visible number, or the number does not match the reference |
| Sidenote/anchor co-location | Compare the note's page with its anchor's page | They differ |
| Navigation apparatus present | Look for TOC, folio on each body page, section-accurate running head | Any is missing, or the running head names a section the page is not in |
| Absent slots raise no findings | Read the finding's cited slot | It cites Buttons, Inputs, Feedback, or States |
| Callout classified correctly | Read the notice's origin | It is evaluated as runtime feedback rather than as authored content in a framed region |

## Anti-patterns

- Inventing a "print button" — a boxed, tinted call-to-action rendered on paper
  — and then reviewing it against the Buttons slot's variant and state
  contracts. The slot is absent; the artifact is a Cards-slot callout.
- Treating a printed form's ruled blanks as Inputs and reporting missing helper
  text, validation, or error states.
- Declaring Navigation absent alongside the other four. It is the one
  interaction-adjacent slot with a genuine static substitution, and dropping it
  removes the obligation to have a usable TOC.
- Mapping a slot to a *styling* ("Cards → a grey background") rather than to a
  primitive ("Cards → a framed environment"). The mapping must name a thing the
  typesetter emits, so that a brand or type profile has something to style.
- Leaving a slot unlisted. Eight slots exist in the taxonomy and eight rows
  appear above; a ninth slot added upstream must be classified here before this
  profile is conforming again.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/token_translation.md" />
