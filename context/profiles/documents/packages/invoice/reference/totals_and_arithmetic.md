# Totals and Arithmetic Legibility

Totals alignment and arithmetic legibility for invoices — decimal alignment down the money column, consistent currency-symbol placement, the subtotal-to-tax-to-total progression readable as a chain, and the grand total carrying the page's heaviest numeric weight.

An invoice's money column is the only part of the document a reader is expected
to **verify**, not merely read. Verification is a scanning task: the eye runs
down a column of numbers, compares magnitudes, and follows an addition chain to
its result. Every typographic decision in the money column either supports that
scan or defeats it.

The failure mode is specific and common: numbers that are *individually* well
set but *collectively* unscannable. Ragged decimal points, a currency symbol
that appears on some rows and not others, and a grand total set at the same
weight as a line item all leave the reader re-reading and, in the worst case,
reaching for a calculator to confirm what the page should have made obvious.

## Testable obligations

- **Decimal points align down every money column.** All amounts in a column
  share a common decimal position, so the integer parts stack right-aligned and
  the fractional parts stack left-aligned from that point. This holds across
  amounts of different magnitudes (`9.50` and `12,480.00` in the same column)
  and across the line-item block and the totals block if they share a column
  axis.
- **Fractional digits are uniform within a column.** Every amount in a column
  carries the same number of decimal places, including trailing zeros. A column
  mixing `100`, `100.5`, and `100.50` is a finding even when the values are
  correct.
- **Currency-symbol placement is consistent and stated once where possible.**
  Either every amount in the column carries the symbol in the same position, or
  the symbol appears in the column header / adjacent to the grand total only.
  Mixed presence within one column is a finding.
- **Thousands separators are present and uniform.** An invoice with
  five-or-more-digit amounts uses a separator, and uses the same one
  throughout. Locale determines which; consistency is the obligation.
- **The subtotal → tax → total progression reads as an arithmetic chain.** The
  operand rows and the result row are visually distinguished — typically by a
  rule above the result, or by a weight step — so a reader can see what is being
  added to what without reading the labels.
- **The grand total carries the heaviest numeric weight on the page.** It is the
  single most prominent number: larger, heavier, ruled, or otherwise stepped
  above every line-item amount and every intermediate subtotal. No line item
  outweighs it.
- **Amount labels sit adjacent to their amounts, not across the page.** The gap
  between a total's label and its value does not exceed the width at which the
  eye loses the row; where it must, a leader or a shared background row binds
  them.
- **Negative amounts and credits are unambiguous.** A discount, credit, or
  reversal is distinguishable from a positive amount by more than a hyphen —
  parentheses, an explicit sign with adequate whitespace, or a labelled row.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Decimal alignment | Draw a vertical line through the decimal points of a money column on the rendered page | Any decimal point sits off the line |
| Uniform fractional digits | Count digits after the separator on every amount in a column | Counts differ within one column |
| Currency-symbol consistency | Scan the column for symbol presence and position | Some rows carry it and some do not, or position varies |
| Thousands separators | Find the largest amount; check for a separator; compare with every other 4+-digit amount | Missing on any, or the separator character varies |
| Arithmetic chain legible | Cover the labels; try to identify operands vs. result from typography alone | The result row is indistinguishable from the operand rows |
| Grand total heaviest | Rank every number on the page by visual weight (size × weight × contrast) | Anything ties or outranks the grand total |
| Label/value adjacency | Measure the horizontal gap between a total label and its value | The gap exceeds roughly a third of the text-block width with no leader |
| Signed amounts unambiguous | Locate any negative or credit amount | Distinguished only by a hyphen that reads as a dash or hyphenation artifact |

## Anti-patterns

- Centering the money column. Centering destroys decimal alignment by
  construction; the column becomes unscannable no matter how well the numerals
  are set.
- Setting amounts in a proportional face with proportional (non-tabular)
  figures, so digit widths differ per glyph and the column will not align even
  when the decimal points nominally do. Tabular figures are the mechanism the
  alignment obligation assumes.
- Giving the grand total a decorative treatment (a tinted band, a box) that
  raises its *area* but not its *type weight*, while a line-item amount is set
  larger. Area is not the ranking channel a reader uses on a number.
- Right-aligning the labels and left-aligning the amounts, so the two drift
  apart in the middle of the page and the pairing collapses.
- Dropping the currency entirely on the assumption that context supplies it.
  An invoice crossing a border with no currency named is a completeness finding,
  not just a legibility one.
- Repeating the currency symbol on every one of forty line items, which turns a
  column of amounts into a column of symbols and defeats the magnitude scan the
  alignment exists to serve.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::invoice@documents/reference/single_page_pressure.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />
