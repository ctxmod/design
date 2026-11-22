# Single-Page Pressure

Single-page pressure for invoices — an invoice that breaks to a second page to carry one line is a finding; the widow-page check measures the final page's content height as a fraction of the text block.

An invoice is expected to be **one page**. That expectation is not aesthetic
preference: it is what makes the document a single physical object that can be
filed, mailed in one envelope, scanned in one pass, and checked without turning
anything over. A reader who receives a two-page invoice checks the second page
for content they might have missed, and is annoyed to find it carries a footer
and one line.

This is the one principle in the paginated-print stack where **the page count
itself is the finding**. Elsewhere the medium's fixed geometry is a constraint
the design works within; here the design is obliged to work within *one*
instance of it, and exceeding it by a small margin is worse than exceeding it
by a large one.

## The rule, stated sharply

**An invoice that breaks to a second page to carry a small remainder is a
finding.** The remainder is what makes it a finding: an invoice with sixty line
items legitimately runs to three pages, and the third page carrying twenty
items is not a defect. An invoice whose second page carries the totals block
and nothing else — or a single orphaned line item, or only the footer — has
paid the full cost of a second page for almost none of its benefit.

The severity scales inversely with the remainder. A final page at 5% fill is a
worse finding than one at 40%.

## Testable obligations

- **A final page carrying under roughly 15% of a full text block's content
  height is a widow-page finding.** The threshold is a heuristic, not a
  constant: it marks the region where the page's fixed overhead (margins,
  running head, folio, footer) exceeds the content it carries. Report it; state
  the measured fraction so the reader can judge.
- **The totals block does not break across pages.** Subtotal, tax, and grand
  total sit together on one page. A grand total separated from its operands has
  broken the arithmetic chain that
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::invoice@documents/reference/totals_and_arithmetic.md" />
  requires.
- **A single line item does not sit alone on the final page.** One orphaned row
  is the canonical instance of the finding.
- **The footer content — payment details, bank information, terms text — is not
  the sole occupant of a page.** If it is, the break happened one element too
  early.
- **Where a break is genuinely unavoidable, the break is deliberate and
  signalled.** A multi-page invoice repeats the column headers on each page,
  carries a page-`n`-of-`m` folio, and marks intermediate page ends as
  continuations rather than endings (no grand total on a non-final page).
- **The remedy proposed with the finding is proportionate.** A widow page
  caused by two lines of slack is a leading, margin, or line-height adjustment —
  not a redesign. Name the smallest change that would recover the page.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Widow page | Measure the vertical extent of content on the last page; divide by the full text-block height | The fraction is under ~0.15 |
| Totals block intact | Locate subtotal, tax, and grand total on the rendered pages | They do not share a page |
| No orphaned line item | Count line-item rows on the final page | Exactly one, with nothing else but chrome |
| Footer not alone | Read the final page's content | It carries only payment/bank/terms text |
| Deliberate multi-page | On a genuine multi-page invoice, check each non-final page | Column headers not repeated, no `n of m` folio, or a grand total appears before the last page |
| Proportionate remedy | Read the finding's proposed fix | It proposes restructuring where a spacing adjustment would recover the page |

## Anti-patterns

- Reporting a page-count finding on a long invoice that legitimately needs the
  pages. The finding is about the *remainder*, not the count; an invoice at
  three full pages is not in scope.
- Solving a widow page by shrinking body type below the medium's legibility
  floor. Recovering one page at the cost of an unreadable one trades a
  proportionate finding for a disproportionate one; the paginated-print layer's
  type-size obligations still bind.
- Solving it by deleting content — dropping the payment terms or truncating
  descriptions — which converts a layout finding into a completeness finding.
  See <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::invoice@documents/reference/address_and_legal_fields.md" />.
- Treating the ~15% threshold as a hard constant and reporting a page at 16%
  fill as clean. State the measurement and let the number carry the argument;
  the threshold marks a region, not a boundary.
- Suppressing the running head and folio on the second page to make it look
  less like a page. It still is one, and now it has lost its wayfinding.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/affordance_adaptation.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />
