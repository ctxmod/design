# Information Density

Information-per-area as a first-class principle — manage cognitive load via progressive disclosure and density modes matched to expertise.

## What + why

Information density is the amount of meaningful information presented per unit of
screen area. It is a first-class design variable, not a side-effect of layout: every
screen sits somewhere on a continuum from sparse to packed, and where it sits
determines how much mental effort the user spends to read it.

Density drives **cognitive load**. The grounding is **Cognitive Load Theory**
(Sweller 1988): mental effort splits into **intrinsic** (the inherent difficulty of
the task), **extraneous** (effort wasted parsing poor presentation), and **germane**
(effort that builds useful understanding). Total capacity is fixed, so extraneous
load — clutter, inconsistency, gratuitous variation — steals from the budget the task
itself needs. Density is the lever: too high and the user drowns in extraneous load;
too low and the task fragments across scrolls and screens, taxing memory instead.

The ceiling is set by **working-memory capacity** (Cowan 2001): a user can hold only
about **4** novel, unchunked items at once (Miller's 7±2 applies only to familiar,
chunked content). A dense view that presents more than ~4 simultaneous novel items
exceeds what the user can hold, regardless of how cleanly it is styled. Both laws are
catalogued in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />; this principle is
their concrete application to the density variable.

The resolution is not "always sparse." It is to spend the area budget deliberately:
strip extraneous load, reinforce germane load with consistent schemas, reveal detail
progressively, and tune the overall density to who is reading.

## Testable obligations

- **Minimize extraneous load.** Remove clutter, redundant decoration, and
  inconsistent patterns that make the user work to parse the interface rather than
  the task. The same concept must look the same across screens.
- **Support germane load.** Use consistent, predictable schemas (one spacing system,
  repeated layouts, stable component vocabulary) so the user's effort goes into the
  work, not into re-learning the UI on each screen.
- **Layer summary → drill-down (progressive disclosure).** Present a high-level
  summary first and reveal detail on demand. Do not show every field, option, and
  edge case at once; depth is opened by the user, not forced on them.
- **Cap simultaneous novel items near Cowan-4.** Limit the distinct *novel,
  unchunked* items presented at one moment to ~4. Chunking (grouping into named
  units) is the fix that raises the budget toward 7±2 — apply it before adding items.
- **Match density to user expertise.** Experts operating a high-frequency tool
  tolerate — and prefer — higher density; novices and first-run flows need a more
  spacious layout. Choose the density for the actual audience and task frequency, not
  a single default for everyone.

## Tunable dimension

Density is itself a continuum, so it is the principle's tunable axis. Name the poles:

- **compact** — maximum information per area; for experts and high-frequency,
  data-dense surfaces (dashboards, tables, IDE panels) where scanning speed beats
  breathing room.
- **comfortable** — the balanced default; readable for a general audience without
  wasting space.
- **spacious** — generous whitespace and large targets; for novices, first-run flows,
  marketing, and low-frequency tasks where guidance beats throughput.

This axis is also a token **mode**: a `density` mode re-resolves semantic
spacing/sizing roles (e.g. `space-component-pad`) to tighter or looser primitives
without touching component code. See the Modes subsection of
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" /> — density is one of the
three concrete modes (theme, density, locale).

## Frequency-vs-severity heuristic

When deciding what earns scarce screen space, the practitioner rule is **frequency ×
severity**: content that is both *frequently needed* and *high-severity* (costly to
miss — errors, destructive confirmations, the primary action) earns prominent, always-
visible space; content that is rare and low-stakes is demoted, deferred, or hidden
behind progressive disclosure. A rarely-needed, low-consequence setting does not
deserve the same real estate as the action the user takes every minute.

This is a **heuristic, not a law** — it can trade off against cognitive-load
minimization. Promoting every frequent-and-severe item can itself crowd the screen
past the Cowan-4 ceiling. Use frequency × severity to *rank* candidates for space,
then let the load obligations *cap* how many you actually present at once.

## How to verify

- **Item count.** Count the distinct novel items a user must hold to complete a step.
  More than ~4 unchunked items is a violation unless the content is demonstrably
  familiar/chunked (then up to ~7).
- **Extraneous-load audit.** Scan for the same concept rendered differently across
  screens, decoration that carries no meaning, and controls that vary without reason —
  each is removable extraneous load.
- **Progressive disclosure.** Confirm the first view is a summary and that detail is
  reachable on demand; a screen that dumps every field at once fails.
- **Density-to-audience.** Name the audience and task frequency in one sentence; the
  chosen density pole (compact / comfortable / spacious) must match it.
- **Space allocation.** For the most prominent content, confirm it ranks high on
  frequency × severity; prime real estate spent on rare, low-stakes content is a
  misallocation.

## Anti-patterns

- **Wall of everything** — every field, option, and edge case shown at once, exceeding
  the working-memory ceiling; no summary, no drill-down.
- **Decorative clutter** — borders, fills, icons, and variation that add extraneous
  load without encoding meaning.
- **One density for all** — shipping a single spacious layout to expert power users who
  want compact, or cramming a novice first-run flow into a dense expert layout.
- **Inconsistent schemas** — the same concept styled or laid out differently per
  screen, forcing the user to re-learn the UI and converting germane effort into
  extraneous load.
- **Heuristic as law** — promoting every frequent-and-severe element until the screen
  is crowded past Cowan-4, treating frequency × severity as a mandate to show rather
  than a rule to rank.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
