# Inputs

The data-entry slots — text, select, checkbox, radio, toggle, slider; label/helper/error pattern, states, and validation feedback.

The **data-entry slots**. Inputs let the user supply information: text, choices,
ranges, toggles. Their shared job is to make entry effortless and error recovery
painless — to be obvious about what is expected, forgiving about mistakes, and
clear about what went wrong. Part of the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

**Canonical names:** these are several Open UI primitives —
[`input`](https://open-ui.org/), [`select`](https://open-ui.org/), [`checkbox`](https://open-ui.org/),
[`combobox`](https://open-ui.org/) — not one slot. Role/state/keyboard semantics
follow the matching ARIA APG patterns ([combobox](https://www.w3.org/WAI/ARIA/apg/patterns/combobox/),
[checkbox](https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/),
[radio group](https://www.w3.org/WAI/ARIA/apg/patterns/radio/),
[slider](https://www.w3.org/WAI/ARIA/apg/patterns/slider/)) per family member
(see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />).

## The input family

Each is a distinct slot sharing a common contract:

| Slot | Purpose | Choose when |
|------|---------|-------------|
| **Text input** | Single-line free text | Short, open-ended values (name, email) |
| **Textarea** | Multi-line free text | Longer prose; show it can grow |
| **Select** | One choice from many | More options than fit comfortably as radios (≈ 6+) |
| **Checkbox** | Independent on/off, or multi-select | Each option toggles independently |
| **Radio group** | One choice from a small set | 2–5 mutually exclusive options, all worth showing |
| **Toggle / switch** | Immediate binary state | The change takes effect at once (a setting), not on form submit |
| **Slider** | Value within a range | Approximate selection along a continuum |

Choosing the right slot is itself a design decision: a select for two options, or
radios for twenty, are both wrong.

## The label / helper / error pattern

Every input field is a small composite with a consistent structure:

- **Label** — always present and always visible. Names what the field is, from the
  user's side of the screen (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/information_architecture.md" />).
  *Placeholder text is not a label* — it vanishes on input and fails contrast (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
- **Helper text** — optional guidance shown *before* an error: format hints,
  constraints, examples. Calm and persistent.
- **Error text** — replaces or accompanies helper text when validation fails. Says
  what went wrong *and how to fix it*, in the interface's voice, specific not
  vague ("Enter a date in the future", not "Invalid input").
- **Required/optional indication** — communicated consistently and explicitly, not
  by an unexplained asterisk alone.

The label must be programmatically associated with the control (a click on the
label focuses the field; assistive tech announces it).

## States

| State | Must communicate |
|-------|------------------|
| **Empty** | The field is ready; the label (and placeholder, if any) shows what's expected |
| **Focus** | This field is active — visible focus indicator (≥ 3:1) |
| **Filled** | A value is present and legible |
| **Error** | Validation failed — color *plus* an icon/text, with a fix-it message |
| **Success** (optional) | Validation passed where confirmation helps (e.g. unique username) |
| **Disabled** | Not editable now; visibly inert but still readable |
| **Read-only** | Value shown for reference, not editable — distinct from disabled |
| **Loading** (async) | Validating or fetching options — show progress |

Distinguish **disabled** (can't edit, often temporary) from **read-only** (won't
edit, value matters) — they mean different things to the user.

## Validation feedback

Validation is a design problem, not just a logic one:

- **Validate at the right time.** Prefer validating on blur or submit, not on every
  keystroke (which scolds the user mid-entry). Re-validate *as the user fixes* so
  the error clears the moment it's resolved.
- **Show errors at the field**, inline and adjacent, not only in a summary far from
  the input. For long forms, a summary that links to each failing field helps too.
- **Never rely on color alone** for the error state — pair red with an icon and a
  message (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).
- **Preserve the user's input** on error; never clear a form because one field
  failed.
- **Error copy directs.** It explains the fix, doesn't apologize, and isn't vague
  (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" /> for the shared voice of failure states).

## Responsibilities

Any input implementation must guarantee:

- A **visible, associated label** and an **accessible name**.
- A **visible focus state** and full keyboard operability (tab to reach, type/space/arrow
  to operate; radio groups arrow-navigate, selects open by keyboard).
- **Adequate target size** for checkboxes, radios, and toggles — pad the hit area
  beyond the small glyph (≥ 44px, see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
- **Forgiving input** — trim/normalize where safe, accept reasonable formats, don't
  reject on trivial differences.
- **Stable layout** — showing an error message must not shove the rest of the form
  around jarringly; reserve space or animate gently (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

## Anti-patterns

- Placeholder text used *as* the label.
- Validation that fires on every keystroke and turns the field red before the user
  finishes typing.
- Error messages that say "invalid" without saying what's valid.
- Clearing the whole form on a single field error.
- Tiny checkbox/radio targets.
- Color-only error indication.
- A toggle used for a setting that actually requires a submit (use a checkbox), or a
  checkbox for something that takes effect immediately (use a toggle).
