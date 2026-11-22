# Paginated-print medium

The **medium tier** of the user-facing-surface design stack, for the
**paginated-print** medium. This profile takes the medium-agnostic principles
defined by the `core` umbrella and concretizes them for a
typeset document: a fixed page rectangle, a hard page break, running heads and
folios, footnotes and margin notes, ink on paper, and **no runtime whatsoever**.

It is the sibling of `web` and conforms to the same
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/medium_charter.md" />. Where
`web` maps the umbrella onto the DOM, this profile maps it onto the page.

It sits between the abstract umbrella above it and the concrete document-type
profiles below it:

```
core                    ← principles + abstract component taxonomy (medium-agnostic)
  └── documents         ← this profile: paginated-print concretization
        └── <type>      ← opt-in document-type package: invoice, academic, report
```

## What lives here

The five sections the medium charter makes mandatory, one principle file each:

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/capability_declaration.md" /> —
  every umbrella principle classified supported / adapted / dropped for print.
  **This file is the SSOT for the print exemption set.**
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" /> —
  each umbrella component slot mapped to a document primitive, or declared
  **absent with a reason**.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/token_translation.md" /> —
  how semantic tokens emit to LaTeX lengths and colors; which mode axes
  re-resolve and which collapse.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/affordance_adaptation.md" /> —
  the medium's interaction reality: read-only input model, no hit targets,
  page-in-hand viewing distance, density default.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/confidence_note.md" /> —
  where this profile's guidance is validated and where it is extrapolated,
  including the sampling and extraction-mode limits of automated review.

## What does NOT live here

- **Abstract principles** — typographic theory, the spacing model, color
  reasoning, the component taxonomy. Those stay in the
  `core` umbrella; this profile references them and maps
  them onto page primitives.
- **Web concretization** — breakpoints, viewport units, DOM semantics, CSS.
  That belongs to `web`. The two media are
  siblings, not layers; neither inherits the other's mechanics.
- **Concrete style values** — chosen page size, margins, typeface pairing,
  `base-font-size`, per-role size multipliers. Those belong to the rendering style
  a document is rendered with, and to the document-type packages below.
- **Document-type conventions** — invoice totals alignment, academic citation
  formatting, report appendix structure. Those belong to
  the document-type packages (`academic`, `invoice`, `report`).

## How document-type packages use this

A document-type package (`academic`, `invoice`, `report`) layers on `documents` and inherits the
paginated-print layer unchanged: it does not re-derive that print has no hover,
or that elevation becomes rules and whitespace. It adds **only what its type
demands** — the genre conventions a reader of that document kind expects — and
expresses them through the page primitives this profile establishes.

Document-type packages are opt-in. A document whose kind no document-type
package covers is designed under `core` + `documents` alone, which is why every
mandatory section here must stand on its own without a type package beneath it.
