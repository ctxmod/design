# Address Blocks and Legal Fields

Address-block conventions and legal-field completeness for invoices — sender/recipient placement and distinction, window-envelope compatibility as a physical constraint, postal-format fidelity, and the presence and prominence of the identifying, dating, and tax fields the document declares.

An invoice carries two categories of content besides the money: **who the
parties are** and **what identifies this transaction**. Both are read by
someone looking for a specific string rather than reading the page — a clerk
matching a payment, an auditor reconciling a ledger, a postal machine reading
through a window. Design that serves reading prose does not automatically serve
retrieval, and this is the part of an invoice where the difference bites.

## Address blocks

Two address blocks appear on almost every invoice and they have opposite jobs.
The **sender** block establishes identity and is normally paired with the
letterhead. The **recipient** block is an addressing artifact: it may be read
through an envelope window, keyed into a system, or compared against a
customer record.

### Testable obligations

- **The two blocks are visually distinguishable without reading them.**
  Position, weight, size, or rule — some channel other than the words separates
  sender from recipient. A reader must not have to parse the addresses to learn
  which party is which.
- **Each block is labelled where the layout does not make the roles obvious.**
  A conventional layout (sender top-left with the mark, recipient below-left in
  the window zone) may carry the roles positionally. A non-conventional layout
  must label them.
- **The recipient block is a contiguous rectangle with no interleaved
  content.** No rule, icon, or field is set between the recipient's name line
  and the last line of its address. A block interrupted mid-way is unreadable
  through a window and awkward to transcribe.
- **Window-envelope compatibility is preserved when the document declares a
  window-compatible layout.** The recipient block sits within the region a
  standard window exposes for the page size in use, with the block's own
  margins clear of the window edge on all four sides. This is a physical
  constraint: an address a millimetre outside the aperture is not a cosmetic
  finding.
- **Postal format follows the recipient's convention, not the sender's.**
  Line order, the position of the postal code relative to the locality, and the
  presence of a country line follow the destination's postal convention. A
  cross-border invoice carries a country line.
- **Line breaks in the address are semantic, not typographic.** An address line
  is never wrapped mid-line by measure. Where the block is too narrow for a
  line, the block widens or the type reduces; the line does not fold.

## Legal and identifying fields

An invoice carries a set of fields that identify the transaction: an invoice
number, an issue date, a due date, payment terms, tax identifiers (VAT number,
EIN, organization number, or the local equivalent), and per-line descriptions
of what is being charged for.

### Scope note — completeness, not a tax-law checklist

**This profile does not enumerate the fields any jurisdiction requires.** A
reviewer reading a rendered page cannot determine the issuer's jurisdiction,
and inventing a legal checklist would produce confident findings with no basis.
The obligation is stated over the fields *the document itself declares*: a
field the document carries must be complete and findable, and a field the
document's own template implies (a labelled row with no value, a "Tax ID:" with
nothing after it) must be filled.

A jurisdiction-specific requirement is a matter for the invoice's author or the
style it is rendered with — not for a visual review.

### Testable obligations

- **Every declared field carries a value.** A label with an empty value, a
  placeholder that survived into the render (`{{invoice_number}}`, `TBD`,
  `XXX`), or a date rendered as a raw timestamp is a finding.
- **The invoice number is findable in a single fixation.** It is set apart from
  the surrounding fields by position or weight — not buried mid-paragraph or
  set at body weight inside a run of other metadata.
- **Dates are unambiguous.** Numeric-only dates in a format where day and month
  are both plausible (`03/04/2026`) are ambiguous on a document that may cross
  borders; a month name or an ISO-ordered form removes the ambiguity. Issue
  date and due date are distinguishable by label, not by position alone.
- **Payment terms and the due date agree.** If both appear, the terms
  (`Net 30`) and the explicit due date must be consistent with the issue date.
  A visible contradiction is a finding.
- **Tax identifiers are labelled.** A bare alphanumeric string with no label is
  not a tax identifier to any reader who does not already know the format.
- **Line-item descriptions are legible at their set size and are not
  truncated.** A description clipped by its column, ending in an ellipsis, or
  overflowing into the adjacent column has lost the content the line exists to
  carry.
- **The field block does not compete with the grand total for prominence.**
  These fields are retrieval targets, not the page's headline; they are
  findable, not loud. See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::invoice@documents/reference/totals_and_arithmetic.md" />.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Blocks distinguishable | Squint at the page; identify which block is which without reading | Only the words separate them |
| Recipient block contiguous | Trace the block top to bottom | Any non-address element interrupts it |
| Window compatibility | Overlay the standard window aperture for the page size on the rendered page | Any address line, or its clearance margin, falls outside |
| Postal format | Compare line order and postal-code position against the destination's convention | It follows the sender's convention instead |
| No typographic folding | Look for a second line that begins mid-phrase | An address line has wrapped by measure |
| Fields carry values | Read every label on the page; check for a value after each | Any label is empty, or a placeholder token survived |
| Invoice number findable | Time a search for it on the page image | It requires reading surrounding text to locate |
| Dates unambiguous | Read every date | Numeric-only with an ambiguous day/month order, or issue and due are indistinguishable |
| Terms/due agree | Compute the due date from the issue date and the stated terms | The computed and printed dates differ |
| Descriptions intact | Scan the description column for clipping | Any ends in an ellipsis, is cut by the column edge, or overlaps a neighbour |

## Anti-patterns

- Centering the recipient block. It defeats window compatibility, and it
  defeats transcription: the eye loses the left edge that address reading
  depends on.
- Setting the sender block larger and heavier than the grand total in pursuit of
  brand presence, which inverts the page's hierarchy for the reader who opened
  it to check an amount.
- Rendering a date with the system's default timestamp format
  (`2026-08-09T00:00:00Z`) because no formatting was applied. It is a
  completeness failure disguised as a formatting one.
- Inferring a jurisdiction from a currency symbol or a language and then
  reporting a "missing legally required field" on that basis. The scope note
  above exists to prevent exactly this.
- Packing the identifying fields into a dense single line to save vertical
  space, so retrieval — the only reason the fields are there — becomes a parse.
- Treating a truncated line-item description as acceptable because the full
  text "is in the system". The invoice is the artifact; what it does not say,
  it does not say.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/internationalization.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />
