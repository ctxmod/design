# Data Display

The read-heavy slots — tables, lists, key-value, badges/tags, avatars; density, sorting/filtering, and the full non-happy state set.

The **read-heavy slots**. These components present existing information for the user
to read, scan, compare, and act on — rather than to enter (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />). Their shared job is **legibility at volume**: making rows,
values, and labels scannable, comparable, and navigable without overwhelming. Part
of the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

**Canonical names:** Open UI [`table`](https://open-ui.org/) and
[`treegrid`](https://open-ui.org/) for the structured-data slots; role/state/keyboard
semantics follow the matching ARIA APG patterns ([table](https://www.w3.org/WAI/ARIA/apg/patterns/table/),
[treegrid](https://www.w3.org/WAI/ARIA/apg/patterns/treegrid/)). Badges and tags
are *presentational* — read, not interactive — and carry no dedicated pattern (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />).

## The data-display family

| Slot | Purpose | Choose when |
|------|---------|-------------|
| **Table** | Compare multiple records across multiple attributes | Data is genuinely tabular (rows × columns) and comparison matters |
| **List** | Sequence of items, one primary dimension | Items are read top-to-bottom, not column-compared |
| **Key-value / description list** | Labeled attributes of one entity | Showing the properties of a single thing (a profile, an order) |
| **Badge / tag / chip** | A compact label for status, category, or count | Annotating an item with a small piece of metadata |
| **Avatar** | Visual identity of a person/entity | Representing a user/account compactly |

The most common mistake is a **table used for non-tabular data** (a list of cards
forced into rows) or a **list used where comparison is needed** (forcing the user
to scroll back and forth instead of seeing columns). Match the slot to how the user
actually reads the data.

## Density

Data display is where <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" /> matters most. The same data
can be comfortable or compact:

- **Comfortable rows** — more padding, easier on the eyes, fewer rows per screen.
  Good for casual reading and touch.
- **Compact rows** — tighter padding, more rows per screen, faster comparison. Good
  for expert tools and large datasets.

Offer density as a systematic option, and within one table/list keep it uniform.
Even at high density, preserve enough rhythm (consistent row height, aligned
columns) that scanning stays effortless — alignment is what makes dense data
readable (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />).

Alignment conventions aid scanning:

- **Numbers right-aligned** (and decimal-aligned) so magnitudes line up.
- **Text left-aligned.**
- **Column headers aligned to their data.**

## Sorting and filtering contracts

For tabular and list data, sorting and filtering are part of the slot:

- **Sorting** — sortable columns indicate they are sortable, show the current sort
  column *and direction*, and allow exactly one (or a defined multi-) sort at a
  time. The sort state is visible, not hidden.
- **Filtering** — active filters are *visible* (the user must see what's narrowing
  the data, e.g. filter chips), and individually removable. Filtering to zero
  results yields a "no results" empty state distinct from "no data yet" (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />).
- **Pagination / virtualization** — large sets are paged or virtualized; the
  current position is shown (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" /> pagination). Don't
  silently truncate data without telling the user there's more.

These contracts are about *making state visible*; the mechanics are medium-tier.

## Badges, tags, and avatars

- **Badge / status indicator** — communicates a state (active, pending, error) and
  obeys the severity color contract: never color-alone, pair with text/icon (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />). A badge is read, not clicked.
- **Tag / chip** — a category or attribute label; may be removable (in a filter
  context) — when removable it gains a control state set and a clear remove target.
- **Count badge** — a number annotation (unread count); keep it legible and cap
  large values ("99+").
- **Avatar** — identity; always has a *fallback* (initials, default) when no image,
  and an accessible name. Avatar groups show overflow ("+3").

## States

Every data-display component needs its non-happy states designed:

| State | Communicates |
|-------|--------------|
| **Loaded** | The data, scannable |
| **Loading** | Data arriving — skeleton rows matching the layout, not a bare spinner (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />) |
| **Empty (no data)** | Nothing exists yet + how to create the first item |
| **Empty (no results)** | The filter/search matched nothing + how to broaden |
| **Error** | The data failed to load + retry |
| **Partial / paginated** | More exists beyond what's shown; current position visible |
| **Row interaction** | If rows are selectable/clickable, they carry hover/focus/selected states |
| **Selected** | For multi-select tables, selected rows + a bulk-action affordance |

A data table without an empty state and a loading state is incomplete — these are
the states users hit most outside the demo data.

## Responsibilities

- **Match the slot to the reading task** (compare → table, sequence → list,
  attributes → key-value).
- **Scannability** — consistent alignment, row rhythm, and column structure.
- **Visible state** for sort, filter, pagination, and selection.
- **All non-happy states designed** — loading (skeleton), empty (both kinds),
  error.
- **Accessible structure** — real table semantics (headers associated with cells),
  meaningful row labels, badges/avatars with text equivalents (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
- **Responsive strategy** — wide tables need a deliberate small-screen approach
  (priority columns, horizontal scroll with a frozen key column, or a stacked
  card view). The medium tier picks the technique; the slot requires that one
  exists.

## Anti-patterns

- A table for data that isn't tabular; a list where comparison is needed.
- Numbers left-aligned so magnitudes don't line up.
- Hidden sort/filter state (the user can't tell what's applied).
- Silent truncation of large datasets.
- A bare spinner over a table instead of skeleton rows.
- No empty/error states; the same empty state for "no data" and "no results".
- Status badges distinguished by color alone.
- Avatars with no fallback for the no-image case.
