# Confidence / Evidence Note

Charter section 5 for the paginated-print medium — what is validated (print typography and legibility) versus extrapolated (the web-derived umbrella mapped onto print), the sampled and role-heuristic limits of automated document review, and the ISO 9241-110 drop justifications.

This is **section 5 of the five the medium charter makes mandatory**. It states,
honestly, where this profile's guidance is **validated** by medium-specific
evidence and where it is **extrapolated** from the umbrella by analogy.

The note is honest, not paralyzing. An extrapolated guideline is still
actionable; the flag tells a reader how much weight to put on it and where
medium-specific validation would most improve the profile.

## Validated: print typography and legibility

This medium is unusual among the non-web media in having a **deep, independent
evidence base** that predates the web entirely.

- **Typographic practice** — measure, leading, the relationship between type
  size and line length, the recto/verso relationship, the margin proportions
  that make a book comfortable to hold and read — is centuries of accumulated,
  refined craft with a large body of written record. It was not derived from
  screen design; screen design derived from it.
- **Legibility research is measured, not inferred.** Reading speed,
  comprehension, and fixation behavior as functions of type size, x-height,
  measure, and leading have been studied directly on print, at print reading
  distances, since well before digital typesetting.

The parts of this profile that rest on that base and are therefore
**validated**:

- The 10–12pt body band and the ~8pt annotation floor
  (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/affordance_adaptation.md" />).
- Page-in-hand viewing distance at 30–40cm and its consequences for sizing.
- The comfortable density default and the role of margins as a handling and
  measure-bounding instrument.
- The type-scale mechanism itself — a base size with per-role ratios — which is
  how typeset documents have always been specified.
- The subtractive-gamut and ink-coverage constraints in
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/token_translation.md" />,
  which are press facts.

## Extrapolated: the umbrella mapped onto print

The umbrella's principles were largely synthesized from **web** research, WCAG,
and APG — the charter says as much when it names `web` the calibration
baseline. Mapping that corpus onto print is therefore an **analogy**, and the
following are flagged as extrapolated:

- **The slot mapping as a whole.** Mapping the umbrella's component taxonomy
  onto page primitives is a structural analogy. It is defensible and internally
  consistent, but there is no print-native "component taxonomy" literature that
  independently arrives at these eight slots. The four *absences* are the
  best-supported part (they follow from the medium having no runtime, which is
  not in doubt); the four *mappings* are the more speculative part.
- **Elevation → rules and whitespace.** The substitution is sound in that print
  has no z-axis, but "which rule weight corresponds to which elevation step" is
  an invented correspondence, not a measured one.
- **Page-position weight as a hierarchy channel.** That top-of-page is stronger
  than mid-page is consistent with serial-position and scan-path findings, but
  the specific claim is extrapolated from those, not measured on documents.
- **The spread as a compositional unit.** Well established as *craft* — book
  designers have always designed spreads — but its expression as an umbrella
  `composition` adaptation is this profile's framing.
- **The ISO 9241-110 classifications** in the capability declaration. ISO
  9241-110 is written for interactive systems; applying its seven dialogue
  principles to a static artifact is an extrapolation the charter invites but
  does not validate.

Where a validated and an extrapolated claim conflict, **the validated one
wins.** If the slot mapping's framing of a table would push type below the
legibility floor, the floor holds.

## Limits of automated document review

Two limits are properties of how automated document review gathers evidence
(sampled components and sections, and role-heuristic region extraction), not
of the guidance above. Both bound what a clean review result can be taken to mean.

### Evidence is sampled, not exhaustive

Review evaluates **representative component and section samples** — three
components and three sections, for example — rather than every page and every
occurrence.

The consequence is directional and must be stated plainly: **a clean review
does not establish that the document is clean.** A defect present only in an
unsampled occurrence is missed. If a document has forty tables and three are
examined, a broken alignment in the thirty-seventh is invisible to the review.

What a clean review *does* establish is that the sampled representatives are
clean, which is meaningful evidence about systematic defects — a template-level
error tends to appear in every instance and so is very likely to be sampled.
The limit bites hardest on **localized, one-off defects**: a single overfull
line, one figure that broke to the wrong page, one table whose header did not
repeat.

Raising the sample count narrows the gap and does not close it. Reviewers and
readers of review output should treat findings as **existence proofs** (this
defect is present) and non-findings as **absence of evidence** (this defect was
not observed in the sample), never as absence of the defect.

### `role-heuristic` extraction cannot see custom component types

In `role-heuristic` extraction mode, regions are classified by their **rendered
role** — heading, table, paragraph, list, figure — inferred from layout and
typographic evidence on the page. That is all the mode has to work with, and it
produces two specific blind spots:

- **It cannot distinguish custom component types.** A region that the author
  authored as a `<totals>` component is indistinguishable from a plain table:
  both render as an aligned grid of numbers. The mode reports "table". Any
  obligation that depends on knowing *which* component a region is — an
  invoice's totals-arithmetic legibility rules, for example — cannot be
  evaluated from role-heuristic evidence alone.
- **It cannot reliably distinguish heading levels.** Level inference rests on
  relative size and weight, which collide as soon as two adjacent levels sit
  close on the type scale — an h2 at `size: 1.15` and an h3 at `size: 1.0` are
  separated by 1.65pt in an 11pt document. Findings about *section hierarchy
  depth* are therefore weaker in this mode than findings about the visual
  treatment of a heading.

Neither limit affects findings about things the page image shows directly:
type size, measure, leading, contrast, alignment, margins, float placement,
page breaks, and the presence of running heads and folios are all fully
observable in role-heuristic mode.

## ISO 9241-110: justifying the unavoidable drops

The charter holds the seven dialogue principles exempt from casual dropping and
requires that any unavoidable drop be justified here. The capability declaration
records three that are not fully supported. Each is justified below.

**Controllability — adapted, weakly.** The reader does set the pace: they turn
pages when ready, re-read at will, and enter at any point through the TOC or
index. Random access across the whole artifact is, in one sense, *more* complete
than a paginated web view offers. But this is **reader-side navigation, not a
system responding to direction** — the document does not change in response to
anything the reader does, and every affordance it offers was fixed at typeset
time. It is a real form of control and a weak one, and calling it fully
supported would overstate the medium.

**Suitability for individualization — dropped.** The rendering is fixed when the
document is typeset. There is no mechanism by which a reader adapts type size,
contrast, density, or layout to their needs or abilities. This is the most
consequential of the three drops, because it is an **accessibility** drop: a
reader who needs larger type cannot get larger type from the artifact. The
mitigation is upstream and belongs to whoever commissions the document — issue a
large-print rendering, or ship a reflowable format alongside the paginated one.
Within the medium there is no mechanism, and this profile does not pretend
otherwise.

**Error tolerance — dropped.** The principle concerns preventing user errors and
making them recoverable. There is no user input to be in error and no operation
to recover from, so the principle has nothing to bind to. One adjacent obligation
is *not* dropped and should not be conflated with it: **preventing reader
misreading** — disambiguating similar figures, avoiding tables that continue
across a page break without repeating headers, making cross-references resolve —
is live here and is carried by
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/slot_mapping.md" /> and the
umbrella's typography obligations. What is dropped is *interaction* error
tolerance, not care for the reader.

## Where medium-specific validation would help most

Ranked by how much it would improve this profile:

1. **The elevation → rule-weight correspondence.** Currently invented. A small
   study of perceived separation by rule weight and whitespace on paper would
   replace an analogy with a measurement.
2. **Page-position weight.** Whether and how much top-of-page and recto
   placement raise perceived importance is empirically answerable and currently
   extrapolated.
3. **The slot mapping's four mapped slots.** Whether page/column/float/sidenote
   is the right decomposition of "layout containers" for review purposes is a
   framing choice that document-review practice could confirm or revise.

## Testable obligations

- **Every finding cites a mechanism.** A finding whose only support is "this
  looks wrong" is not reportable regardless of confidence tier.
- **A finding resting on an extrapolated claim says so** and is reported at
  lower severity than an equivalent finding resting on a validated one.
- **No review output states or implies that the document is defect-free.** The
  sampled-evidence limit forbids it.
- **No finding depends on knowing a region's custom component type** when the
  extraction mode is `role-heuristic`.
- **No finding is raised for missing individualization, error tolerance, or
  interactive controllability.** All three are justified drops above.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Findings cite a mechanism | Read each finding's stated cause | It names no principle, threshold, or measurement |
| Extrapolated claims flagged | Match the finding's basis against the extrapolated list | An extrapolated basis is reported at the same severity as a measured one |
| No clean-document claim | Read the review's summary language | It asserts the document is clean, correct, or free of defects rather than that the sample was |
| No custom-type dependence in `role-heuristic` | Read the finding's premise | It asserts a region is a specific custom component |
| Justified drops unreported | Read each finding's cited dialogue principle | It cites individualization, error tolerance, or interactive controllability |

## Anti-patterns

- Reporting "no issues found" as "the document is well designed". The sample
  does not support the generalization, and the overstatement is exactly what
  erodes trust in review output.
- Raising a totals-arithmetic finding from `role-heuristic` evidence. The mode
  cannot tell a totals component from a table, so the premise is unfounded even
  when the conclusion happens to be right.
- Presenting an extrapolated claim — an elevation-to-rule-weight mapping, a
  page-position weighting — with the same confidence as the 10–12pt body band.
  One is measured; the other is an analogy this profile authored.
- Suppressing a validated legibility finding because an extrapolated framing
  claim points the other way. Validated wins.
- Treating the individualization drop as a reason to ignore accessibility. The
  drop is about the *mechanism*; contrast, type size, reading order, and tagged
  structure are all live obligations under the adapted
  `accessibility-as-quality` classification.
- Omitting this note, or reducing it to "guidance is extrapolated". The charter
  requires the split to be specific enough that a downstream agent can tell
  which claims to lean on.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::print@documents/reference/capability_declaration.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/medium_charter.md" />
