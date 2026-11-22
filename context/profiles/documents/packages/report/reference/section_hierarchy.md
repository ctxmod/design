# Section Hierarchy Depth

Section hierarchy depth for long-form reports — how deep the numbered hierarchy runs before it stops aiding navigation, and whether adjacent heading levels are visually distinguishable from one another.

A numbered hierarchy is a **navigation aid**, and like every navigation aid it
has a working range. Within that range a number like `3.2` tells a reader where
they are and how to get back. Past it, `4.2.3.1.2` tells the reader only that
the document has more structure than they can hold, and they stop reading the
numbers.

Depth also has a structural meaning. A section that needs a fourth or fifth
numbered level is usually not one section with fine structure — it is several
sections that were never promoted. The depth is the symptom; the unpromoted
material is the cause.

## Testable obligations

### Depth

- **Three numbered levels is the working range.** `1`, `1.2`, `1.2.3` are
  legible as addresses and hold in working memory. A fourth level (`1.2.3.4`) is
  a signal worth reporting; a fifth is a finding.
- **A fourth level is reported as a structural signal, not a rule violation.**
  The claim is that the material at that depth probably wants promoting — the
  subsection becoming a section, or the section becoming a chapter. State where
  it occurs and how much of the document sits at that depth.
- **Depth is uniform across the document.** A report whose chapter 2 runs three
  levels and chapter 6 runs five has an inconsistency independent of the depth
  itself. Compare across chapters, not within one.
- **Unnumbered subheadings below the deepest numbered level are the intended
  escape hatch.** A run-in bold lead-in or an unnumbered subheading gives fine
  structure without extending the address space, and using it is conforming, not
  a workaround.
- **The table of contents reflects the hierarchy at a usable depth.** A TOC
  listing every level to depth five is a second navigation problem; a TOC
  truncated to two levels in a three-level document hides a level the body
  numbers. The TOC's depth is a deliberate choice consistent with the body's.

### Distinguishability

- **Adjacent heading levels are distinguishable without reading the number.**
  Size, weight, case, face, space-above, or rule — some channel separates level
  2 from level 3 at a glance. A reader must be able to tell a subsection start
  from a sub-subsection start on a page they did not enter at the top of.
- **The channel used is consistent per level across the document.** Level 3 is
  the same treatment in chapter 7 as in chapter 2. See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/cross_chapter_consistency.md" />.
- **Space-above exceeds space-below for every heading level.** A heading binds
  to the content that follows it; equal or inverted spacing detaches it and
  makes the hierarchy unreadable regardless of the type treatment.
- **The steps between levels are monotone.** Each deeper level is smaller,
  lighter, or less prominent than the one above — never equal, never larger.
  Two levels at the same size distinguished only by italic is a weak step, and
  weak steps compound with depth.
- **A heading is not orphaned at a page foot.** A level-2 or level-3 heading
  with fewer than two lines of its content beneath it has broken the binding
  the space-above obligation establishes.

## How to verify

| Obligation | Check | Flag when |
|---|---|---|
| Depth within range | Find the deepest numbered heading in the TOC or the body | A fifth level exists; a fourth level exists and carries substantial content |
| Depth uniform | Compare the deepest level used per chapter | Chapters differ by more than one level |
| Escape hatch used | Look at fine structure below the deepest numbered level | It is numbered rather than set as unnumbered subheadings |
| TOC depth deliberate | Compare TOC depth against body depth | The TOC omits a level the body numbers, or lists a level too fine to scan |
| Levels distinguishable | Cover the numbers on a sampled page; identify each heading's level | Two adjacent levels are indistinguishable |
| Treatment consistent | Compare the same level's treatment in an early and a late chapter | They differ |
| Space above > below | Measure the gap above and below a heading | Below is equal or greater |
| Monotone steps | Rank the heading levels by visual weight | Any deeper level ties or outranks a shallower one |
| No orphaned headings | Check each page foot | A heading sits with fewer than two lines beneath it |

## Anti-patterns

- Reporting a fourth level as a hard rule violation. The document may have a
  genuine reason; the finding is a structural signal and reads as one only if it
  says what the material at that depth should become.
- Distinguishing level 3 from level 2 by number alone — same size, same weight,
  same spacing — so the hierarchy exists in the TOC and nowhere on the page.
- Adding depth to a heading treatment by making level 3 italic at the same size
  as level 2, then discovering level 4 needs a step and having no channel left.
  Depth budget and treatment budget run out together.
- Setting generous space below headings to "give them room", which visually
  binds each heading to the content above it and inverts the whole structure.
- Judging depth from one chapter. Depth uniformity is a cross-chapter property
  and a single sample cannot show it.
- Truncating the TOC to one level to keep it to a page, in a document whose
  readers enter at section level.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::report@documents/reference/appendix_conventions.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />
