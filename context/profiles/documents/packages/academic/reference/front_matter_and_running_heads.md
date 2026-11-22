# Front Matter and Running Heads

Front-matter structure and running-head conventions for scholarly documents — title block, abstract placement and length, keywords, front-matter ordering, and the verso/recto running-head asymmetry with suppression on chapter-opening pages.

Front matter and running heads answer the same question at two scales: **what
is this, and where am I in it?** The front matter answers it once for the whole
document, before the argument starts. The running head answers it again on
every page, for a reader who opened the document in the middle.

Both are apparatus, not content, and both are judged by whether they work for a
reader who did not start at page one.

## Front matter

### Testable obligations

- **The title block is the strongest hierarchy step in the document.** The
  title outranks every heading in the body. Authors and affiliations sit below
  it, subordinated but grouped with it.
- **Author-affiliation binding is unambiguous.** Where multiple authors carry
  different affiliations, the marker system (superscript symbols or numerals)
  resolves every author to at least one affiliation, and every affiliation is
  claimed by at least one author.
- **The abstract is on the first page or the page immediately following the
  title page**, before any body section. An abstract after the introduction is
  not an abstract.
- **The abstract is visually set apart from the body.** A narrower measure,
  a smaller size, an indent, or a labelled block — some channel marks it as not
  being the first section of the argument.
- **The abstract is self-contained and bounded.** It carries no citation
  requiring the reference list, no reference to a numbered float, and no
  undefined abbreviation. Where the document or its venue declares a word
  limit, it is within it; absent a declared limit, an abstract running past
  roughly a third of its page has stopped being a summary.
- **Keywords, where present, follow the abstract and are formatted uniformly.**
  One separator, one capitalization rule, one order convention throughout.
- **The front-matter order is the conventional one for the document class and
  is applied without interleaving body material.** For an article: title block →
  abstract → keywords → body. For a thesis: title page → abstract →
  acknowledgements → table of contents → lists of figures/tables → body. A
  document may reorder for a venue's requirement; it may not scatter.
- **Front matter carries its own page treatment.** Where front matter is
  numbered separately (roman numerals) the scheme is applied consistently and
  the body restarts at arabic 1.

## Running heads

Running heads are the per-page wayfinding the paginated-print medium
substitutes for runtime navigation. See
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" />.

### Testable obligations

- **Every body page carries a folio.** No exceptions in the body; front matter
  may follow its own scheme.
- **The running head names the section the page is actually in.** A head naming
  a section that ended two pages earlier is stale and worse than no head at all.
- **Twoside documents observe verso/recto asymmetry.** The conventional
  assignment puts the broader context on the **verso** (left, even) page and
  the narrower on the **recto** (right, odd) — typically document or chapter
  title verso, section title recto. A document may invert this, but it applies
  one assignment throughout.
- **Running heads are suppressed on chapter-opening pages.** A page that
  already carries a chapter title in full display does not repeat it in the
  head. The folio may remain, and conventionally moves to the foot.
- **Running heads are suppressed on the title page and on full-page floats**
  where the convention of the document class calls for it, and the choice is
  uniform.
- **The head is typographically subordinate to every body heading.** It is
  smaller, lighter, or set in small caps — never at a weight that competes with
  the section heading below it.
- **Long titles are shortened, not folded.** A running head is one line. Where
  the full title will not fit, a declared short form is used; the head does not
  wrap and is not silently clipped mid-word.
- **RTL documents mirror the assignment.** Verso/recto reverse with the
  binding, and the folio position mirrors with them. See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/internationalization.md" />.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Title outranks headings | Compare the title's visual weight against the largest body heading | A heading ties or outranks it |
| Author/affiliation resolve | Trace every marker in both directions | An author has no affiliation, or an affiliation no author |
| Abstract placement | Find the abstract; find the first body section | The abstract follows a body section |
| Abstract set apart | Squint at the first page | The abstract reads as the first body paragraph |
| Abstract self-contained | Read it alone | It cites, references a float number, or uses an undefined abbreviation |
| Abstract bounded | Measure its height against the page's text block | It exceeds roughly a third with no declared limit permitting it |
| Keywords uniform | Read the keyword line | Separator or capitalization varies within it |
| Front-matter order | List front-matter elements in page order | Body material is interleaved, or an element is out of the class's order |
| Numbering scheme | Check the front matter's folios and the body's first folio | The scheme is mixed, or the body does not restart |
| Folio on every body page | Page through the body | Any body page lacks one |
| Head accuracy | On a sampled page, compare the head against the section the content belongs to | They differ |
| Verso/recto asymmetry | Compare a facing verso and recto pair, then another pair later in the document | Both carry the same content, or the assignment flips between pairs |
| Chapter-opening suppression | Look at a chapter-opening page | The head repeats the chapter title shown in display below it |
| Head subordinate | Compare head type against the section heading on the same page | The head is at or above the heading's weight |
| Short form used | Find the longest title | The head wraps to two lines or is clipped mid-word |

## Anti-patterns

- Setting the title at the same size as the top-level body headings so the
  first page reads as the first section, leaving the document with no visual
  beginning.
- Printing an abstract that opens with "In this paper we..." and then cites
  three works by number, which forces the reader out of the abstract to
  understand it.
- Repeating the chapter title in the running head on the chapter's own opening
  page, which spends the page's most prominent horizontal band restating what
  the display heading already says.
- Leaving a stale running head after a mid-page section change and treating it
  as acceptable because it is "close enough". A stale head actively misdirects;
  a missing one merely fails to help.
- Using the same running-head content on verso and recto in a twoside document,
  which discards the one channel a spread offers for showing two levels of
  context at once.
- Clipping a long title in the head with an ellipsis rather than authoring a
  short form, so every page carries a truncated fragment.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/citations_and_references.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />
