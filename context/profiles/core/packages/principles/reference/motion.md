# Motion

Motion as a design material justified only by helping the user — purposes, easing, duration bands, choreography, and when not to animate.

Motion is a design material with a single justification: it must help the user.
Animation that exists for delight alone is the fastest way to make an interface
feel cheap, slow, or "AI-generated." Every animation should answer a question the
user is already asking — *where did that come from? what changed? did my action
register? what happens next?* If it answers none of those, it should not exist.

This document is the *principle* of motion. Platform mechanics — CSS transitions,
the Motion library, `prefers-reduced-motion`, GPU-friendly properties — belong to
the medium tier. Honoring reduced-motion preferences is mandatory, but it is a
medium-tier implementation of the principle stated here: *motion is optional and
must degrade gracefully.*

Motion is **medium-conditional**. Web and iOS have animation as a first-class
material; LaTeX, print, and CLI largely *don't*. A medium profile must declare
where it stands: a profile like `cli` or `latex` declares motion
as **dropped** in its capability declaration, and the principles below do not
apply there. Treat this as the generality hook — the triad and the semantic
categories that follow are the shared vocabulary a motion-capable medium fills,
and a motion-incapable medium explicitly forgoes.

## The motion triad

Every motion decision is a triad: **duration band + easing curve + animated
property**. A motion token is not a single number. "300ms" is underspecified —
300ms of *what*, eased *how*? A complete token names all three: a duration band
(below), a semantic easing curve (below), and the property it animates (opacity,
transform, color — and, for performance, transform/opacity are preferred over
layout-affecting properties at the medium tier).

Obligation: any motion token a brand defines must specify all three. A duration
without an easing curve, or an easing curve without a bound property, is an
incomplete token.

## The purposes of motion

Useful motion serves one of a small set of jobs:

| Purpose | What it does | Example |
|---------|--------------|---------|
| **Feedback** | Confirms an action registered | Button depresses on press; toggle slides |
| **Continuity** | Preserves object identity across a change | A card expands into a detail view rather than cutting |
| **Wayfinding** | Shows spatial relationships | A drawer slides in from the edge it lives on |
| **Status** | Communicates ongoing process | Progress fill, indeterminate spinner |
| **Direction of attention** | Draws the eye to a change | A new item gently fades/slides in |

If a proposed animation maps to none of these, cut it.

## Easing curves

Easing is how an animation distributes its motion over time. It is the difference
between motion that feels physical and motion that feels mechanical.

- **Ease-out** (fast start, slow settle) — the default for elements *entering* or
  responding to user input. It feels responsive because the result appears
  quickly, then settles.
- **Ease-in** (slow start, fast end) — for elements *leaving*. They accelerate
  away.
- **Ease-in-out** — for elements moving *within* the view (repositioning,
  reordering).
- **Linear** — only for continuous, looping motion (spinners, marquees) where any
  acceleration would look wrong.
- **Spring / overshoot** — adds personality and a sense of physicality, but
  overshoot reads as playful and can feel toy-like on serious products. Use it
  intentionally as part of the brand's voice, not as a default.

Avoid the symmetric `ease` default for UI; it feels sluggish on entry. Tie a small
set of named curves to the design language and reuse them (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/design_language.md" />).

### Semantic easing categories

Curves are not chosen per-animation; they are chosen per *meaning*. Brands fill a
small set of named semantic categories (as Material 3 does), and the perceptual
meaning is fixed even as the exact cubic-bezier varies by brand:

| Category | Curve family | Meaning (perception) | Use |
|----------|--------------|----------------------|-----|
| **`motion-standard`** | gentle ease-in-out | neutral, reversible | Enter/exit and small reversible transitions — the everyday default |
| **`motion-emphasized`** | pronounced ease-in-out | "this matters" | Large or important transitions; the hero motion of the product |
| **`motion-decelerated`** | ease-out | **arriving / settling** | Things coming *into* view: result appears fast, then settles |
| **`motion-accelerated`** | ease-in | **leaving / urgent** | Things *exiting*: accelerate away and clear the view |

The perceptual rule under it: **ease-out = arriving/settling** (the eye catches
the element early, then it comes to rest), **ease-in = leaving/urgent** (the
element gathers speed as it departs). A brand defines the four categories once;
every motion token then references a category rather than a raw curve.

## Duration bands

Duration should match the size and importance of the change. Reuse a small set of
bands rather than per-animation guesses:

| Band | Range | Use |
|------|-------|-----|
| Instant | 50–100 ms | Micro-feedback: hover, press, small state flips |
| Fast | 150–250 ms | Most UI transitions: dropdowns, toggles, tooltips |
| Moderate | 250–400 ms | Larger surfaces: modals, drawers, page sections |
| Slow | 400–600 ms | Big, deliberate moments: full-page transitions, hero reveals |

Rules of thumb:

- **Smaller and more frequent → faster.** A hover that takes 400 ms feels broken.
- **Larger travel → slightly longer**, but rarely above 600 ms; users perceive
  anything slower as lag.
- **Exits can be a touch faster than entrances** — the user has already moved on.

## Choreography

When several elements animate together, choreograph them rather than firing
everything at once:

This rests on **common fate**, the Gestalt principle that elements moving
together are perceived as related (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/perception_cognition.md" />). Choreography is the
deliberate use of common fate: shared motion groups elements, divergent motion
separates them.

- **Stagger** related items (list rows, cards) by a small delay each, so the group
  reveals as a sequence. One orchestrated page-load sequence with staggered reveals
  delivers more delight than dozens of scattered micro-interactions.
- **Sequence cause and effect** — the trigger animates, then the result. A menu
  button rotates, then the menu expands.
- **Respect spatial origin** — things should appear from and disappear toward
  where they logically live (a tooltip from its anchor, a drawer from its edge).
  This reinforces <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/visual_hierarchy.md" />.
- **Don't over-stagger.** Long stagger chains make the UI feel slow; keep the
  total sequence short.

## When NOT to animate

Restraint is the harder, more valuable skill:

- **Never animate the critical path.** If the user must wait for an animation to
  finish before they can act, the animation is now latency.
- **Don't animate frequent, repeated actions** into something slow. The hundredth
  time the user opens a menu, a flourish is friction.
- **Don't animate to mask a slow operation** unless the animation communicates the
  wait honestly (a real progress indicator, not a fake delay).
- **Don't scatter micro-interactions** everywhere. Density of motion reads as
  noise and is a hallmark of generic output. Spend motion where it carries
  meaning, and keep the rest still.
- **Always provide a reduced-motion path.** Some users are physically harmed by
  motion. The principle: every animation must have a calm fallback (instant state
  change or a simple opacity fade). The medium tier implements this via
  `prefers-reduced-motion`; the design must be authored so that removing motion
  loses delight but never loses function or meaning.

The test for any animation: *remove it.* If the interface is now confusing or
unresponsive, the motion was doing real work — keep it. If the interface is
merely less flashy, it was decoration — leave it removed.

A second test, for any motion *token*: it must name all three legs of the triad
(duration band, semantic easing category, animated property) and reference one of
the named easing categories rather than a raw curve. A token that specifies only
a duration, or an easing curve with no bound property, is incomplete.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
