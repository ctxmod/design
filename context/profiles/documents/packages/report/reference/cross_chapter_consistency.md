# Cross-Chapter Data-Display Consistency

Data-display consistency across chapters — the same table treatment, figure caption style, and number formatting in chapter 7 as in chapter 2. The cross-document dimension a single-page review cannot see.

This is the principle a single-page review cannot reach. Every obligation below
is a **comparison between distant samples**: the finding is never that a page
is wrong, but that two pages disagree.

The reason it matters is that a long report is usually written by several people
over several months, and data display is where that shows. Chapter 2's tables
were set by whoever wrote chapter 2. The reader, encountering chapter 7's
tables, has to relearn how to read a table — and, worse, cannot tell whether a
difference in treatment signals a difference in meaning. In a document whose
whole purpose is to present evidence, an unintended visual difference reads as
an intended one.

This is the report-scale expression of the umbrella's design-language
principle: the grammar of consistent, repeated decisions. See
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />.

## Sampling is the method

A finding here requires at least two samples from **different chapters, far
apart in the document**. A review that samples one page, or several pages from
one chapter, cannot raise or clear any obligation on this page.

Where a document is sampled rather than read exhaustively, state which chapters
were compared. An inconsistency found between chapters 2 and 7 says nothing
about chapters 3 through 6, and a finding that implies otherwise overstates its
evidence. See the sampling limits in the medium's confidence note.

## Testable obligations

### Tables

- **Rule treatment is uniform across chapters.** Whether the document uses
  horizontal rules only, full grids, or zebra banding, it uses the same one
  everywhere. Booktabs-style (top, header, bottom rules only) in chapter 2 and
  a full grid in chapter 7 is a finding.
- **Header treatment is uniform.** Weight, case, alignment, and any background
  are the same in every chapter.
- **Column alignment rules are uniform by content type.** Numbers align the
  same way everywhere (right or decimal), text the same way everywhere (left),
  and the rule does not change between chapters.
- **Cell padding and row height are uniform.** A dense table in one chapter and
  an airy one in another, at the same information density, is a finding.
- **Header repetition on continued tables is uniform.** Either every table
  spanning a page break repeats its header row, or none does.

### Figures and captions

- **Caption placement is uniform per float class across chapters.** The
  convention chosen holds document-wide. See the placement obligation in the
  academic profile's float principle for the underlying convention.
- **Caption typography is uniform.** Size, face, weight, alignment, and the
  label's format (`Figure 3.` vs `Figure 3:` vs `Fig. 3 —`) are the same in
  every chapter.
- **Figure sizing and placement follow a shared system.** Figures do not run
  full-measure in one chapter and half-measure in another without a content
  reason; the reader should not infer importance from a width difference that
  was an accident of authorship.
- **Chart conventions are uniform where the same data type recurs.** Axis
  labelling, gridline treatment, legend position, and series color assignment
  are the same across chapters for comparable charts. A metric shown in one
  color in chapter 2 and another in chapter 7 is the most damaging instance of
  this class.

### Numbers and units

- **Number formatting is uniform.** Thousands separator, decimal separator,
  significant-figure convention, and negative-number treatment are the same
  everywhere.
- **Units are formatted uniformly.** Spacing between value and unit, symbol vs.
  spelled-out form, and prefix conventions do not vary between chapters.
- **Date formatting is uniform.** One format throughout, with no chapter
  switching between numeric and spelled-out months.
- **Percentages, currency, and ranges follow one convention each.** `5–10%` and
  `5% to 10%` are both fine; both in one document is not.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Rule treatment | Compare a table from an early chapter with one from a late chapter | The rule system differs |
| Header treatment | Compare header rows across the same samples | Weight, case, alignment, or fill differs |
| Column alignment | Compare a numeric column in each sample | The alignment rule differs |
| Padding and row height | Measure cell padding in each sample | It differs at comparable density |
| Continued-table headers | Find a table spanning a break in each of two chapters | One repeats the header and the other does not |
| Caption placement | Note caption position for a float in each of two chapters | It differs for the same float class |
| Caption typography | Compare caption type and label format across chapters | Size, face, or label punctuation differs |
| Figure sizing | Compare figure widths across chapters | Widths differ without a content reason |
| Chart conventions | Compare two comparable charts from different chapters | Axis, gridline, legend, or series color assignment differs |
| Number formatting | Collect the largest number and a decimal number from each chapter sampled | Separator or precision convention differs |
| Unit formatting | Compare a value-with-unit from each sample | Spacing or symbol form differs |
| Date formatting | Collect a date from each sample | The format differs |
| Percent/currency/range | Collect one of each from two chapters | Two conventions appear for one type |

## Anti-patterns

- Raising a consistency finding from a single sample. Without two distant
  samples the claim has no evidence, and the reader cannot act on it.
- Reporting each differing table as its own finding. One finding names the
  divergence, the two samples that show it, and the treatment that should
  become canonical.
- Declaring consistency clean after sampling one chapter. Absence of evidence in
  one chapter is not evidence of consistency across seven.
- Nominating the *first* observed treatment as canonical by default. The
  treatment that appears most often, or that best serves the data, is the one to
  standardize on — chapter order is not an argument.
- Treating a deliberate difference as a finding. A chapter presenting a
  different kind of data may legitimately need a different table treatment; the
  finding is unexplained variation, and a reader should be able to see the
  reason from the content.
- Flagging series-color divergence without checking whether the document is
  reproduced in monochrome, where the color assignment may not be the channel
  carrying the distinction at all.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/section_hierarchy.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/appendix_conventions.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />
