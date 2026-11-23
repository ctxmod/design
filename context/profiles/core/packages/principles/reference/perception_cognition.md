# Perception & Cognition

The named perception and cognition laws that ground the design principles — Gestalt, Fitts, Hick, working memory, serial position, von Restorff, aesthetic-usability, cognitive load, processing fluency.

## What + why

The design principles in this profile are not matters of taste. Each one is a
practical consequence of how the human visual system and working memory
actually behave — phenomena that have been named, measured, and replicated for
a century. This file is the **empirical foundation**: the catalog of laws the
principles rest on, stated so they can be cited by name and verified against
concrete artifacts.

These laws are **medium-agnostic**. Proximity governs grouping whether the
medium is a web layout, a CLI table, an iOS screen, or a LaTeX document.
Fitts's law applies to a mouse pointer, a thumb, and a keyboard's tab order
alike. Working-memory limits are properties of the user, not the surface.
Because the laws transfer unchanged, a principle grounded in a named law
inherits that law's validity in every medium — which is exactly why the design
profile is platform-independent at the principle tier.

Cite these laws by name when you justify a design decision or review one. "The
cancel button is too close to delete" is an opinion; "this violates Fitts's law
— the destructive and safe targets are adjacent, so pointer slips are
catastrophic" is a falsifiable claim with a fix.

## Testable obligations

- Every design decision that invokes a perceptual or cognitive rationale names
  the specific law it relies on, not a vague appeal to "best practice."
- Each principle file that depends on a law cross-links here by the law's name
  (see the catalog's "grounds" column).
- Claims are stated as the law actually holds — including its **caveats and
  bounds** (Hick weakens for complex navigation; 7±2 holds only for chunked
  content). Do not over-apply a law past its validated range.

## How to verify

- Pick any principle obligation; trace it to a named law in this catalog. If no
  law grounds it, the obligation is either taste (label it as such) or a missing
  entry here.
- For each law's "how to verify" below, the check is a concrete measurement on a
  real artifact (pixels, item counts, squint tests), not a subjective judgment.

## Anti-patterns

- **Cargo-culting a law past its bounds** — applying Hick's law to justify
  flattening a deep, familiar menu, or invoking Miller's 7±2 to cram seven novel
  controls into a toolbar. The bounds are part of the law.
- **Unnamed mechanism** — "this just looks more grouped" where *proximity* is
  the actual reason; naming it makes the fix mechanical.
- **Law as decoration** — citing a law to dress up a decision already made on
  taste. The law must actually predict the outcome you claim.

---

## The catalog

Each entry: **name + citation → definition → design obligation (imperative) →
how to verify → grounds**.

### Gestalt laws of grouping (Wertheimer 1923, and extensions)

The Gestalt psychologists showed that the visual system organizes raw marks
into wholes *pre-attentively* — before conscious reading — according to fixed
grouping cues. The user perceives these groupings whether or not you intend
them, so the only choice is to design with them.

#### Proximity

- **Definition.** Elements close together are perceived as a single group;
  space between them signals separation.
- **Obligation.** Encode relatedness with spacing first: related items get less
  space between them than unrelated items. Never space related fields like
  unrelated ones and then try to repair it with borders or color.
- **Verify.** Measure the gaps: the within-group gap must be strictly smaller
  than the between-group gap (e.g. 8px inside a field cluster, 24px between
  clusters). Equal gaps everywhere is a violation.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" /> (grouping),
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" /> (gaps create relatedness).

#### Similarity

- **Definition.** Elements that share shape, color, size, or orientation are
  perceived as belonging to the same category.
- **Obligation.** Style elements of the same kind identically; reserve visual
  difference to signal a real difference in kind or state.
- **Verify.** Two elements that look alike must *be* alike in role; find any
  pair that shares styling but differs in function — that is a false grouping.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />.

#### Common region

- **Definition.** Elements inside a shared boundary (a card, panel, or filled
  background) are perceived as a group, even when proximity and similarity are
  weak.
- **Obligation.** Use a region (card/panel/fill) to bind a group only when
  spacing alone cannot; one grouping mechanism is usually enough, do not stack
  region + heavy border + background on the same cluster.
- **Verify.** Each enclosing boundary must contain exactly one logical group;
  a card spanning two unrelated concerns is a violation.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" /> (grouping).

#### Uniform connectedness

- **Definition.** Elements joined by a continuous visual link (a connecting
  line, a shared background strip, a bracket) are grouped more strongly than by
  proximity or similarity alone — the strongest grouping cue.
- **Obligation.** When a relationship must override proximity (e.g. a label
  connected to a far control), use an explicit connector; otherwise rely on the
  cheaper cues.
- **Verify.** Any explicit connector must correspond to a real relationship;
  decorative lines that connect unrelated elements mislead and are a violation.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />.

#### Good continuation

- **Definition.** Elements arranged along a line or smooth curve are perceived
  as related and as continuing in that direction; the eye follows the flow.
- **Obligation.** Align elements onto shared edges and lines so the eye flows in
  reading order; stray elements aligned to nothing break continuity.
- **Verify.** Trace the alignment lines; count distinct left/center edges — a
  proliferation of near-identical edges reads as broken continuation.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" /> (alignment, continuity).

#### Closure

- **Definition.** The visual system completes incomplete shapes, perceiving a
  whole from partial contours.
- **Obligation.** Partial borders, implied containers, and open shapes can group
  as effectively as closed ones — exploit closure to reduce visual weight rather
  than drawing every full box.
- **Verify.** An implied grouping must still read as one group when squinted at;
  if the closure fails, the group dissolves.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />.

#### Common fate

- **Definition.** Elements that move together — same direction, same timing —
  are perceived as a single group, even if otherwise dissimilar.
- **Obligation.** Animate elements that belong together with shared motion
  (direction, timing, easing); animate unrelated elements separately so motion
  does not imply a false relationship.
- **Verify.** Watch any multi-element animation: elements moving in unison must
  be a real group; if unrelated items share a motion, that is a false grouping.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" /> (elements moving together read as related).

#### Figure-ground

- **Definition.** The visual system separates a scene into a *figure* (the
  attended object) and *ground* (the background) before anything is read; this
  separation is pre-attentive and automatic.
- **Obligation.** Ensure every primary element clearly reads as figure against
  its ground — sufficient contrast, separation, and elevation — so the user's
  eye lands on it without effort. Ambiguous figure-ground (low contrast, busy
  background) forces conscious work.
- **Verify.** Squint or blur the screen; the intended figure must remain
  distinct from the ground. If figure and ground blend, contrast or separation
  is insufficient.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" /> (figure-ground, the
  focal point reads as figure).

#### Prägnanz (law of good figure / simplicity)

- **Definition.** The visual system resolves ambiguous input into the simplest,
  most regular interpretation available — order is perceived as easier than
  disorder.
- **Obligation.** Favor regular, simple, predictable arrangements; complexity
  that does not carry meaning is perceived as noise and costs effort to resolve.
- **Verify.** For any layout, ask whether a simpler arrangement conveys the same
  structure; gratuitous irregularity that adds no meaning is a violation.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />.

### Fitts's law (Fitts 1954)

- **Definition.** The time to acquire a target is proportional to
  `log2(distance / width + 1)`: larger and closer targets are faster to hit;
  small or distant targets are slower and error-prone.
- **Obligation.** Make primary and frequently-used targets **large** and place
  them where the pointer/thumb already is. Place **destructive** actions far
  from their safe counterparts, and never make cancel-vs-confirm or
  delete-vs-keep targets adjacent and identically sized — a pointer slip must
  not be catastrophic.
- **Verify.** Count pixels: the primary-action target is ≥ 44px on its smallest
  dimension (the standard touch minimum) and is at least as large as secondary
  actions. Measure the gap between a destructive action and the nearest safe
  action; adjacency of delete and cancel is a violation. On non-pointer media:
  the primary action is reachable in the fewest keystrokes / earliest tab stop.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" /> (the primary action is
  large and prominent), and component button/dialog rules.

### Hick's law (Hick 1952; Hyman 1953)

- **Definition.** Decision time increases with the number and complexity of
  simultaneous choices, roughly logarithmically. **Caveat (Liu et al. 2020):**
  the relationship weakens or breaks down for complex, novel, or hierarchical
  navigation, where users do not evaluate all options serially — so the law does
  *not* straightforwardly argue for flattening deep menus.
- **Obligation.** Limit the number of choices presented *at one moment* —
  progressive disclosure, sensible defaults, and grouping reduce decision cost.
  Do **not** apply the law naively to deep or familiar navigation: splitting one
  rich menu into many shallow steps can be worse, not better.
- **Verify.** Count the simultaneous, equally-weighted choices on a decision
  surface (e.g. a primary toolbar or a first-run screen); a long flat list of
  co-equal options with no grouping or default is a violation. For deep
  navigation, do not cite Hick to justify added depth without evidence.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />.

### Working-memory capacity (Cowan 2001; Miller 1956)

- **Definition.** Working memory holds only a few items at once. **Cowan's**
  estimate for *novel, unchunked* items is about **4**. **Miller's** classic
  **7±2** applies only to *chunked, familiar* content, where each "item" is a
  meaningful unit the user already knows.
- **Obligation (the applicability rule — state both).** Design novel or
  unfamiliar groupings to **≤ 4 simultaneous items**. The larger **7±2** budget
  is achievable *only* for familiar, well-chunked content and expert interfaces
  where the items are recognized units, not raw elements. When in doubt about
  familiarity, design to the 4-item limit.
- **Verify.** Count the distinct novel items a user must hold to complete a step
  (form fields without grouping, options to compare, steps to remember). More
  than 4 novel items at once is a violation *unless* the content is demonstrably
  familiar/chunked, in which case up to ~7 is acceptable. Chunking (grouping
  into named units) is the fix that moves content from the 4-budget to the
  7-budget.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" /> (grouping/chunking),
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />.

### Serial position effect (Ebbinghaus; Murdock 1962)

- **Definition.** In an ordered sequence, items at the **start (primacy)** and
  **end (recency)** are remembered and noticed better than items in the middle.
- **Obligation.** Place the most important actions and information at the
  **start or end** of an ordered sequence (lists, menus, toolbars, steps), never
  buried in the middle where attention and recall are weakest.
- **Verify.** Identify the highest-priority item in any ordered set; it must
  occupy a first or last position. A primary action stranded mid-list is a
  violation.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />.

### von Restorff / isolation effect (von Restorff 1933)

- **Definition.** An item that differs perceptually from its neighbors is
  attended first and remembered best — the distinct one stands out.
- **Obligation.** Make the single primary action **perceptually distinct** from
  everything around it (the "one focal point"). Distinctiveness is spent, not
  scattered: if many elements are emphasized, none stands out.
- **Verify.** Squint test — exactly one element should survive as dominant. If
  two or more elements are equally emphasized, the isolation effect is squandered
  and there is no clear focal point.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" /> (one focal point, the
  isolated element).

### Aesthetic-usability effect (Kurosu & Kashimura 1995)

- **Definition.** Users perceive attractive interfaces as easier to use, and are
  more tolerant of minor usability problems in them — perceived usability tracks
  perceived beauty.
- **Obligation.** Treat visual craft as a **usability lever**, not surface
  polish. Invest in alignment, rhythm, color, and detail; a more attractive
  interface is measurably perceived as more usable. (This does not license
  hiding real usability defects behind beauty — it raises the floor, not a
  cover.)
- **Verify.** Craft is checkable via the other principles' obligations
  (consistent spacing scale, aligned edges, restrained color). An interface that
  fails those reads as lower-quality and inherits lower *perceived* usability.
- **Grounds.** the design profile as a whole; <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />.

### Cognitive Load Theory (Sweller 1988)

- **Definition.** Mental effort splits into three loads: **intrinsic** (inherent
  task difficulty), **extraneous** (effort wasted on poor presentation), and
  **germane** (effort that builds useful understanding). Total capacity is
  fixed; extraneous load steals from the rest.
- **Obligation.** **Minimize extraneous load** — remove clutter, inconsistency,
  and gratuitous variation that make the user work to parse the interface rather
  than the task. **Support germane load** — use consistent, predictable schemas
  so the user's effort goes into the work, not into re-learning the UI each
  screen.
- **Verify.** Audit for inconsistency: the same concept presented differently
  across screens, redundant decoration, controls that vary without reason — each
  is extraneous load. Consistency across screens (shared patterns, one spacing
  system) is the reduction.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />.

### Processing fluency (Reber et al.; CHI 2023)

- **Definition.** Visuals that are easy to process — clear, consistent,
  high-contrast, predictable — are judged more trustworthy, more usable, and
  more pleasant. Ease of perception is misattributed as a property of the thing
  perceived.
- **Obligation.** Raise fluency through **consistency and clarity**: predictable
  layouts, legible type, sufficient contrast, and reuse of established patterns.
  Disfluent presentation (low contrast, erratic layout, novel-for-novelty's-sake
  patterns) is read as less trustworthy.
- **Verify.** Check the fluency drivers concretely: contrast meets the
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" /> thresholds, type is legible,
  patterns repeat rather than reinvent per screen. Each inconsistency is a
  fluency cost.
- **Grounds.** <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />, and the aesthetic-usability effect above.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
