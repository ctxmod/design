# Floats and Numbering

Figure and table numbering for scholarly documents — sequential gap-free numbering per float class, a caption-placement convention applied consistently (tables above, figures below by default), every float referenced from the body, and no orphaned floats.

A float is a figure, table, listing, or equation that the typesetter may
relocate away from the point in the prose where it is discussed. That
relocation is what makes numbering necessary: the reader is told "see Table 3"
and must find Table 3 somewhere else on the spread or a page over. The number
is the address, and the caption is the label at that address.

This is the paginated-print medium's substitute for a hyperlink, and it fails
in the same way a broken link fails: silently, and only for the reader who
tried to follow it.

## Testable obligations

### Numbering

- **Each float class numbers independently and sequentially.** Figures run
  1, 2, 3…; tables run 1, 2, 3…; the two sequences do not interleave and
  neither skips.
- **Numbering is gap-free and duplicate-free within a class.** A jump from
  Figure 2 to Figure 4, or two Table 3s, means a float was removed or a counter
  was reset.
- **A chapter-scoped scheme is applied uniformly.** A thesis numbering
  `Figure 2.1`, `2.2`, `3.1` is conforming; one that switches to flat numbering
  mid-document is not.
- **The number appears at the float, not only in the reference.** A figure
  referred to as "Figure 3" carries a visible "Figure 3" at its own position.

### Captions

- **One caption-placement convention is applied per float class.** The dominant
  academic convention places **table captions above** the table and **figure
  captions below** the figure, and that is the default to apply absent another
  signal. Journals differ; a document that captions figures above throughout is
  conforming. A document that varies within a class is not.
- **The caption is bound to its float.** Caption and float sit on the same page,
  with a gap smaller than the gap separating the float from surrounding body
  text. A caption separated from its float by a page break has lost its label.
- **The caption is typographically distinct from body text.** Size, weight, or
  face separates it, so a reader scanning for floats can find the captions.
- **The caption says what the float shows.** A caption reading only "Figure 3"
  or "Results" is a label, not a caption; a reader who lands on the float from
  a distant reference needs it to stand alone.

### Reference and orphaning

- **Every float is referenced at least once from the body text.** A float no
  prose points to is orphaned: the reader has no signal about when to look at
  it or why.
- **Every in-text float reference resolves to an existing float.** A "see
  Table 5" in a document with four tables is a broken address.
- **Unresolved reference markers do not survive into the render.** A visible
  `??`, `\ref{fig:x}`, or `Figure ?` is a build failure.
- **A float appears on the same page as its first reference, or on a following
  page — never before it.** A reader encountering Figure 4 two pages before the
  text that introduces it has been given an answer before the question.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Sequential per class | List every figure number in page order; repeat for tables | The sequence skips, repeats, or interleaves classes |
| Scheme uniform | Compare the numbering form in the first and last chapters | Flat and chapter-scoped both appear |
| Number at the float | Look at each float on the rendered page | A referenced float carries no visible number |
| Placement convention | Note caption position for every table, then every figure | Position varies within one class |
| Caption bound | Measure caption-to-float gap vs. float-to-body gap; check page numbers | The caption is farther from its float than from the body, or on another page |
| Caption distinct | Squint at a page carrying a float | The caption is indistinguishable from body text |
| Caption self-contained | Read the caption alone | It does not state what the float shows |
| Every float referenced | For each float, search the body for its number | Any is unreferenced |
| Every reference resolves | For each in-text float reference, find the float | Any has none |
| No unresolved markers | Scan for `??`, `\ref`, `Figure ?` | Any appears |
| Float not ahead of reference | Compare the float's page with its first reference's page | The float precedes the reference |

## Anti-patterns

- Numbering figures and tables in one shared sequence (`Figure 1`, `Table 2`,
  `Figure 3`). It is unambiguous but breaks the reader's expectation that each
  class counts from one, and makes "the third table" unfindable.
- Placing a caption above one table because it happened to fall at a page top
  and below the next because it did not. Placement is a convention, not a
  layout convenience.
- Writing captions that duplicate the surrounding prose verbatim, which makes
  the caption long without making the float self-contained.
- Reporting an orphaned float in a document whose floats are deliberately
  gathered in an appendix and referenced as a set — check for the set reference
  before flagging each member.
- Treating a visible `\ref{fig:method}` as a numbering finding. It is a build
  failure: the cross-reference pass did not resolve, and the fix is a rebuild,
  not a renumber.
- Setting captions in the body face at body size to "keep the page calm",
  removing the only channel by which a reader scanning for evidence can find it.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/citations_and_references.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />
