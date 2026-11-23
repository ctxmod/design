# Accessible PDF Output

When a paginated document ships as a PDF that people will read on screen — published on a site, attached to a decision, sent to a customer — the adapted `accessibility-as-quality` obligation ("tagged-PDF structure where the output format carries one") becomes concrete: the file carries a logical structure tree, not just ink positions.

The capability declaration classifies accessibility as **adapted** for print: no
focus, no hit targets, but legibility, reading order and structure survive. A
PDF is where that surviving substance is either encoded or lost. A visually
perfect page with no tags reads to a screen reader as an unordered stream of
glyphs — headings indistinguishable from body, tables flattened, figures
silent.

## What the standards ask (checked 2026-11-23)

- **PDF/UA** is the accessibility profile of PDF: **PDF/UA-1** (ISO 14289-1)
  for PDF 1.7 files, **PDF/UA-2** (ISO 14289-2:2024, published 2024-03) for
  **PDF 2.0** (ISO 32000-2:2020) files. PDF/UA-2 does not replace PDF/UA-1;
  pick the part that matches the PDF version emitted.
- **EN 301 549 clause 10** (non-web documents) applies WCAG success criteria to
  documents; V4.1.1 (published 2026-09-02, awaiting Official Journal citation)
  moves that mapping to WCAG 2.2. European public-sector law covers office
  file formats on public sites published since 2018-09-23 (earlier ones only
  when needed for active administrative processes).
- **Not every document needs it.** A print-only artefact (a poster, a mailed
  letter) is judged on ink legibility alone; the PDF obligations attach to
  documents distributed for screen use.

## The structure a tagged document must carry

Each item maps an umbrella obligation onto the PDF structure tree:

| Umbrella obligation | PDF expression |
|---|---|
| Heading hierarchy = visual hierarchy | Heading tags in order, no skipped levels; the outline (bookmarks) mirrors them |
| Unambiguous reading order | Tag order follows the logical order; running heads, folios and decorative rules are artifacts, not content |
| Tables carry header relationships | Table, row, header-cell and data-cell tags; header cells scoped; repeated headers on continuation pages are artifacts |
| Figures carry meaning | Alternative text on informative figures; decorative ones marked as artifacts |
| Language is declared | Document language set, with spans for passages in another language |
| Links and cross-references work | Link annotations tied to their tagged text |
| Text is real text | Fonts embedded with a Unicode mapping, so extraction and reflow return the words |

Colour, contrast and type size remain governed by the umbrella colour and
typography principles; tagging adds structure, it does not rescue an illegible
page.

## Producing it from LaTeX

The LaTeX Project's tagging work states that the LaTeX core now produces
PDF/UA-2-conforming documents; package coverage is still uneven. The current
switch is the `\DocumentMetadata` declaration before `\documentclass`, with
tagging turned on explicitly: since the 2025-11-01 LaTeX release the declaration
always loads the tagging modules, but `tagging` (`on` / `off` / `draft`) decides
whether a structure tree is written, and `pdfstandard=ua-2` sets only XMP
metadata — it does not activate tagging and belongs with PDF 2.0:

```latex
\DocumentMetadata{lang=en, pdfversion=2.0, pdfstandard=ua-2, tagging=on}
\documentclass{article}
```

- LuaLaTeX is the engine the tagging project's usage guidelines (for LaTeX
  2026-06-01 and 2025-11-01) prefer for new documents; it can also emit MathML
  for formulas automatically.
- Check each package a style loads against the published tagging-status data
  (the `latex-tagging-status` package, queried with
  `\DocumentMetadata{check-tagging-status}`); a package without tagging support
  can silently drop structure for the content it typesets.
- Treat a claim of PDF/UA conformance as a validation result, not a build flag:
  run a PDF/UA validator over the output, then spot-check reading order with a
  screen reader.

## Testable obligations

| Obligation | How to check | Fails when |
|---|---|---|
| The PDF is tagged | Inspect the document catalog for a structure tree and marked-content flag | No structure tree, or tags only on a fraction of pages |
| Declared standard matches the file | Compare the PDF/UA part in the metadata with the PDF version | PDF/UA-2 declared on a PDF 1.7 file, or vice versa |
| Heading tags match the visual hierarchy | Extract the tag tree and compare with the section structure | Levels skipped, or headings tagged as paragraphs |
| Page furniture is artifact | Read the tag order across a page break | Running heads or folios appear inside the reading order |
| Validator passes | Run a PDF/UA validator | Any failure left unreported |

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/capability_declaration.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />

## Sources

- https://www.iso.org/standard/82278.html — ISO 14289-2:2024 (PDF/UA-2), edition 1, 2024-03, use of ISO 32000-2; accessed 2026-11-23
- https://tagging-project.latex-project.org/documentation — LaTeX core produces PDF/UA-2-conforming documents; package support is the current focus; accessed 2026-11-23
- https://tug.ctan.org/macros/latex/required/latex-lab/documentmetadata-support.dtx — `\DocumentMetadata` keys: modules always loaded from 2025-11-01, `tagging=on|off|draft`, `pdfstandard` sets only XMP metadata, `check-tagging-status`; accessed 2026-11-23
- https://latex3.github.io/tagging-project/documentation/usage-instructions — usage guidelines for LaTeX 2026-06-01 / 2025-11-01: LuaLaTeX preferred, example `\DocumentMetadata` lines; accessed 2026-11-23
- https://ctan.org/pkg/latex-tagging-status — per-package tagging-support classification read by `check-tagging-status`; accessed 2026-11-23
- https://eur-lex.europa.eu/eli/dir/2016/2102/oj/eng — Web Accessibility Directive Art. 1(4)(a) office-file exemption before 2018-09-23 and recital 26; accessed 2026-11-23
- https://nda.ie/news/en301549-published — EN 301 549 V4.1.1 (2026-09-02) moves the non-web document clauses to WCAG 2.2 AA; accessed 2026-11-23
