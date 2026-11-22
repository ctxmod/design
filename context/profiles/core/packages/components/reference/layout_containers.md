# Layout Containers

The structural slots — page shell, header, sidebar, content regions, modals, drawers, popovers; width contract, overlays, and responsive reconfiguration.

The **structural slots**. Layout containers are the skeleton every other component
sits inside: the page shell, its regions, the surfaces that overlay it, and the
rules that constrain content width. They are mostly invisible when done well — the
user notices structure only when it's broken (content too wide to read, a modal
that traps them, a sidebar that won't collapse). This file applies the theory in
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" /> to concrete structural slots. Part of the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

**Canonical names:** these are mostly *regions*, not primitives — structural areas
map to ARIA [landmark regions](https://www.w3.org/WAI/ARIA/apg/practices/landmark-regions/)
(header / nav / main / complementary / contentinfo). Overlays are *patterns*:
modals and blocking drawers follow the ARIA APG
[dialog (modal) pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)
for focus and role semantics (see canonical vocabulary (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />, section `#canonical-vocabulary`)).

## The container family

| Slot | Purpose |
|------|---------|
| **Page shell** | The outermost frame: header + content + (optional) footer/sidebars |
| **Header / app bar** | Persistent top region: brand, primary nav, global actions |
| **Sidebar** | Persistent side region: navigation or contextual tools, collapsible |
| **Content region / main** | The primary content area, width-constrained per its type |
| **Section / region** | A bounded sub-area within content (a landmark) |
| **Modal / dialog** | An overlay that demands focused attention, blocking the page |
| **Drawer / sheet** | An overlay sliding from an edge, often non-blocking |
| **Popover / dropdown surface** | A small transient overlay anchored to a trigger |

## The page shell

The shell defines the product's persistent frame. Its contract:

- **Persistent regions stay put** — the header (and sidebar, if present) keep the
  same position across screens so they are fixed reference points (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />).
- **Clear landmark regions** — header, nav, main, footer are distinct structural
  areas. This is both a compositional and an accessibility decision: clear regions
  produce clear landmarks for assistive tech (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/accessibility_as_quality.md" />).
- **One main content area** — the primary region the rest frames.

## The content-width / max-width contract

The most consequential container decision is **how wide content is allowed to be**,
because it directly controls readability and density:

- **Reading content is constrained.** Prose is capped at a comfortable measure
  (≈ 45–75 characters; see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />) regardless of how wide
  the viewport gets. Full-width paragraphs are unreadable.
- **Functional/dashboard content can fill width.** Tables, grids, and tool layouts
  use available space because the task is throughput, not reading (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/data_display.md" />).
- **Declare the intent per region.** A container states whether it is a *reading*
  container (narrow, centered) or a *fluid* container (fills, with sensible max),
  so the same page can mix a wide dashboard with a narrow reading panel
  consistently.
- **Margins frame the content** — the gutter between content and viewport edge
  comes from the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" /> and breathes more on larger
  screens.

## Overlays: modals, drawers, popovers

Overlays sit above the page and carry special responsibilities because they
interrupt the normal flow:

- **Modal / dialog** — *blocking*. Use only when the user must respond before
  continuing (a confirmation, a critical form). It requires:
  - A **scrim/backdrop** that dims and disables the page behind.
  - **Focus trapping** — focus moves into the dialog, stays within it, and returns
    to the trigger on close.
  - **Escape and an explicit close** affordance.
  - Restraint — modals are interruptions; overusing them is a known anti-pattern.
    Prefer inline disclosure when the task doesn't truly require blocking.
- **Drawer / sheet** — slides from an edge, often *non-blocking* or
  lightly-blocking; good for secondary navigation, filters, or contextual detail.
  It animates from the edge it lives on (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" /> wayfinding).
- **Popover / dropdown surface** — small, transient, anchored to its trigger;
  dismisses on outside-click or escape. Used by menus (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />) and contextual actions.

All overlays share: appear from/return to a logical origin, manage focus, be
dismissible by keyboard, and not lose the user (always a way back).

## States

| State | Applies to | Communicates |
|-------|-----------|--------------|
| **Default** | shells, regions | Resting structure |
| **Collapsed / expanded** | sidebars, drawers | Space-saving state, visible + announced |
| **Open / closed** | overlays | Visibility, with focus managed on transition |
| **Scrolled** | shells | Header may condense/elevate on scroll |
| **Loading** | content regions | Region-level loading (skeleton/spinner) (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />) |
| **Responsive reconfiguration** | shell | Regions reflow/stack at smaller sizes |

## Responsiveness (abstract)

Containers are where responsive behavior is most structural. The slot contract
(the medium tier sets the breakpoints):

- **Reflow, don't shrink.** Sidebars collapse to a drawer or off-canvas pattern;
  multi-region layouts stack; the header adopts a compact pattern (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/navigation.md" />).
- **Preserve reading order** through every reconfiguration (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />).
- **Width and density adapt** — narrower viewports get a single column and lower
  density; wider viewports earn more regions.

## Responsibilities

- **Provide a clear, consistent frame** with persistent, well-placed regions.
- **Enforce the width contract** — reading content constrained, functional content
  fluid, intent declared.
- **Manage overlays correctly** — scrim, focus trap/restore, dismissal, logical
  origin.
- **Yield clean landmarks** — structural regions that map to accessible landmarks.
- **Reconfigure responsively** while preserving order and readability.

## Anti-patterns

- Unconstrained prose spanning the full viewport width.
- A modal for something that didn't need to block the user.
- A modal that doesn't trap focus or doesn't return focus on close.
- Overlays with no keyboard dismissal.
- A desktop sidebar/nav left to overflow on mobile instead of collapsing.
- Shifting region positions between screens, destroying the user's spatial memory.
- A drawer that slides in from an edge it doesn't logically belong to.
