# Navigation

The wayfinding slots — primary/secondary nav, tabs, breadcrumbs, pagination, menus; the active-state contract, hierarchy, and states.

The **wayfinding slots**. Navigation answers the user's persistent questions:
*where am I, where can I go, and how do I get back?* These components are the
product's map and address system. Their shared contract is a clear **active state**
(you are here) and a structure that reflects the real
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/information_architecture.md" />.
Part of the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

**Canonical names:** Open UI [`nav`](https://open-ui.org/), [`tabs`](https://open-ui.org/),
and [`menu`](https://open-ui.org/) per family member. Role/state/keyboard semantics
follow the matching ARIA APG patterns ([tabs](https://www.w3.org/WAI/ARIA/apg/patterns/tabs/),
[menu button](https://www.w3.org/WAI/ARIA/apg/patterns/menu-button/),
[breadcrumb](https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)) — see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

## The navigation family

| Slot | Purpose | Choose when |
|------|---------|-------------|
| **Primary nav** | Top-level destinations | The few main sections of the product |
| **Secondary nav** | Within-section destinations | A section has its own sub-areas |
| **Tabs** | Switch views of the *same* context | Alternate views/panels at one location, no URL-level move required |
| **Breadcrumbs** | Show position in a hierarchy + step back up | Deep, nested hierarchies |
| **Pagination** | Move through a sequence of pages/results | Long, ordered result sets |
| **Menu / dropdown** | A collapsed list of actions or links | Many options that shouldn't occupy permanent space; overflow |

Distinguish **tabs** (switch views in place — same context, no real navigation)
from **primary nav** (move to a different destination). Misusing tabs as
navigation, or nav as tabs, confuses the user's mental model of "where am I."

## The active-state contract

The single most important navigation responsibility: **always show where the user
is.** Every navigation component must mark the current location/selection
unambiguously.

- The active item is visually distinct via *more than one* channel — not color
  alone (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />,
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />) — e.g. color plus a
  weight change plus an indicator bar.
- The active state must be **announced** to assistive tech (current page /
  selected tab), not just styled.
- In nested navigation, the active state should cascade: the active sub-item also
  implies its parent section is active.
- Exactly one active item per navigation group (one current tab, one current page).

## Hierarchy

Navigation *is* hierarchy made visible. Its structure must mirror the IA:

- **Depth discipline.** Keep primary navigation shallow (a small number of
  top-level items). Deep menus hide content; if everything is three levels down,
  the IA needs rework, not more menus (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/information_architecture.md" />).
- **Consistent placement.** Primary nav lives in the same place on every screen so
  it becomes a fixed reference point (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />).
- **Levels are distinct.** Primary, secondary, and tertiary navigation should be
  visually differentiated so users sense which level they're operating at (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />).
- **Labels are nouns the user recognizes** — named by what the user wants, not how
  the system is built. Each label is one word, used everywhere that destination is
  referenced.

## States

Navigation items carry an interaction state set on top of the active state:

| State | Communicates |
|-------|--------------|
| **Default** | A reachable destination |
| **Hover** | It's interactive |
| **Focus** | Keyboard focus — visible ring, correct order |
| **Active (current)** | You are here — the persistent location marker |
| **Pressed** | The choice registered |
| **Disabled** | Unavailable now (e.g. pagination "next" on the last page) |
| **Expanded/collapsed** | For menus/disclosure nav, the open/closed state must be visible and announced |

Tabs add a **selected** state (the visible panel); pagination adds **current page**
plus disabled boundaries.

## Responsibilities

- **Always answer "where am I"** via the active-state contract.
- **Reflect the real IA** — navigation that doesn't match the content structure
  misleads.
- **Full keyboard support** — all items reachable and operable by keyboard; menus
  open/close and arrow-navigate; focus is managed when a menu opens and restored
  when it closes (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
- **A mobile pattern, not an overflow.** On small screens, navigation must adopt a
  deliberate pattern (drawer, bottom tabs, disclosure menu) — never a desktop bar
  that overflows or wraps. The medium tier specifies the breakpoint behavior; the
  slot's contract is that a small-screen pattern *exists*.
- **Adequate targets** — nav items and pagination controls meet the minimum target
  size.

## Anti-patterns

- No visible "current location" indicator.
- Active state shown by color alone.
- Tabs used to navigate between unrelated pages (or nav used to switch in-place
  views).
- Deeply nested menus hiding primary content.
- A desktop nav bar left to overflow on mobile.
- Inconsistent nav placement between screens.
- Breadcrumbs that don't actually reflect the hierarchy, or exist on a flat site
  that has no hierarchy to show.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" />
