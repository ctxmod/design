# Academic document type

The **document-type tier** for scholarly documents: articles, theses,
dissertations, conference papers, and the technical monographs that follow the
same conventions. It specializes
`documents` with the apparatus a scholarly reader
expects and a scholarly publisher requires.

```
core                    ← principles + abstract component taxonomy
  └── documents         ← paginated-print concretization
        └── academic  ← THIS (package): citations, floats, notes, front matter
```

This package inherits the paginated-print layer unchanged and adds **only what
the academic genre demands**.

## What makes an academic document different

Three properties separate a scholarly document from every other paginated one:

1. **It is a node in a citation graph.** Its claims point outward to other
   documents and its own identity depends on those pointers resolving. An
   unresolvable citation is not a typographic defect; it is a broken edge.
2. **Its evidence is numbered and referenced from a distance.** Figures,
   tables, and equations are addressed by number from prose that may be pages
   away. The numbering system is load-bearing navigation, not decoration.
3. **It has a formal front matter.** A reader — and a reviewer, and an indexing
   system — expects a title block, an abstract, and keywords in a known order
   before the argument begins.

## Convention, applied consistently

Academic conventions vary by discipline, journal, and style manual. Author-date
and numeric citation systems are both correct; caption-above and caption-below
are both defensible; front-matter ordering differs between a thesis and a
letter. **This package does not pick a house style.** Every obligation below is
stated as *the document applies one convention and applies it throughout*. A
document that captions its tables above and its figures below is conforming; a
document that captions two tables above and one below is not.

Where a dominant convention exists it is named as the default to apply absent
another signal, never as the only correct answer.

## What lives here

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/citations_and_references.md" /> —
  internal consistency of the citation system, bidirectional resolution between
  in-text citations and the reference list, and reference-list alignment.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/floats_and_numbering.md" /> —
  sequential numbering, caption placement convention, every float referenced
  from the body, no orphaned floats.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/footnote_density.md" /> —
  when the note apparatus has grown into content that belongs in the body or an
  appendix, with a checkable threshold.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/front_matter_and_running_heads.md" /> —
  title block, abstract, keywords, front-matter ordering, and the verso/recto
  running-head asymmetry with its chapter-opening suppression.

## What does NOT live here

- **Paginated-print mechanics** — page geometry, break behavior, footnote
  *placement* mechanics, the print gamut. Those are
  `documents`. This package governs how much
  footnote there should be, not how the typesetter places it.
- **A specific style manual.** No APA / Chicago / Vancouver rule set is
  reproduced here. See "Convention, applied consistently" above.
- **Concrete style values** — page size, margins, typeface pairing,
  `base-font-size`. Those belong to the rendering style the document is
  rendered with.

## Selection

This package is opt-in: a session selects it explicitly (the `documents`
profile with the `academic` package) when the document is scholarly. A renderer may
map its own style categories onto the document-type packages; that mapping is
documented by the renderer, not here.
