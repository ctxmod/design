# Appendix Conventions

Appendix conventions for long-form reports — a lettering or numbering scheme distinct from the body, every appendix referenced from the body, and appendices carrying supporting material rather than load-bearing argument.

An appendix is the report's answer to a real tension: material that must be
*available* but would destroy the argument if it were *inline*. A forty-row data
table, a survey instrument, a full regulatory citation — each needs to exist and
none belongs in the middle of a chapter.

That makes an appendix a **deferral with a promise**: the body promises the
material is there, and the appendix keeps the promise. Both halves are
checkable, and each fails in its own way. A body that defers to nothing leaves
the reader looking; an appendix nobody defers to is material that was never
placed.

## Testable obligations

### Identification

- **Appendices use a scheme distinct from the body's section numbering.**
  Letters (`Appendix A`, `A.1`, `A.2`) are the dominant convention and the
  default absent another signal; a distinct numeric range works equally well.
  Continuing the body's numbering into the appendices makes `Section 9` and an
  appendix indistinguishable in a cross-reference.
- **The scheme is sequential and gap-free.** `Appendix A`, `B`, `D` has lost
  one.
- **A single appendix is still labelled.** "Appendix" with no letter is
  acceptable for exactly one; the moment there are two, both take a letter.
- **Sub-elements within an appendix carry the appendix's prefix.** Tables and
  figures inside Appendix B are `Table B.1`, `Figure B.2` — not a continuation
  of the body's float sequence. Otherwise a reader following "see Table 12"
  cannot tell whether to look in chapter 6 or the back.
- **Each appendix starts on a new page and carries a title, not only a letter.**
  `Appendix C` alone tells the reader nothing about whether it holds what they
  are looking for.
- **Appendices appear in the table of contents.** With their letters and their
  titles, at the same depth the TOC gives body chapters.

### Reference

- **Every appendix is referenced at least once from the body.** An appendix no
  prose points to has no entry point: the reader has no signal that it exists
  or when it is relevant.
- **Every in-body appendix reference resolves.** A "see Appendix D" in a
  document with three appendices is a broken address.
- **The reference sits where the deferred material would have gone.** A pointer
  to the survey instrument belongs in the methodology discussion, not only in a
  list at the end. The reference is the promise, and it must be made at the
  point the reader would otherwise want the content.
- **Unresolved markers do not survive into the render.** A visible `??`,
  `\ref{app:x}`, or `Appendix ?` is a build failure, not a convention failure.

### Content boundary

- **An appendix carries supporting material, not load-bearing argument.** A
  claim the report depends on, stated only in an appendix, has been moved out of
  the document most readers read. Data supporting a claim belongs in an
  appendix; the claim does not.
- **A recommendation never appears only in an appendix.** Recommendations are
  the report's output and belong in the body and the executive summary. See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/executive_summary.md" />.
- **The body remains readable without the appendices.** A reader who skips them
  should reach the conclusions with the argument intact. Where a body sentence
  cannot be understood without turning to an appendix, the deferral was made at
  the wrong point.
- **An appendix that has grown into a chapter is a chapter.** Appendix material
  running to a substantial fraction of the body, with its own argument and
  internal structure, is a structural finding: it was deferred to avoid a
  restructuring decision.
- **Appendix data display follows the body's conventions.** Table treatment,
  caption style, and number formatting carry through. See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/cross_chapter_consistency.md" />
  — appendices are the most common place this consistency lapses, because they
  are often assembled last.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Distinct scheme | Compare an appendix heading against a body section heading | The two use the same numbering space |
| Sequential | Read the appendix letters in order | One is skipped or repeated |
| Single appendix labelled | Count the appendices | Two or more exist and any lacks a letter |
| Prefixed sub-elements | Find a table or figure inside an appendix | It continues the body's float sequence |
| New page and title | Look at each appendix opening | It runs on from the previous page, or carries only a letter |
| In the TOC | Read the TOC's tail | Appendices absent, or listed without titles |
| Every appendix referenced | For each appendix, search the body for a pointer | Any is unreferenced |
| Every reference resolves | For each in-body appendix reference, find the appendix | Any has none |
| Reference placed usefully | Find where each appendix is first referenced | Only in a terminal list, not at the point of deferral |
| No unresolved markers | Scan for `??`, `\ref`, `Appendix ?` | Any appears |
| No load-bearing argument | Read each appendix for claims and recommendations | A claim or recommendation appears only there |
| Body readable alone | Read a body section that defers heavily | It cannot be followed without turning to the appendix |
| Appendix not a chapter | Compare appendix length against body length | An appendix approaches a chapter's scale with its own argument |
| Conventions carry through | Compare an appendix table against a body table | Rule treatment, caption style, or number formatting differs |

## Anti-patterns

- Numbering appendices as `Section 9`, `Section 10` continuing the body, so a
  cross-reference cannot tell a reader whether to look forward or back.
- Collecting every appendix reference into a single line at the end of the body
  ("Supporting material appears in Appendices A–F"), which satisfies the letter
  of the reference obligation and none of its purpose.
- Using an appendix as the destination for material that would not survive
  review in the body. The appendix is for volume, not for burial.
- Restarting float numbering inside appendices without a prefix, producing two
  Table 1s in one document.
- Assembling appendices from source documents verbatim and inheriting their
  typography, so the back of the report reads as a different document. This is
  the single most common cross-chapter consistency lapse.
- Reporting an unreferenced appendix without checking the TOC and the front
  matter — a document may legitimately introduce its appendices there, though
  that does not substitute for a pointer at the point of deferral.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/section_hierarchy.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />
