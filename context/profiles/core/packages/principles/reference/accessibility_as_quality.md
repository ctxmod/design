# Accessibility as Quality

Accessibility framed as a measure of design quality — contrast, focus, targets, structure, and multi-channel meaning authored into the design.

Accessibility is not a compliance checklist bolted on at the end. It is a measure
of design quality: an interface that more people can perceive, operate, and
understand is, by definition, a better interface. The same decisions that make a
design accessible — clear contrast, visible focus, generous targets, real
structure — make it more usable and more polished for *everyone*. The frame is
simple: **good design is accessible design.** Treating the two as separate is what
produces designs that are technically compliant and still bad.

This document is about accessibility as a *design lever*. The platform mechanics —
ARIA roles, semantic HTML, focus management code, reduced-motion queries — belong
to the medium tier. The design must be authored so those mechanics have something
correct to express.

## Why it's a quality metric, not a tax

Each accessibility property is also a usability property:

| Accessibility need | Also benefits |
|--------------------|---------------|
| Sufficient contrast | Everyone in sunlight, on bad screens, while tired |
| Visible focus | Keyboard power users, anyone who lost the cursor |
| Large touch targets | Everyone on a phone, on the move, with cold hands |
| Clear text & structure | Skimmers, non-native speakers, the distracted |
| Captions / labels | Everyone in a quiet office or loud room |

Designing for the edge improves the center. This is the "curb-cut effect": ramps
built for wheelchairs help everyone with a cart, stroller, or suitcase.

## Contrast

Contrast is the most common and most consequential failure (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />). Designs that look elegant in a mockup — grey text on grey,
thin low-contrast type — fail real readers. The ratio thresholds derive from the
human contrast-sensitivity function (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />).

Cite the success criteria, not just the ratios:

- **SC 1.4.3 Contrast (Minimum)** — Level AA, the normative floor: body text
  **4.5 : 1** against its actual background; large text (≥ 18 pt ≈ 24 CSS px, or
  ≥ 14 pt ≈ 18.66 CSS px bold — WCAG's "large scale" is defined in points, not
  pixels) **3 : 1**.
- **SC 1.4.11 Non-text Contrast** — Level AA: UI components and graphical objects
  (icons, borders, focus rings, chart strokes, input outlines) **3 : 1**.
- **SC 1.4.6 Contrast (Enhanced)** — Level AAA *(labeled stretch goal, not the
  baseline)*: body text **7 : 1**, large text **4.5 : 1**.
- Verify against the *real* background, including overlays and images.
- Light grey placeholder text often fails contrast — design real labels, don't
  rely on placeholders to carry meaning (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />).

## Focus visibility

Every interactive element must have a clearly visible focus state. A keyboard or
switch user navigates entirely by focus; an invisible focus ring makes the product
unusable for them.

- The focus indicator must have **≥ 3 : 1 contrast** against adjacent colors and
  be unmistakable — a ring, outline, or strong background shift, not a 1px tint
  (**SC 2.4.7 Focus Visible**, Level AA).
- The focused element must not be fully hidden by sticky headers, footers, or
  other overlaying content (**SC 2.4.11 Focus Not Obscured (Minimum)**, Level AA,
  *new in WCAG 2.2*); keeping it fully unobscured is **SC 2.4.12**, Level AAA.
  Account for sticky chrome when authoring scroll-into-view and focus behavior.
- Never remove focus outlines without replacing them with something better.
- Focus order must follow the visual/reading order (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />); a logical layout produces a logical
  tab order.
- This is a *design* responsibility: specify the focus treatment for every
  component as a first-class state (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />).

## Target sizes

Interactive targets must be large enough to hit reliably. The two WCAG criteria
are distinct conformance levels — don't conflate them:

- **SC 2.5.8 Target Size (Minimum)** — Level AA, the normative floor: **24×24 px**
  (with exceptions for inline targets, spacing, and equivalents).
- **SC 2.5.5 Target Size (Enhanced)** — Level AAA *(labeled stretch goal)*:
  **44×44 px**. This is the comfortable, mobile-proven target; aim here for primary
  touch controls, but it is *not* the AA baseline.
- Small visual elements (a 16px icon button) need adequate *padding* to reach the
  target size even if the glyph is small.
- Maintain spacing between adjacent targets so users don't mis-tap (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />).

## Pointer input

Operation must not depend on a single complex pointer interaction:

- **SC 2.5.1 Pointer Gestures** — Level A: anything driven by a multipoint or
  path-based gesture (pinch, swipe-along-a-path) must also be operable with a
  single-pointer action (tap, click).
- **SC 2.5.7 Dragging Movements** — Level AA, *new in WCAG 2.2*: any function that
  uses dragging (reorder, slider, drag-to-dismiss) must offer a single-pointer
  alternative that is not a drag (e.g. tap-target buttons, a numeric input).
  Design the non-drag path as a first-class affordance, not a fallback.

## Help, re-entry, and authentication (new in WCAG 2.2)

Three of WCAG 2.2's nine new criteria are about *flows*, not pixels, and are
easy to miss because no contrast or focus check surfaces them:

- **SC 3.2.6 Consistent Help** — Level A: where help mechanisms (contact
  details, a help link, a chat) repeat across pages, they appear in the same
  relative order.
- **SC 3.3.7 Redundant Entry** — Level A: information the user already gave in
  the same process is auto-populated or selectable, not re-typed (except for
  security or when the earlier value is no longer valid).
- **SC 3.3.8 Accessible Authentication (Minimum)** — Level AA: no step of
  sign-in relies on a cognitive function test (remembering a password,
  transcribing a code, solving a puzzle) unless an alternative, a mechanism to
  assist (paste and password-manager autofill allowed), object or personal
  content recognition is available. Never block paste into credential fields.

WCAG 2.2 also made **SC 4.1.1 Parsing** obsolete — it is no longer a failure
condition, though work held to WCAG 2.0/2.1 may still need to report it.

## Readability

Readability is an accessibility property:

- Body text large enough to read comfortably (≈ 16px floor on the web; smaller is
  a barrier).
- Comfortable measure (45–75 characters) and line height (≈ 1.5 for body) — see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />.
- Plain, specific language. Clear copy is an accessibility feature; jargon and
  vagueness exclude people.
- Don't justify body text to hard edges (rivers of whitespace hurt dyslexic
  readers); avoid long runs of all-caps.

## Don't encode meaning in one channel

Information must survive the loss of any single perceptual channel:

- **Not color alone.** Error/success/selected states need an icon, label, shape,
  or position in addition to color, so color-blind users perceive them (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />).
- **Not motion alone.** Anything communicated by animation must also be readable
  when motion is removed (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).
- **Not position alone** where it can be missed by assistive tech — pair it with a
  label.

## Structure as a design lever

Semantic structure is something the designer *designs*, not just something the
engineer codes:

- A real **heading hierarchy** (one h1, nested h2/h3 in order) is the same thing as
  a clear visual hierarchy. Design them together so the visual and semantic order
  match (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />).
- **Landmark regions** (header, nav, main, footer) come from a clear page
  composition (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" />). A
  well-structured layout is automatically more navigable for screen readers.
- **Labels and names** for every control are content decisions: name things by
  what the user does, consistently (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/information_architecture.md" />).
- **States must be perceivable** — disabled, selected, loading, expanded — not just
  styled. Designing the visible state and the announced state together is what
  makes a component complete.

## Build to a quality floor, quietly

Accessibility is part of the definition of "done," not a separate pass. The
conformance position is explicit: **WCAG 2.2 Level AA is the normative floor;
Level AAA criteria are labeled stretch goals**, applied where they fit, never
presented as the baseline (do not, for example, treat the 44px AAA target as a
requirement). Cite the [WCAG 2.2 specification](https://www.w3.org/TR/WCAG22/)
for the authoritative criterion text.

### Standards currency (checked 2026-11-23)

- **WCAG 2.2** is the current W3C Recommendation (first published 2023-10-05;
  current edition 2024-12-12) and is also **ISO/IEC 40500:2025** (W3C
  announcement 2025-10-21), which lets national rules cite it directly.
- **WCAG 3.0** is a Working Draft (latest 2026-09-10). It is not a standard,
  W3C states WCAG 3 does not replace or deprecate WCAG 2, and its content will
  change — never present a WCAG 3 draft method (scoring, a new contrast
  algorithm such as APCA) as a conformance requirement.
- **EN 301 549**, the European harmonised standard legal regimes point at, was
  published as **V4.1.1 on 2026-09-02**, adopting WCAG 2.2 Level AA for web,
  non-web documents and software, plus requirements WCAG does not have. It
  confers presumption of conformity only once the European Commission cites it
  in the Official Journal; until then **V3.2.1 (WCAG 2.1 AA)** stays the cited
  reference. Treat any legal-conformance claim as tied to the cited edition,
  and the jurisdiction-specific detail as a medium/locale profile's concern.

The design floor (WCAG 2.2 AA) is therefore ahead of, and compatible with, the
legal floor (WCAG 2.1 AA via EN 301 549 V3.2.1) until V4.1.1 is cited.

- Responsive down to small screens.
- Visible keyboard focus on every interactive element.
- Reduced motion respected.
- Contrast verified, not assumed.
- Real labels, real structure, real states.

### How to verify: convergent vs. divergent checks

**Automated tools detect only ~25–30% of WCAG criteria.** Split verification
accordingly:

- **Convergent** (automate well — run them in CI): contrast ratios
  (SC 1.4.3 / 1.4.6 / 1.4.11), keyboard operability and focus visibility
  (SC 2.4.7), and screen-reader semantics (heading order, landmark roles,
  accessible names). These have deterministic pass/fail signals.
- **Divergent** (need manual review — a tool cannot judge them): correctness of
  ARIA patterns and announced state, pointer-gesture and dragging alternatives
  (SC 2.5.1 / 2.5.7), focus-not-obscured behavior under sticky chrome
  (SC 2.4.11 / 2.4.12), help placement and multi-step flows (SC 3.2.6 /
  3.3.7 / 3.3.8 — walk the real sign-in and form journeys), and whether meaning
  genuinely survives the loss of a single channel. Budget for keyboard-only and screen-reader walkthroughs.

Hit this floor without announcing it. It is included in the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_review.md" /> precisely because
a beautiful design that fails it is not finished.

## Sources

- https://www.w3.org/TR/WCAG22/ — WCAG 2.2 Recommendation (edition 2024-12-12): "large scale" definition (18 pt / 14 pt bold), SC 3.2.6, 3.3.7, 3.3.8, 4.1.1 obsolete; accessed 2026-11-23
- https://www.w3.org/WAI/news/2025-10-21/wcag22-iso — WCAG 2.2 approved as ISO/IEC 40500:2025, 2025-10-21; accessed 2026-11-23
- https://www.w3.org/standards/history/wcag-3.0/ — WCAG 3.0 publication history, latest Working Draft 2026-09-10; accessed 2026-11-23
- https://nda.ie/news/en301549-published — EN 301 549 V4.1.1 published 2026-09-02, references WCAG 2.2 AA, binding only after OJEU citation, V3.2.1 in force until then; accessed 2026-11-23
- https://www.deque.com/blog/en-301-549-v4-1-1-is-final-what-changed-what-it-means-and-what-you-should-do/ — V4.1.1 changes and citation-date uncertainty (2026-09-08, updated); accessed 2026-11-23
