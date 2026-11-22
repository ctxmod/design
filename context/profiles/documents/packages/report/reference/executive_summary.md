# Executive Summary

Executive-summary placement for long-form reports — front-loaded ahead of the body, self-contained so it reads without the body, and bounded in length relative to the document.

The executive summary exists because **most of a report's readers will not read
the report**. It is not an introduction and not an abstract: an introduction
prepares a reader for the body, and an abstract describes what the document
contains. A summary substitutes for the body — it states the findings and the
recommendations, in full enough form that a reader who stops there has the
document's answer.

That substitution is what generates every obligation below. A summary that must
be supplemented by the body has not substituted for it.

## Testable obligations

### Placement

- **The summary precedes the body.** It sits after the title block and any
  contents apparatus, and before the first numbered body section. A summary
  placed after the introduction, or at the end as a conclusion, is not
  performing this role.
- **It is reachable without the table of contents.** A reader opening the
  document lands on or immediately before it. In practice this means the first
  or second spread.
- **It is visually marked as summary, not as section 1.** A distinct heading
  treatment, a rule, a tinted region, a different measure, or an unnumbered
  heading — some channel says "this is the summary" rather than "this is the
  first thing".
- **Where the summary is numbered, the numbering does not put it inside the
  argument.** An unnumbered summary is the conventional treatment. A summary
  numbered as section 1 makes the body's section 2 the introduction, which
  distorts the hierarchy the rest of the document depends on.

### Self-containment

- **It states findings and recommendations, not the document's structure.** A
  summary reading "Section 3 examines the data; Section 4 draws conclusions" is
  a table of contents in prose. The reader wants the conclusions.
- **It reads without the body.** No reference to a numbered float, no
  cross-reference to a section as the carrier of a claim, no abbreviation
  defined only in the body, no dependency on a definition introduced later.
- **Where it references the body, the reference is a pointer to detail, not a
  substitute for content.** "See section 4 for the methodology" is conforming;
  "the three drivers are analyzed in section 4" is not — it withholds the three
  drivers.
- **Its claims are consistent with the body's.** A number in the summary
  matches the number in the body it summarizes. Divergence is the most
  damaging failure this principle covers, because the summary is the part that
  gets quoted.

### Bounds

- **The summary is bounded relative to the document.** Roughly one page for a
  report of twenty to fifty pages, and not more than about a tenth of the body
  for longer ones. A summary running past that has begun re-arguing rather than
  summarizing.
- **It is not a stub.** A single paragraph in front of a hundred-page report
  cannot carry the findings, and the reader who stops there leaves with
  nothing.
- **It is set to be read, not scanned into.** Body-size type, a normal measure,
  and paragraph structure. A summary compressed into a dense sidebar or reduced
  type is the one part of the report that must not be typographically
  subordinate.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Precedes the body | Find the summary and the first numbered body section | The summary follows it |
| Reachable | Note the page the summary starts on | It starts past the second spread |
| Marked as summary | Squint at its opening page | It is indistinguishable from a body section opening |
| Numbering does not distort | Read its heading | It is numbered as section 1 with the introduction as section 2 |
| States findings | Read it alone | It describes the document's structure instead of its conclusions |
| Self-contained | Read it alone; list every term, number, and reference | Any requires the body to interpret |
| References are pointers | Find every cross-reference in it | One withholds a finding by deferring to a section |
| Claims consistent | Compare each figure in the summary against its body source | Any differs |
| Bounded | Measure summary length against body length | It exceeds roughly a tenth of the body |
| Not a stub | Compare summary length against document length | One paragraph fronting a long report |
| Set to be read | Compare its type size and measure against body text | It is reduced or compressed relative to the body |

## Anti-patterns

- Writing a summary that summarizes the *report* rather than the *findings*:
  "This report examines X, presents Y, and concludes with Z." The reader
  already knows a report exists.
- Placing it after the introduction, which forces the reader who wanted the
  answer to read the setup first — precisely the reader the summary exists for.
- Deferring the headline number to the body ("the cost impact is quantified in
  section 5") on the grounds that the summary should be short. Length is not the
  constraint that matters; substitution is.
- Setting it at a reduced size to fit one page, making the document's most-read
  page its least legible.
- Letting the summary's numbers drift from the body's during revision. The
  summary is written first and edited last, and the mismatch is the predictable
  result — check it explicitly rather than assuming it.
- Treating an abstract as an executive summary in a report that has both. They
  answer different questions and a document carrying both should show the
  difference.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/section_hierarchy.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/appendix_conventions.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />
