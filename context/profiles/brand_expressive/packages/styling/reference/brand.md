# Expressive — Brand

Expressive brand identity card — essence, pink+blue dual-accent palette with contrast notes, IBM Plex Mono everywhere with weight-as-hierarchy, playful spring motion, structured-chaos shape system, and do/don't.

The identity card for **Expressive**: a vibrant, personality-driven design system
that pairs bold color with playful layout and a single monospaced typographic voice
to feel energetic and creative while staying structurally sound. The mono voice is
the through-line — it shows up in every label, heading, and field, and it is what
makes the brand immediately recognizable.

## Essence

Energetic, creative, distinct. Expressive wants the interface to have an opinion —
it reads as made by people with taste rather than generated from a template. The
discipline that keeps it from tipping into noise is structure: a strict grid, a
fixed <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />, and <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" /> that always
answers a question. Playful, never random.

**Use Expressive for:** creative tools, developer and design products, playful
SaaS that wants to escape the blue-and-sans-serif template, agency and portfolio
sites, and any surface that benefits from a strong, human voice. **Avoid it for:**
high-trust, low-affect contexts (banking, medical, legal) where the monospace voice
and bright accents would undercut gravity.

## Color palette

A **dual-accent** system: pink and blue are co-equal accents, not a primary plus a
muted secondary. They carry identity together; either may anchor a given surface,
and they are balanced across a screen rather than one dominating (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> for the identity-vs-signal split).

```css
:root {
  /* Dual accents — co-equal */
  --be-pink:        #db2777; /* hot pink — actions, links, active */
  --be-pink-strong: #be185d; /* pressed / dense-on-light */
  --be-pink-soft:   #fce7f0; /* pink tint surface */
  --be-blue:        #2563eb; /* electric blue — the equal partner */
  --be-blue-strong: #1d4ed8; /* pressed */
  --be-blue-soft:   #e0ebff; /* blue tint surface */

  /* Status (reserved — never used as a third accent) */
  --be-success: #16a34a;
  --be-warning: #d97706;
  --be-danger:  #dc2626;
  --be-info:    var(--be-blue);

  /* Surface + text */
  --be-surface:    #ffffff;
  --be-surface-2:  #faf8fb; /* faint warm-pink-biased raised tint */
  --be-ink:        #111827; /* near-black body/heading */
  --be-ink-muted:  #4b5563;
  --be-border:     #111827; /* thick borders use ink, not grey */
}
```

The **dual-accent rule**: treat pink and blue as a pair. A button cluster makes the
primary pink and the secondary blue; a card grid may color-block alternating cards.
Do not introduce a third competing accent — status colors are reserved for
severity and never decorate. **Contrast:** pink `#db2777` (4.7:1 on white) and blue
`#2563eb` (5.1:1 on white) both clear AA for text; on filled pink/blue buttons use
white foreground (clears 4.5:1 on both). Verify accents in situ — both shift
against the soft-tint surfaces.

## Typography

**IBM Plex Mono everywhere** — display, headings, body, labels, data. This single
choice is the defining move (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" /> on single-superfamily
systems exploiting weight for contrast). Mono works at UI scale because Plex Mono is
humanist, not terminal-stiff: its even rhythm reads as deliberate and
technical-yet-warm, and the fixed advance width makes tabular data and code-adjacent
UIs align for free.

```css
:root {
  --be-font: "IBM Plex Mono", ui-monospace, "SFMono-Regular", monospace;

  /* Type scale — 14/16/18/24/32/40 */
  --be-text-caption: 14px;
  --be-text-body:    16px;
  --be-text-lead:    18px;
  --be-text-h3:      24px;
  --be-text-h2:      32px;
  --be-text-h1:      40px;
}
```

**Weight AS hierarchy.** With one face, weight is the primary hierarchy lever — use
the *full* 100–900 spectrum and the extremes for drama, not adjacent steps:

```css
--be-weight-display: 800; /* headlines, hero — black-ish */
--be-weight-strong:  700; /* section headings, button labels */
--be-weight-body:    400; /* body copy */
--be-weight-quiet:   300; /* captions, helper, metadata */
--be-weight-hair:    200; /* large thin display accents */
```

Mono for body needs managed readability: keep body line-height at `1.6`, constrain
the measure to ~60ch (mono runs wider per character than a proportional face, so err
shorter), and reserve weight `<300` for short, large text only. Headings tighten to
`1.05–1.15` leading with slightly negative tracking.

## Motion vocabulary

Playful and physical. Expressive leans on spring/overshoot eases that calmer brands
avoid — here they are part of the voice (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />: spring is a
deliberate brand choice, not a default). Energetic but never slow.

```css
:root {
  --be-ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);   /* bouncy overshoot */
  --be-ease-out:    cubic-bezier(0.22, 1, 0.36, 1);
  --be-dur-instant: 90ms;   /* hover/press micro-feedback */
  --be-dur-fast:    180ms;  /* most transitions */
  --be-dur-pop:     260ms;  /* spring entrances */
}
```

Signature interactions: a slight **scale + rotate** on hover (`scale(1.03)
rotate(-1deg)`), a tactile press that overshoots back, accent **color shifts**
pink↔blue on state change, and spring entrances for cards/toasts. Keep the critical
path instant; the bounce decorates feedback, it never gates the action. **Always
provide a reduced-motion fallback** — collapse springs to a 120ms opacity fade and
drop all rotation/scale (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" /> for the
`prefers-reduced-motion` mechanism).

## Shape & surface

Structured chaos. The grid stays strict; within it, geometry plays:

- **Varied radii** — chunky `--be-radius: 14px` on most surfaces, occasional pill
  (`9999px`) buttons, and a sharp `2px` corner for sticker accents.
- **Thick borders** — `2px`–`3px` solid `--be-border` (ink), not hairlines. The
  heavy outline is a signature.
- **Sticker layering** — small offset/rotated badges and accent blocks that sit
  *over* a card edge, with a hard offset shadow (`4px 4px 0 var(--be-ink)`) rather
  than a soft blur.
- **Color blocks** — solid pink or blue fills used as active markers, card headers,
  and section dividers.

## Do / Don't

- **DO** let IBM Plex Mono carry the voice in every role.
  **DON'T** mix in a proportional font casually — it breaks the whole identity.
- **DO** use the full 100–900 weight range so weight reads as hierarchy.
  **DON'T** lean on adjacent weights (400 vs 500); the difference disappears in mono.
- **DO** balance pink and blue as co-equal accents across a screen.
  **DON'T** add a third competing accent, or let one accent crowd out the other.
- **DO** use spring motion and slight rotation as personality.
  **DON'T** over-animate into chaos, or animate the critical path.
- **DO** keep the grid strict so the playful geometry has something to push against.
  **DON'T** mistake randomness for expressiveness — every offset is intentional.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/navigation.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/feedback.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
