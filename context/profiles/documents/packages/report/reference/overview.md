# Report document type

The **document-type tier** for long-form reports: government and agency
reports, technical reports, memoranda, white papers, and the multi-chapter
analytical documents that share their shape. It specializes
`documents` with the conventions that make a long
document navigable and internally coherent.

```
core                    ← principles + abstract component taxonomy
  └── documents         ← paginated-print concretization
        └── report    ← THIS (package): hierarchy, summary, cross-chapter consistency, appendices
```

This package inherits the paginated-print layer unchanged and adds **only what
the report genre demands**.

## What makes a report different: length

An invoice is one page. A paper is read front to back. A report is neither: it
is long enough that most readers never read all of it, and it is entered
repeatedly at different points by different people looking for different
things. Every obligation here follows from that.

Length changes what a review can even see. A single page of a report tells you
almost nothing about the report — the interesting failures are **differences
between distant pages**. The table treatment in chapter 2 and the table
treatment in chapter 7 are each defensible; that they differ is the finding.
This is the dimension `documents` cannot express,
because the medium profile governs a page and this one governs a document.

**A report review that samples one page has not reviewed a report.** Sampling
must span the document, and the comparison across samples — not the judgment of
any one sample — is where this package's value lives. See the sampling limits
in the medium's confidence note.

## What lives here

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/section_hierarchy.md" /> —
  how deep the numbered hierarchy runs before it stops aiding navigation, and
  whether the levels are visually distinguishable from one another.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/executive_summary.md" /> —
  front-loaded, self-contained, bounded.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/cross_chapter_consistency.md" /> —
  the same table treatment, caption style, and number formatting in chapter 7
  as in chapter 2. The cross-document dimension.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/appendix_conventions.md" /> —
  appendix lettering, every appendix referenced from the body, and appendices
  carrying supporting material rather than load-bearing argument.

## What does NOT live here

- **Paginated-print mechanics** — page geometry, break behavior, running-head
  placement, the print gamut. Those are
  `documents`.
- **Scholarly apparatus** — citation systems, float numbering schemes,
  footnote density thresholds, front-matter ordering. A report that carries
  those conventions is better reviewed under `academic` package; this
  profile does not duplicate them.
- **Concrete style values** — page size, margins, typeface pairing,
  `base-font-size`. Those belong to the rendering style the document is
  rendered with.

## Selection

This package is opt-in: a session selects it explicitly (the `documents`
profile with the `report` package) when the document is a long-form report. A renderer may
map its own style categories onto the document-type packages; that mapping is
documented by the renderer, not here.
