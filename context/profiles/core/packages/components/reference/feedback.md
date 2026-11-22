# Feedback

The status/communication slots — toasts, alerts, banners, validation, loading/progress, empty states; severity, dismissibility, and the voice of failure.

The **status / communication slots**. Feedback components tell the user what is
happening, what happened, and what to do about it — confirmations, warnings,
errors, progress, and the absence of content. They are where an interface's
*character under stress* shows: anyone can design a happy path, but the quality of
a product is revealed by how it handles failure, waiting, and emptiness. Part of
the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

**Canonical names:** Open UI [`alert`](https://open-ui.org/), [`toast`](https://open-ui.org/),
and [`dialog`](https://open-ui.org/) per family member. Role/state semantics follow
the matching ARIA APG patterns ([alert](https://www.w3.org/WAI/ARIA/apg/patterns/alert/),
[dialog](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)) — see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

## The feedback family

| Slot | Purpose | Lifespan |
|------|---------|----------|
| **Toast / snackbar** | Transient confirmation of a completed action | Auto-dismiss (seconds) |
| **Alert** | An important inline message tied to a region/context | Until resolved/dismissed |
| **Banner** | A page- or app-level message | Persistent until addressed |
| **Inline validation** | Field-level feedback during data entry | Until the field is valid (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />) |
| **Loading / progress** | Communicates an operation in flight | Duration of the operation |
| **Empty state** | Communicates "nothing here yet" and what to do | Until content exists |

Choose by *scope and lifespan*: a toast for a quick "Saved", an alert for a
context-specific problem, a banner for a system-wide notice.

## The severity contract

Most feedback carries a **severity** that maps to a fixed semantic meaning and
color (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />):

| Severity | Means | Tone |
|----------|-------|------|
| **Info** | Neutral notice, FYI | Calm |
| **Success** | An action completed | Affirming, brief |
| **Warning** | Something needs attention but isn't broken | Cautioning |
| **Error / danger** | Something failed or is invalid | Direct, corrective |

Contract rules:

- Severity is **consistent everywhere** — error is always the danger color and
  always means failure; success never borrows the warning color.
- **Never severity-by-color-alone.** Each severity pairs its color with an icon
  and/or label so it survives color-blindness and low contrast (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
- Severity affects *prominence*: errors interrupt more than info; calibrate the
  visual weight to the severity (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />).

## Dismissibility and persistence

How long feedback lives, and who controls that, is a deliberate contract:

- **Auto-dismiss** (toasts) — for low-stakes confirmations the user need not act
  on. Give enough time to read (longer for more text), and never auto-dismiss
  anything the user must act on or might miss.
- **Manual dismiss** — for messages the user should acknowledge; provide a clear
  close affordance.
- **Persistent** — for unresolved problems (a failed sync, a required action). The
  message stays until the underlying condition is fixed; dismissing it would hide a
  real problem.
- **Never stack** a wall of toasts; collapse or queue them. Don't let transient
  feedback obscure the content or the action that produced it.

## Loading and progress

Waiting is feedback. Choose the right indicator:

- **Indeterminate** (spinner, indeterminate bar) — when duration is unknown.
- **Determinate** (progress bar/ring) — when progress is measurable; show real
  progress, never a fake crawl.
- **Skeletons** — for content that's loading into a known layout; a skeleton
  matching the final shape prevents reflow and feels faster than a spinner (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" />).
- **Optimistic UI** — for fast, reversible actions, show the result immediately and
  reconcile in the background, reverting with an error message if it fails.
- Respect <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />: loading animation should be calm and continuous;
  don't make the wait *feel* longer with jarring motion, and provide a
  reduced-motion fallback.

## Empty states

An empty screen is a design opportunity, not a blank. Every list, table, and
collection needs an empty state (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />). A good
empty state:

- **Explains why it's empty** — first use? filtered to nothing? cleared?
- **Tells the user what to do next** — the primary action to create the first item,
  or to clear the filter.
- **Matches the voice** — an invitation, not an apology. Distinguish "no results
  for this search" (suggest broadening) from "nothing created yet" (offer to
  create).

## The voice of failure and waiting

Feedback copy is design material (this voice is shared with
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" /> validation):

- **Errors explain and direct** — what went wrong and how to fix it, specifically.
  They don't apologize, don't blame the user, and are never vague ("Something went
  wrong" with no recourse is a failure of the feedback).
- **Confirmations are brief and consistent** — the action named "Publish" produces
  "Published".
- **Warnings are honest** — they state the consequence so the user can decide.
- Treat failure and emptiness as moments for **direction, not mood**.

## Responsibilities

- Provide feedback for **every** user action — success and failure both.
- Carry a **consistent severity** with icon+text, not color alone.
- Make **dismissibility match stakes** — auto-dismiss only the unimportant.
- **Announce to assistive tech** — status messages should be perceivable without
  sight (live regions are a medium-tier concern; the slot's contract is that the
  message is announced, not merely shown).
- **Don't obscure** the content or the triggering control.

## Anti-patterns

- Silent success (the action worked but nothing confirmed it) or silent failure.
- Generic "Something went wrong" with no cause and no fix.
- Severity by color only.
- Auto-dismissing an error or a required action before the user can read/act.
- Fake progress bars; spinners where a skeleton would feel faster.
- A blank empty state with no explanation or next step.
- Toasts stacking into an unreadable pile.
