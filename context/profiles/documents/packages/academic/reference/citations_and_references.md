# Citations and References

Citation and reference formatting for scholarly documents — one citation system applied consistently, bidirectional resolution between in-text citations and the reference list, and the alignment and hanging-indent treatment that makes a reference list scannable.

Which citation style to adopt and how to write citations is owned by
`github.com/ctxmod/writing_academic/context` (profile `core`, package `citations`,
and profile `scholarly_prose`, package `citation_practice`). This file covers the
typographic and layout side: consistency, resolution, and reference-list setting.

A scholarly document's citations are its **edges to other documents**. Unlike
almost everything else on the page, a citation is judged by whether it
*resolves*: the reader must be able to move from a mark in the prose to a full
entry, and from that entry to the cited work. A citation that cannot be
followed has failed regardless of how well it is set.

The reference list is the other end of that edge, and it is read differently
from the body: scanned for an author name or a year, not read in sequence. Its
typography must serve a lookup, which is why the hanging indent — a device that
appears nowhere else in the document — is the convention.

## Testable obligations

### System consistency

- **One citation system is used throughout.** Author-date (`(Doe 2024)`),
  numeric (`[12]`), and note-based (a superscript keyed to a footnote) are all
  correct; mixing them within one document is not. A single stray form is a
  finding.
- **The in-text form is uniform.** Bracket style, the presence or absence of a
  comma between author and year, the treatment of multiple authors and of
  `et al.`, and the separator between multiple citations in one parenthesis are
  all applied the same way at every occurrence.
- **Page-locator formatting is uniform.** If the document cites specific pages,
  the locator's separator and prefix (`, p. 14` / `:14` / `, 14`) are the same
  every time.
- **The reference list's entry format is uniform per source type.** Every
  journal article follows the same field order, punctuation, and emphasis
  treatment as every other journal article; the same holds within books,
  chapters, and web sources. Different source types may differ from each other.

### Bidirectional resolution

- **Every in-text citation resolves to a reference-list entry.** A mark in the
  prose with no corresponding entry is a broken edge and a finding at full
  severity.
- **Every reference-list entry is cited at least once in the body.** An
  uncited entry is either a leftover or a bibliography masquerading as a
  reference list. Where the document declares a *bibliography* (works consulted)
  rather than a *reference list* (works cited), this obligation is waived — but
  the document must say which it is.
- **Unresolved markers do not survive into the render.** A visible `[?]`,
  `(author year)`, `\cite{key}`, `??`, or a bare citation key is a render
  failure, not a formatting one.
- **Numbering, where numeric, is sequential and gap-free.** A numeric system
  numbering `[1] [2] [4]` has lost an entry.

### Reference-list typography

- **Entries use a hanging indent.** The first line sits at the left margin and
  continuation lines are indented, so the author names form a scannable
  left-hand column. This is the dominant convention and the default to apply
  absent another signal; a numbered list may instead align continuation lines
  to the text after the number, which serves the same scan.
- **The entry-separating space exceeds the intra-entry line spacing.** A reader
  must be able to see where one entry ends and the next begins without reading
  the words.
- **Long URLs and DOIs do not break the measure.** They wrap, or the measure
  accommodates them; a URL running into the margin is a finding.
- **Ordering is consistent with the system.** Author-date lists are ordered
  alphabetically by first author; numeric lists are ordered by first citation or
  alphabetically, but not by both.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| One system | Sample citations from the first, middle, and last thirds of the body | Two forms appear |
| In-text form uniform | Collect every citation on a sampled page; compare bracket, separator, and `et al.` treatment | Any differs |
| Locator uniform | Collect every page-locator citation | Separator or prefix varies |
| Entry format uniform | Compare three entries of the same source type | Field order, punctuation, or emphasis differs |
| Citations resolve | For each sampled in-text citation, find its entry | Any has none |
| Entries cited | For each sampled entry, find a citation | Any is uncited and the list is declared as references |
| No unresolved markers | Scan the rendered pages for `[?]`, `??`, `\cite`, or a bare key | Any appears |
| Numbering gap-free | Read the numeric sequence in the reference list | A number is skipped or repeated |
| Hanging indent | Look at the left edge of the reference list | Continuation lines start at the same x as first lines |
| Entry separation visible | Squint at the reference list | Entry boundaries are indistinguishable from line breaks |
| URLs contained | Check the right margin through the reference list | A URL crosses it |
| Ordering consistent | Read the first field of consecutive entries | The ordering rule changes partway |

## Anti-patterns

- Reporting a document for using a citation system the reviewer does not prefer.
  The obligation is consistency, not conformity to a chosen manual.
- Justifying the reference list, which opens rivers between the short tokens
  that make up a citation entry and destroys the left-column scan the hanging
  indent creates. Reference lists are set ragged-right.
- Treating a visible `\cite{doe2024}` as a citation-formatting finding. It is a
  build failure: the citation processor did not run, and reporting it as a style
  issue misdirects the fix.
- Setting the reference list at the same leading and spacing as the body, so it
  reads as a paragraph block rather than as a lookup table.
- Flagging an uncited entry in a document whose list is explicitly titled
  "Bibliography" or "Further reading" — the waiver above exists for exactly this.
- Hyphenating URLs to make them fit, introducing a hyphen a reader cannot
  distinguish from one that belongs to the address.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/floats_and_numbering.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::academic@documents/reference/footnote_density.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />
