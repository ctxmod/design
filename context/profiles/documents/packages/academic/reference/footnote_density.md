# Footnote Density

Footnote density for scholarly documents — a checkable threshold on the fraction of the text block the note apparatus consumes, above which the notes carry content that belongs in the body or an appendix.

A footnote is a **second text stream** running below the first, spatially bound
to a point in it. That binding is the primitive's entire value: the reader can
consult the note without leaving the page, and return without losing their
place. It is also the primitive's cost — every note the reader consults is an
interruption of the argument.

Density is where the cost overtakes the value. A page whose lower third is
notes has stopped being a page with notes and become two documents typeset on
top of each other, and the reader must choose which one to read. The content
that produced that page usually wants to be somewhere else: an aside long
enough to argue belongs in the body, and a digression too tangential for the
body belongs in an appendix.

## The threshold

**A page whose footnote apparatus consumes more than roughly one third of the
text block's height is a density finding.** State the measured fraction with
the finding.

The threshold is a heuristic marking a region, not a constant. One dense page
in a document of otherwise light notes is a local artifact — report it as such,
at low severity. A pattern of dense pages is the finding that matters, and it
is a structural claim about the document, not a claim about any one page.

Severity scales with both the fraction and the frequency:

| Pattern | Reading |
|---|---|
| One page over the threshold | Local artifact; low severity |
| A run of consecutive pages over it | The section's material wants restructuring |
| A majority of pages over it | The document's note apparatus is carrying its argument |

## Testable obligations

- **Measure the apparatus, not the note count.** Twelve one-line citation notes
  are lighter than two half-page discursive notes. Height on the page is the
  measure.
- **Report a run, not each page in it.** Consecutive pages over the threshold
  are one finding about a section, with the page range and the peak fraction
  named.
- **Distinguish citation notes from discursive notes.** A note-based citation
  system (where every reference is a footnote) produces high counts by design
  and is not a density finding unless the apparatus height still exceeds the
  threshold. The finding is about volume of *prose* pushed below the rule.
- **Name where the content should go.** A discursive note over a few lines that
  argues a point is body material; one that supplies data or a tangent is
  appendix material. A finding that only reports the fraction gives the author
  no move.
- **A note does not span more pages than its anchor.** A note continuing onto
  the next page has broken the spatial binding that is the primitive's reason
  to exist — this is a finding regardless of the density fraction. See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" />.
- **The note stream is typographically subordinate.** Notes are set smaller
  than body text and separated from it by a rule or by clear space. Notes set at
  body size compete with the argument rather than supporting it.
- **Note markers are unambiguous in the body.** A superscript numeral must be
  distinguishable from an exponent, and note numbering must not restart in a way
  that makes two notes on facing pages share a marker.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Apparatus fraction | Measure the note block's height on each sampled page; divide by the text-block height | The fraction exceeds ~0.33 |
| Run reported once | Group consecutive over-threshold pages | A separate finding was raised per page |
| Citation vs. discursive | Read a sample of the notes | The finding cites a note-based citation system as excessive prose |
| Remedy named | Read the finding | It states a fraction with no destination for the content |
| Note fits its page | Check whether any note continues past the page break | Any does |
| Notes subordinate | Compare note type size and separation against body | Notes are at body size, or no rule/space separates the streams |
| Markers unambiguous | Look at a marker adjacent to a numeral or in a mathematical passage | It reads as an exponent, or two visible notes share a marker |

## Anti-patterns

- Counting notes instead of measuring them, so a page of terse citation notes
  is flagged and a page carrying two essays is not.
- Raising the finding on every page of a run, producing twenty findings for one
  structural problem and burying everything else in the report.
- Recommending "fewer footnotes" with no destination. The content exists; the
  question is where it lives.
- Flagging a note-based citation system as inherently over-dense. Disciplines
  that use it produce documents with a note on every sentence by design, and
  the apparatus can still sit well under the threshold.
- Setting notes at body size to make them "accessible", which erases the
  subordination that lets a reader skip the stream and removes the visual
  signal that the density finding depends on.
- Treating a note that breaks across pages as a typesetter's problem rather than
  a length problem. The typesetter broke it because it did not fit.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/citations_and_references.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/affordance_adaptation.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />
