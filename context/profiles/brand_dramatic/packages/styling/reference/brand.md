# Dramatic — Brand Foundation

Dramatic brand foundation — near-black canvas, violet+rose stage-light accents, Outfit 400/900 binary weights, cinematic motion, and dark-surface glow discipline.

Dramatic is a high-contrast, dark-surface aesthetic with the intensity of a film
title sequence. The near-black surface is not a background — it is **the stage**.
Light text burns against it, and two accents (violet and rose) cut through the
dark like spotlights. The whole idiom is built on a single move: extreme contrast,
held with discipline.

## When to use Dramatic

Reach for Dramatic when the surface should feel cinematic and premium:

- **Launch / hero pages** — the oversized 900 display headline on near-black is
  the signature moment.
- **Night-mode-first products** — media players, creative tools, dashboards meant
  to be lived in for hours.
- **Premium / editorial brands** where theatrical restraint reads as confidence.

Avoid it for dense, data-heavy admin UIs that need a calm light ground, or where a
client requires a light theme as the default — a light background breaks the
idiom entirely (see Do / Don't).

## Color palette

The palette is **duochrome on near-black**: a near-true-black ground, near-white
text, and exactly two saturated accents. Color is a scarce resource here — most of
every screen is dark neutral, and violet/rose appear only where they carry meaning
(see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).

```css
:root {
  /* Surface ladder — light recedes in dark UIs, so raised = lighter */
  --bd-surface:        #09090b; /* near-true-black — the stage / base */
  --bd-surface-raised: #18181b; /* cards, popovers — one step up */
  --bd-surface-sunken: #050506; /* wells, inputs — one step down */
  --bd-surface-overlay:#0c0c0f; /* modal body, behind a scrim */

  /* Text — near-white burns against the ground (>19:1) */
  --bd-text:        #fafafa; /* primary body + 900 headings */
  --bd-text-muted:  #a1a1aa; /* secondary / supporting (4.5:1+ on surface) */
  --bd-text-subtle: #71717a; /* captions, disabled-adjacent */

  /* Accents — the two stage lights */
  --bd-accent:        #8b5cf6; /* vivid violet — primary actions, key highlight */
  --bd-accent-2:      #f43f5e; /* hot rose — secondary accent, danger-adjacent */
  --bd-on-accent:     #fafafa; /* text on a filled accent */

  /* Status (tuned to read on near-black) */
  --bd-success: #16a34a;
  --bd-warning: #d97706;
  --bd-danger:  #dc2626;

  /* Borders — minimal; the dark + light contrast does the grouping */
  --bd-border:       color-mix(in oklch, var(--bd-text) 10%, transparent);
  --bd-border-glow:  color-mix(in oklch, var(--bd-accent) 45%, transparent);
}
```

### Surface steps for depth

In a dark UI shadows barely read, so elevation is expressed by making raised
surfaces *lighter* (`--bd-surface-raised`) and by adding a hairline border or an
accent glow — never by reusing light-mode drop shadows. The ladder
(sunken → base → raised → overlay) gives depth without a single light panel.

### Contrast discipline

Light-on-dark legibility is the entire point, but the accents must clear WCAG too:

- Body text (`--bd-text` on `--bd-surface`) is well above 19:1 — luminous by
  construction.
- **Accents are not text colors at body size.** Violet (`#8b5cf6`) and rose
  (`#f43f5e`) on near-black sit near ~5–6:1 — fine for large 900 labels, button
  fills, and UI/graphical objects (≥3:1), but verify any small accent text against
  its *actual* surface (a card is lighter than the base — recheck there).
- Glows are decoration; never let a glow be the *only* signal for a state (pair
  with weight, fill, or an icon).

### Dark-first theming

Dramatic is dark by default and does not ship a light theme. Declare the intent so
the browser and form controls cooperate:

```css
:root { color-scheme: dark; }
```

There is no `prefers-color-scheme: light` branch — a light ground is out of idiom.
The only light-related concern is honoring the user's *reduced-transparency* and
*reduced-motion* preferences (see Motion).

## Typography — the two-weight system

The typeface is **Outfit**, a geometric variable sans, restricted to **exactly two
weights: 400 and 900**. This binary is the brand's typographic signature: every
text element is either a *shout* (900) or a *whisper* (400). There is no "kind of
important."

```css
:root {
  --bd-font: "Outfit", system-ui, sans-serif;
  --bd-weight-body:    400; /* body, descriptions, labels, helper text */
  --bd-weight-display: 900; /* headings, hero text, button + nav labels */

  /* Scale: 12 / 14 / 16 / 20 / 24 / 32 (px) */
  --bd-text-caption: 0.75rem;  /* 12 */
  --bd-text-small:   0.875rem; /* 14 */
  --bd-text-body:    1rem;     /* 16 */
  --bd-text-lead:    1.25rem;  /* 20 */
  --bd-text-h2:      1.5rem;   /* 24 */
  --bd-text-display: 2rem;     /* 32 — and up, fluid, for heroes */

  --bd-track-display: -0.02em; /* tight tracking on big 900 type */
  --bd-track-body:    0;       /* normal on 400 body */
  --bd-leading-display: 1.05;  /* big type needs little leading */
  --bd-leading-body:    1.6;   /* comfortable reading band */
}
```

- **900 (Black)** — headings, hero/display text, button labels, active nav, field
  group headers. Tight tracking; tight leading; this is where identity lives.
- **400 (Regular)** — body copy, descriptions, form labels, helper text, inactive
  nav. Normal tracking; comfortable leading; this is the readable workhorse.
- **Never use 500/600/700.** The drama is the *jump* from light to black. A middle
  weight collapses the binary into mush and instantly reads as off-brand (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" /> on using the
  extremes of a family for contrast).

## Motion vocabulary

Dramatic motion is **cinematic**: slow, deliberate reveals rather than perky
micro-interactions. Things fade up through the dark; spotlight glows bloom in.
Durations sit at the long end of the bands — drama needs time — but never so long
they become latency (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

```css
:root {
  --bd-dur-press:  90ms;   /* instant — press/hover feedback stays fast */
  --bd-dur-fast:   220ms;  /* dropdowns, toggles */
  --bd-dur-reveal: 520ms;  /* section + hero reveals (slow band) */
  --bd-ease-out:   cubic-bezier(0.16, 1, 0.3, 1); /* deliberate settle */
  --bd-ease-in:    cubic-bezier(0.7, 0, 0.84, 0); /* accelerate away */
}
```

- **Reveals** fade and rise a few pixels, ease-out, on the slow band; stagger
  grouped items by a small delay so a hero sequence unfolds like a title card.
- **Spotlight reveals** — an accent glow that blooms from low to full opacity as an
  element enters or activates.
- **Feedback stays instant** — press and hover never inherit the slow reveal
  timing; a sluggish press feels broken.
- **Reduced motion is mandatory.** Under `prefers-reduced-motion: reduce`, drop all
  travel and glow-bloom and fall back to an instant state change or a plain opacity
  fade. The reveal loses theatre but never loses meaning (web mechanics inherited
  from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />).

## Shape & surface

- **Dark surface steps for depth**, not light panels — use the surface ladder
  above; raised = lighter, plus a hairline `--bd-border`.
- **Minimal borders.** Lean on light-on-dark contrast to separate regions; add a
  border only where contrast alone won't group (and prefer a faint accent-tinted
  border over a heavy grey one).
- **Glow / vignette accents** are the signature surface device: a soft violet or
  rose glow (`box-shadow` with a wide blur, low opacity) behind a key element reads
  as stage lighting. Use vignettes to focus attention on the hero against the dark.
- **Radius is restrained** — sharp or subtly rounded corners (`--bd-radius:
  0.5rem`); the drama comes from contrast and light, not from soft pillows.

## Do / Don't

**Do**

- Use only Outfit 400 and 900 — embrace the binary whisper/shout.
- Let near-white type burn against the near-black canvas; that luminosity is free.
- Use violet and rose **sparingly**, as spotlights on key actions and accents.
- Give drama negative space — darkness is the medium; let elements breathe.
- Express depth with lighter raised surfaces and accent glows.

**Don't**

- Introduce a middle weight (500/600/700) — it kills the binary contrast.
- Use a light background by default — it breaks the theatrical idiom outright.
- Clutter the stage — dense, evenly-busy layouts undo the drama.
- Spread the accents everywhere — five glowing things means none stands out.
- Rely on a glow as the *only* signal for a state, or skip the reduced-motion
  fallback.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/navigation.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/feedback.md" />
