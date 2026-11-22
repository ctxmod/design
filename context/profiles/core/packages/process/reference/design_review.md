# Design Review

A structured, adversarial critique of a built interface against the principles — posture, a per-principle rubric, and a prioritized findings output.

A design review is a structured, adversarial critique of a built interface against
the design principles. Its job is not to admire the work — it is to find where the
hierarchy is weak, where decoration has crept in, where states are missing, and
where the design fails real users. A good review is uncomfortable; it grills the
work until the weaknesses surface. This procedure turns the principle docs into a
repeatable rubric.

## When to run it

- After building a screen or feature, before considering it done.
- As a polish/QA pass before shipping.
- When something "feels off" but you can't name why — the rubric names it.

## Posture: critique, don't admire

Approach the review as the toughest critic in the room (in the spirit of an
adversarial "grill me" interrogation):

- For every screen, **state where the eye goes first** — and check that it's the
  intended focal point. If you can't tell, the hierarchy has failed.
- **Hunt for decoration that does no work.** Any gradient, shadow, border, or
  animation that doesn't encode meaning is a finding (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/rules/aesthetic_discipline.md" />).
- **Assume the non-happy states exist** and go looking for them — empty, loading,
  error, disabled. Their absence is the most common real defect.
- **Look, don't just read code.** Whenever possible, view the rendered result at
  real sizes; rendering reveals what code review misses (font-load flashes,
  overflow, contrast, reflow).

## The rubric

Each section ties directly to a principle doc. Mark each item pass / needs-work and
cite the specific element.

### Visual hierarchy
- Is the most important element the most prominent? Is there exactly one focal
  point per view? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />)
- Does the type scale create clear, perceptible levels?
- Can you trace a deliberate first → second → third reading order?
- Are there multiple competing "primary" actions? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />)

### Contrast & color
- Does body text meet 4.5:1, large text 3:1, UI elements 3:1? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />)
- Is color used as *signal*, sparingly — or distributed evenly as decoration?
- Is meaning ever encoded in color alone (status, errors, active nav)?
- Do light and dark express the same semantic roles, not a naive inversion?

### Spacing & rhythm
- Do all gaps trace to the spacing scale, or are there one-off values? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/rules/token_usage.md" />)
- Is spacing used to group related things and separate unrelated ones?
- Is density intentional and internally consistent per region?

### Typography
- Is the type on an intentional scale, or are there arbitrary sizes? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />)
- Is body measure 45–75 characters and line height ≈ 1.5?
- Does the font actually load without a jarring flash?

### Motion
- Does every animation serve feedback, continuity, wayfinding, or status? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />)
- Is anything on the critical path blocked by an animation?
- Is there scattered micro-interaction noise? Is reduced-motion respected?

### Components & states
- Do interactive elements have default / hover / focus / active / disabled? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />)
- Do forms have empty / focus / filled / error / disabled? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />)
- Are loading and empty states designed for every list/table/card? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />)
- Is there feedback for every user action (success *and* failure)?
- Are similar components consistent (all cards, all fields, all buttons)?

### Composition & responsiveness
- Is everything aligned to shared edges/a grid? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />)
- Does the layout *reflow* (reorganize) at smaller sizes, not just shrink?
- Is reading order preserved across breakpoints?
- Is reading content width-constrained; functional content sensibly fluid? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" />)

### Accessibility-as-quality
- Visible focus on every interactive element? Logical focus order? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />)
- Touch targets ≥ 44px with spacing between them?
- Real heading hierarchy and landmark regions matching the visual order?
- Labels, alt text, and announced states present?

### Design-language fidelity
- Would someone recognize this as one coherent product? (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />)
- Does any element break the voice (an off-system color, a foreign font, an
  inconsistent component)?
- Does complexity match the vision (minimal executed with precision; maximal
  executed fully)?

## Named review gates

The rubric above asks "is this good?"; these gates make the answer **checkable**.
Each gate is a named, pass/fail test with a defined procedure, so a review reaches
the same verdict regardless of who runs it. Run them as a checklist — a view that
fails any gate has a finding, not an opinion. Each is tagged *automatable*,
*semi-automatable*, or *manual* so the convergent (tool-checkable) parts are never
left to taste.

- [ ] **Grayscale-first test** — *Checks:* does the visual hierarchy hold without
  color? *Run:* desaturate the view (CSS `filter: grayscale(1)`, a screenshot in
  grayscale, or design-tool color-blind preview); the intended focal point should
  still be the most prominent thing. *Fail:* the eye no longer lands on the focal
  point, or nothing stands out — the hierarchy is leaning on color it shouldn't.
  *Manual.*
- [ ] **One-hero test** — *Checks:* exactly one primary action per view? *Run:*
  count the primary-weight buttons / CTAs in the viewport. *Fail:* zero (no clear
  next step) or two-plus (competing heroes). See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />. *Manual.*
- [ ] **Self-evident test** (Krug) — *Checks:* would a first-time user know what to
  do without explanation? *Run:* show the view to someone unfamiliar (or imagine
  one) and ask what this screen is for and what they'd click first; they should
  answer correctly with no narration. *Fail:* they hesitate, ask, or guess wrong.
  *Manual.*
- [ ] **Squint test** — *Checks:* does the focal point survive blur? *Run:* squint
  at the screen, blur it (design-tool blur, `filter: blur(6px)`, or step back from
  the monitor); note what shape/block still reads. *Fail:* what survives the blur
  is not what users should see first — the layout's weight is misplaced. *Manual.*
- [ ] **State-completeness checklist** (from C8) — *Checks:* is every universal
  interaction state *and* every content state designed, not just the happy path?
  *Run:* walk each interactive element and each data region against the canonical
  list — interaction (default / hover / focus / active / disabled / loading) and
  content (empty / loading / partial / error / ideal / overflow). See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/states.md" />. *Fail:* any applicable
  state is undesigned. *Semi-automatable* — lint/grep component source for the
  presence of each state branch; the remaining states are checked manually.
- [ ] **Accessibility gate** (from C4) — *Checks:* the interface clears the WCAG
  success criteria the design owns. *Run:* verify each SC —
  **1.4.3 / 1.4.11** text and non-text contrast (≥ 4.5:1 body, 3:1 large/UI),
  **2.4.7 / 2.4.11** visible and unobscured focus, **2.5.8** target size (≥ 24px,
  44px preferred). *Convergent (automatable):* contrast ratios via tooling (axe,
  Lighthouse, contrast checkers) and target-size measurement. *Divergent
  (manual):* focus-order logic, ARIA roles/labels, and announced states require
  human judgment and AT testing. See
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />.
  *Fail:* any owned SC unmet.
- [ ] **Consistency gate** (from C18) — *Checks:* are design tokens used everywhere
  (no magic numbers) and is the system of constraints held? *Run:* grep/lint the
  source for raw values where a token should be (hex colors, px spacing, ad-hoc
  font sizes, one-off radii/shadows) and spot-check that similar components share
  one implementation. See <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/rules/token_usage.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/rules/aesthetic_discipline.md" />. *Fail:*
  off-scale values or divergent implementations of the same component.
  *Semi-automatable* — token/magic-number lint catches the values; "same system"
  consistency is confirmed manually.

## Output

Produce a **prioritized** list, grouped by severity, each finding citing the
specific element and a concrete fix:

- **Must fix** — broken function, accessibility failures, major principle
  violations (no focal point, failing contrast, missing error states).
- **Should fix** — inconsistencies, missing non-critical states, responsive
  issues.
- **Could improve** — polish, motion refinement, typographic fine-tuning.

End with **what works well** — not as padding, but so the strengths are preserved
in the next pass. A review that only lists faults is as unbalanced as one that only
praises.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_brief.md" />
