# Invoice document type

The **document-type tier** for invoices and the transactional documents that
share their shape (credit notes, quotations, statements, receipts). It
specializes `documents` with the genre conventions a
reader of an invoice already expects before opening it.

```
core                    ← principles + abstract component taxonomy
  └── documents         ← paginated-print concretization
        └── invoice   ← THIS (package): totals, address blocks, legal fields, one page
```

This package inherits the paginated-print layer unchanged. It does not
re-derive that print has no hover, that elevation becomes rules and whitespace,
or that the Buttons slot is absent — those are settled above. It adds **only
what an invoice demands**.

## What makes an invoice different

An invoice is read three times by three readers with three goals, and its
design is judged by all three:

1. **A person checks the amount.** They look for one number and expect it to be
   the most prominent number on the page.
2. **A person checks the arithmetic.** They read the totals column downward and
   expect the steps to add up without re-typing anything into a calculator.
3. **A system or auditor checks the fields.** They look for the invoice number,
   the dates, the terms, and the tax identifiers, and expect each to be present
   and findable.

Every obligation in this package serves one of those three readings. That is
also the ordering principle when two obligations conflict: the amount reading
wins over the arithmetic reading, which wins over the field reading.

## What lives here

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::invoice@documents/reference/totals_and_arithmetic.md" /> —
  decimal alignment down the totals column, currency-symbol placement, the
  subtotal → tax → total progression as a readable chain, and the grand total
  carrying the page's heaviest numeric weight.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::invoice@documents/reference/address_and_legal_fields.md" /> —
  sender and recipient block placement and distinction, window-envelope
  compatibility as a physical constraint, postal-format fidelity, and the
  completeness and prominence of the fields the document itself declares.
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::invoice@documents/reference/single_page_pressure.md" /> —
  the widow-page finding: an invoice that breaks to a second page to carry one
  line has failed, and the check is measurable against the rendered page.

## What does NOT live here

- **Paginated-print mechanics** — page geometry, break behavior, footnote
  placement, the print gamut. Those are `documents`.
- **Jurisdictional tax law.** This package does not enumerate which fields a
  given jurisdiction requires. It states the *completeness and prominence*
  obligation for whichever fields the document declares, because a reviewer
  reading a rendered page cannot determine the issuer's jurisdiction and must
  not invent one. See the scope note in
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::invoice@documents/reference/address_and_legal_fields.md" />.
- **Concrete style values** — chosen page size, margins, typeface, the
  `base-font-size`. Those belong to the rendering style the invoice is
  rendered with.

## Selection

This package is opt-in: a session selects it explicitly (the `documents`
profile with the `invoice` package) when the document is an invoice or another transactional document of the same shape. A renderer may
map its own style categories onto the document-type packages; that mapping is
documented by the renderer, not here.
