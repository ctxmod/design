# Information Architecture

Structuring content before styling — content inventory, site map, navigation model and depth, per-view hierarchy, labeling, flows, and growth.

Information architecture (IA) is the structural layer of a product: how content is
organized, labeled, and connected, and how users move through it. It sits *between*
the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_brief.md" /> and the visual build — you structure the
content before you style it. Designing pixels before the structure is settled
produces beautiful screens that don't add up to a navigable product. IA is where
navigation (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />) and
visual hierarchy (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />) get their marching
orders.

## When to do it

After the brief is written (you know the user's jobs) and before tokens/components.
Revisit it whenever content is about to grow significantly or navigation feels
deep.

## How to produce it

1. **Read the brief** — the key user tasks (JTBD) and audience drive every
   structural decision.
2. **Inventory what exists** — current routes, navigation, layouts, content models.
   Extend the existing structure; don't propose an architecture that ignores it.
3. **Interview on structure** — for each question, offer a recommended answer:
   - What are the primary things a user needs to find or do? Rank by frequency.
   - How many levels of navigation depth are acceptable?
   - What content is fixed vs. what will grow over time?
   - Are there distinct user types needing different entry points?
   - Which single view will the user spend most of their time in?
4. **Produce the IA artifacts** below.

## What IA defines

### Content inventory
A list of everything the product must hold — every page, view, and content type —
including what exists now and what will be added. You can't structure what you
haven't enumerated.

### Site map / structure
A hierarchical map of every page or view, with nesting shown by indentation and a
location pattern for each. This is the backbone the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/layout_containers.md" /> and
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" /> implement.

### Navigation model
- **Primary navigation** — the few top-level destinations. Keep it shallow; if it
  needs many items, the structure is too flat or the grouping is wrong.
- **Secondary navigation** — within-section destinations (sidebars, sub-nav).
- **Utility navigation** — account, settings, help — outside the main content
  hierarchy.
- **Mobile navigation** — the deliberate small-screen pattern, not a desktop bar
  that overflows (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />).

### Navigation depth
How many levels deep content lives. **Shallow beats deep**: each extra level hides
content and adds friction. Most products thrive at two or three levels; if core
content is four levels down, regroup rather than add menus.

### Content hierarchy per view
For each major view, rank content by priority (highest first) with a reason. This
ranking *is* the input to <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />
— the top-ranked content becomes the focal point. The most frequent user task
should land on the most reachable, prominent surface.

### Labeling / naming conventions
A glossary mapping each concept to the *one* word used for it in the UI. Names come
from what the user controls and recognizes, never from how the system is built (a
person manages "notifications", not "webhook config"). Consistency is how people
learn their way around — pick one word and use it everywhere (this vocabulary is
shared with <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" /> and
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" /> labels).

### User flows
The critical paths through the product, each a sequence of steps with decision
points and branches noted. Flows reveal missing screens and dead ends that a static
site map hides. Cover at least the make-or-break flows from the brief (onboarding,
the core task, recovery from error).

### Content growth plan
Which areas accumulate content over time and how the structure absorbs it —
pagination, filtering, search, archiving (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />). An IA that
works at launch but collapses at scale isn't done.

## Principles

- **Structure before style.** Settle organization, labels, and flows before
  visual design.
- **Rank by user frequency**, not by org chart or technical convenience.
- **Shallow over deep.** Minimize the clicks to the most-wanted content.
- **One name per concept**, drawn from the user's vocabulary, used everywhere.
- **Design for growth**, not just the launch dataset.
- **The IA and the visual hierarchy must agree** — the structure's priorities are
  the screen's priorities.

## Anti-patterns

- Designing screens before the structure is decided.
- Deep nesting that buries primary content.
- Navigation that mirrors the system's internals instead of the user's tasks.
- Multiple words for the same concept across the product.
- An IA that ignores how content will grow.
- A flat site forced into breadcrumbs, or a deep hierarchy with no wayfinding.
