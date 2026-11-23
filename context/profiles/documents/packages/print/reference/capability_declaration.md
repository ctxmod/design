# Capability Declaration

Charter section 1 for the paginated-print medium — every umbrella principle and component file classified supported / adapted / dropped, plus the interaction-state and ISO 9241-110 determinations. The SSOT for the print exemption set.

This is **section 1 of the five the medium charter makes mandatory**
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/medium_charter.md" />). It
classifies every principle the design umbrella (the `core` profile) owns against the
paginated-print medium as **supported**, **adapted**, or **dropped**, with the
reason. Nothing is left ambiguously unaddressed: a reviewer reading this file
must be able to see, for any umbrella principle, whether it is in force here,
substituted, or off the table.

## What the medium has and does not have

The classifications below all follow from one pair of facts about the medium.

**The paginated-print medium HAS:** fixed page geometry (a page is a known
rectangle before any content is placed); page breaks (content is cut at a hard
boundary the designer must anticipate); running heads and folios (per-page
repeated wayfinding); footnotes and margin notes (a second, spatially adjacent
text stream); a print color gamut (subtractive ink on a reflective substrate);
and **no interaction**.

**The paginated-print medium does NOT have:** hover, focus, scroll, motion,
theme switching, viewport reflow, or **any non-happy state**. There is no
runtime to enter a loading state, no failure for an error state to report, and
no input for a disabled control to refuse. The rendered page is the terminal
artifact.

## This file is the exemption SSOT

This declaration is the **single source of truth for the default print
exemption set** consumed by any automated document review that infers its
configuration. Such an inference derives an exempt list from the output format;
that list is a *derivation of this table*, not an independent authority.

**When the declaration and the inferred exempt list disagree, the declaration
is correct and the inference is wrong.** A file classified **dropped** below
belongs in the print exemption set; a file classified **supported** or
**adapted** does not. Correcting a disagreement means changing the inference to
match this table, never the reverse.

## Classification — the 13 umbrella principles

| Principle file | Class | Reason |
|---|---|---|
| `typography.md` | **supported** | More in force here than on the web, not less. The medium's entire payload is set text; body size, measure, leading, and face metrics are the whole quality bar. Print has no user zoom and no reflow to rescue a bad measure, so the umbrella's obligations bind harder. |
| `spacing-scale.md` | **adapted** | The scale survives; its units change. Steps resolve to `mm` / `pt` / `em` against a physical page rather than to CSS px against a viewport, and the page's margins become the largest step in the scale. |
| `visual-hierarchy.md` | **adapted** | All the umbrella's contrast channels apply, plus one the umbrella does not have: **page position**. See <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/affordance_adaptation.md" />. |
| `composition.md` | **adapted** | Alignment, grids, Gestalt grouping, and balance all apply. Responsive reflow is void; **the spread replaces it** as the compositional unit for twoside documents. |
| `color.md` | **adapted** | Identity-vs-signal and semantic-role reasoning survive intact. The gamut does not: subtractive ink on paper, no backlight, no emissive contrast. See <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/token_translation.md" />. |
| `information-density.md` | **adapted** | Density remains a first-class principle, but its budget is the **physical page area**, not an unbounded scroll. Progressive disclosure has no interactive mechanism and is re-expressed as document structure (summary before detail, appendix after body). |
| `design-language.md` | **supported** | The grammar of consistent, repeated decisions is medium-agnostic. A document that changes its table treatment between chapters fails this principle exactly as a web app that changes its button treatment between screens does. |
| `perception-cognition.md` | **supported** | The named laws hold on paper: proximity, similarity, working-memory limits, serial position, von Restorff, processing fluency. **Fitts's law is the single exception** and genuinely voids — there is no pointing task. Recorded in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/affordance_adaptation.md" />. |
| `accessibility-as-quality.md` | **adapted** | Focus rings, hit targets, and the live accessibility tree have no analogue. The principle's substance survives as **legibility**: contrast of ink against paper, type size at reading distance, unambiguous reading order, and tagged-PDF structure where the output format carries one — see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/accessible_pdf.md" />. |
| `iconography.md` | **adapted** | Construction discipline (canvas, live area, stroke-to-font-weight matching, optical centering, one concept per icon) applies unchanged. Print adds a resolution floor: an icon must survive rasterization at print DPI, and hairline strokes that hold on a backlit screen disappear in ink. |
| `internationalization.md` | **adapted** | Locale remains an orthogonal token mode and re-resolves here. RTL is a page-level spatial rethink: the gutter, the folio position, and the running-head alignment all mirror, and the recto/verso relationship inverts. |
| `motion.md` | **dropped** | There is no animation runtime in a typeset document. No duration, no easing, no choreography has any expression on a printed page. |
| `dark-mode.md` | **dropped** | There is no theme switch. Print has exactly one surface, and it is the substrate the document is rendered onto. Role-remapping against a second contrast target has no target to remap to. |

## Classification — the 9 component-taxonomy files

| Component file | Class | Reason |
|---|---|---|
| `components/taxonomy.md` | **supported** | The slot concept, the three-tier indirection, and the "map or declare absent" discipline all survive. What narrows is the slot *set*, and narrowing it is what <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" /> does. |
| `components/data-display.md` | **supported** | The read-heavy slots are the medium's core. Tables, lists, key-value pairs, and badges are exactly what a document displays; the density, alignment, and header-repetition obligations apply directly. Only the five *content* states drop (see `states.md` below). |
| `components/layout-containers.md` | **adapted** | Page shells and content-width regions map cleanly. Modals, drawers, and popovers are absent; floats and sidenotes are the print-native containers the umbrella has no name for. |
| `components/cards.md` | **adapted** | The container/grouping contract survives as a **framed region** — a callout box, a sidebar panel, a pull-quote. The header/body/footer contract applies; the interactive variant does not. |
| `components/navigation.md` | **ADAPTED — not dropped** | Print documents genuinely have wayfinding. The substitution is **runtime navigation → static wayfinding apparatus**: table of contents, running heads, folios, and cross-references. A reader still needs to know where they are and how to get elsewhere; only the mechanism changed from clicking to turning. Classifying navigation as dropped would exempt a document from having a usable TOC, which is the opposite of correct. |
| `components/buttons.md` | **dropped** | The slot's one job is action invocation, and a static document invokes nothing. There is no adapted form: unlike navigation, which has a real static analogue, a "button" printed on paper is a picture of a button. Consistent with <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" />, which declares the Buttons slot **absent**. |
| `components/inputs.md` | **dropped** | No interactive data entry. A printed form field is a ruled blank, not an input slot — it has no value, no validation, and no error affordance. |
| `components/feedback.md` | **dropped** | No runtime status to communicate. Toasts, alerts, progress, and inline validation all presuppose a system responding in time; a document has no time axis. |
| `components/states.md` | **dropped** | The universal interaction-state contract has **no live members** in this medium (see below), and the five content states presuppose a fetch that can be pending or fail. Both halves of the file are inexpressible here. |

## The universal interaction-state contract: no live members

The umbrella's normative state set is **default · hover · focus-visible ·
active/pressed · disabled · loading · error**
(<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/states.md" />). A
medium declares which members it honors.

**This medium honors none of them.** Not a subset — none. The charter names
this case explicitly: a static print medium drops all of them. `default` is the
only condition that exists, and a state set with exactly one member is not a
state contract.

The consequence is a review obligation, stated positively: **do not report a
document for failing to express a state this medium cannot express.** An
unstyled table row is not a missing hover state. A ruled blank on a form is not
a missing focus ring.

## ISO 9241-110: the medium-agnostic seven

The charter holds the seven dialogue principles exempt from casual dropping and
requires that any unavoidable drop be justified in the confidence note.

| Dialogue principle | Class | Determination |
|---|---|---|
| Suitability for the task | **supported** | A document serves a reading goal; extraneous apparatus that does not serve it is a finding here as anywhere. |
| Self-descriptiveness | **supported** | Expressed through headings, captions, running heads, folios, and legends. A reader must be able to tell, from any opened page, what they are looking at. |
| Conformity with user expectations | **supported** | Genre conventions are the print form of this principle — an invoice, a paper, and a report each carry reader expectations that predate the document. |
| Suitability for learning | **adapted** | No onboarding mechanism exists. Substituted by expository structure: definitions before use, summary before detail, and a glossary or notation table where the document introduces vocabulary. |
| Controllability | **adapted (weak)** | The reader sets the pace by turning pages and can enter at any point via the TOC or index. This is real but weak — it is reader-side navigation, not a system responding to direction. Justified in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/confidence_note.md" />. |
| Suitability for individualization | **dropped** | The rendering is fixed at typeset time. No mechanism exists for the reader to adapt type size, contrast, density, or layout. Justified in the confidence note. |
| Error tolerance | **dropped** | There is no user input that can be in error and no operation to recover. Justified in the confidence note. |

## Testable obligations

A document rendered under this profile must satisfy these. Each is checkable
against a rendered page image.

- **Every `supported` principle's obligations apply verbatim.** A typography or
  data-display finding is reportable at full severity; the medium supplies no
  excuse.
- **Every `adapted` principle is evaluated by its substitution, not by its
  original mechanism.** Judge `accessibility-as-quality` on ink contrast and
  type size, not on the absence of a focus ring.
- **No finding may be raised against a `dropped` principle.** A finding whose
  entire basis is motion, theme switching, an interaction state, an input, a
  button, or runtime feedback is out of scope for this medium.
- **Navigation is in scope.** A document lacking a table of contents where its
  length demands one, lacking folios, or carrying running heads that do not
  identify the current section, is a reportable navigation finding.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Supported principles bind fully | Read the finding's cited principle file against this table | The finding cites a `supported` file and was downgraded or waived for being "just print" |
| Adapted principles judged by substitution | Read the finding's stated mechanism | The finding names hover, focus, scroll, viewport, or theme as the failing mechanism |
| Dropped principles raise no findings | Cross-check the finding's cited file against the `dropped` rows | The cited file is `motion.md`, `dark-mode.md`, `buttons.md`, `inputs.md`, `feedback.md`, or `states.md` |
| Exemption set matches this table | Compare the inferred exempt list against the `dropped` rows | The two sets differ in either direction — this table wins |
| Navigation apparatus present | Look for TOC (documents past a few pages), folio on every body page, running head identifying the section | Any is missing or the running head is stale relative to the page's content |

## Anti-patterns

- Reporting a printed table for "missing hover states" or "no loading skeleton"
  — both are `dropped` here, and the finding is noise that trains a reader to
  distrust the review.
- Classifying `navigation.md` as dropped because print is not interactive. It
  produces documents with no TOC and no folios, and it contradicts this
  declaration.
- Treating `typography.md` as weakly binding because "it is only a document".
  It is the most binding principle in this medium.
- Silently omitting a principle from this table. An unclassified principle is a
  charter conformance failure, not a neutral default — the charter's key move
  is making not-applicable **explicit**.
- Adding a print exemption in tooling without adding the corresponding
  `dropped` row here. The tooling then asserts a capability claim this
  declaration does not make.
