# Riso — Brand Foundations

Riso brand foundations — risograph essence, two-color palette on warm paper, Space Grotesk type, snappy print motion, and the signature offset print-shadow.

Riso is a **two-color, risograph-inspired** brand: fluorescent pink and federal
blue printed on one continuous sheet of warm off-white paper. It feels printed,
tactile, bright, and handmade — but never messy. The whole product reads like a
well-registered two-ink risograph poster: blue does all the structural ink work
(text, headings, outlines, the offset shadow), pink does all the inviting
(actions, selection, focus, joy). This file establishes the tokens every Riso
component file builds on; the slots themselves live in the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />.

## Essence

The risograph print feel comes from three commitments held together:

- **One paper surface, always.** The entire app sits on `--paper`. Sections do
  not alternate backgrounds — the sheet never changes (see Do / Don't).
- **Two inks create the world.** Blue structures, pink invites. There is no
  third decorative accent. The constraint is the aesthetic.
- **Offset is personality, not elevation.** Depth is suggested by a blurless,
  misregistered blue shadow — the ink "printed slightly off" — not by soft
  digital drop shadows.

**When to use Riso:** playful, expressive products that want a printed,
hand-made-precise character — marketing sites, creative tools, community apps,
docs that want personality. **When not to:** dense enterprise dashboards or
data-tables where the offset shadow and poster type would fight the density, or
brands that need many accent colors.

## Color palette

Riso defines a small set of primitives and wires them into the umbrella's
semantic roles (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />). Values are authoritative; do not
invent new hues. Delivered as CSS custom properties (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />):

| Token | Value | Role |
|-------|-------|------|
| `--paper` | `#FFF8EC` | Continuous warm off-white page canvas — the only ground |
| `--paper-deep` | `#F7EBD8` | Subtle paper variation (sunken wells, hovered rows) |
| `--ink-blue` | `#2C40A7` | Federal blue — headings, body emphasis, outlines, dividers, print-shadow |
| `--ink-pink` | `#F237A1` | Fluorescent pink — interaction, selection, active, focus, emphasis ONLY |
| `--print-shadow` | `#2C40A7` | Offset shadow layer (same blue as the ink) |
| `--text` | `#111827` | Default readable body text (near-black for long copy) |
| `--surface` | `#FFFFFF` | Utility foreground surface only (rare; not a section background) |
| `--success` | `#16A34A` | Positive feedback — reserved, feedback only |
| `--warning` | `#D97706` | Caution — reserved, feedback only |
| `--danger` | `#DC2626` | Errors / destructive — reserved, feedback only |

```css
:root {
  --paper: #FFF8EC;
  --paper-deep: #F7EBD8;
  --ink-blue: #2C40A7;
  --ink-pink: #F237A1;
  --print-shadow: #2C40A7;
  --text: #111827;
  --surface: #FFFFFF;
  --success: #16A34A;
  --warning: #D97706;
  --danger: #DC2626;
}
```

Notes on the constraint and contrast:

- **Pink is interaction, never body text.** `--ink-pink` carries actions,
  active/selected states, focus accents, and joyful emphasis. Body copy is
  `--text`; headings/structure are `--ink-blue`.
- **No additional decorative accents.** The only colors beyond blue/pink are the
  three status hues, and they appear *only* in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/feedback.md" /> — never
  decoratively.
- **Contrast (verify in situ).** `--ink-blue #2C40A7` on `--paper #FFF8EC` is
  ~8.6:1 — comfortable for headings and body. `--ink-pink #F237A1` on `--paper`
  is ~3.4:1 — it clears the 3:1 bar for UI components, large text (≥18px / ≥14px
  bold), and focus rings, but **not** the 4.5:1 body-text bar. So pink fills
  buttons and large/active labels; pink text on paper must be large or bold, and
  small pink-on-paper text is disallowed. `--text` on `--paper` is AAA. Always
  verify against the *actual* background per <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />.

## Typography

Riso uses **Space Grotesk** for everything visible — body, UI, labels, forms,
nav, buttons, and display headings — with **Overpass Mono** for code and
technical values. A single grotesque superfamily, made to feel like a print
poster through weight and tracking rather than a second display face (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />).

| Role | Token | Size | Weight | Leading |
|------|-------|------|--------|---------|
| Display / hero | `--font-display` | 32px | 800–900 (rare poster moments) | 1.05 |
| Page heading (h1) | `--font-h1` | 24–32px | 700 | 1.1 |
| Section heading | `--font-h2` | 20px | 600 | 1.2 |
| Card title | `--font-h3` | 16px | 600 | 1.3 |
| Body | `--font-body` | 16px | 400 | 1.55 |
| Label | `--font-label` | 14px | 500 | 1.4 |
| Caption / meta | `--font-caption` | 12px | 500 | 1.4 |

```css
:root {
  --font-sans: "Space Grotesk", system-ui, sans-serif;
  --font-mono: "Overpass Mono", ui-monospace, monospace;
}
```

Type scale: **12 / 14 / 16 / 20 / 24 / 32px**. Spacing scale (4px base): **4 / 8
/ 12 / 16 / 24 / 32px**, generous and rhythmic. The **print-poster heading feel**
comes from heavy weights (700+) in `--ink-blue`, tightened leading on display
sizes, and — for hero moments — wide uppercase tracking. Reserve 800–900 for
genuine poster moments; identity lives in the large, short text, readability in
the long, small text.

## Motion vocabulary

Motion is snappy, tactile, and print-flavored — the feel of a sticker being
pressed down, not a soft fade (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />). Durations stay in the
instant-to-fast bands; the signature gesture is a tiny **registration shift**:
on press, an element nudges toward its offset shadow as if the ink and the page
realign.

| Token | Value | Use |
|-------|-------|-----|
| `--dur-instant` | 90ms | Hover, press, small state flips |
| `--dur-fast` | 180ms | Dropdowns, toggles, tooltips, active transitions |
| `--dur-moderate` | 300ms | Modals, drawers, banners |
| `--ease-out` | `cubic-bezier(0.2, 0.8, 0.2, 1)` | Entering / responding to input |
| `--ease-in` | `cubic-bezier(0.4, 0, 1, 1)` | Leaving |

```css
@media (prefers-reduced-motion: reduce) {
  * { transition-duration: 1ms !important; animation: none !important; }
}
```

Snappy, never springy-bouncy; the registration shift is a 2–3px translate, not an
overshoot. Reduced-motion is mandatory — the shift collapses to an instant
color/state change, losing the tactility but never the meaning.

## Signature effect — the offset print-shadow

The defining Riso mechanic. A **blurless blue double-edge** that simulates
risograph misregistration: the blue ink layer printed a few pixels off from the
paper, so a hard blue shadow peeks out below-right. No blur radius — that is what
separates it from a generic drop shadow.

```css
:root {
  --print-shadow-sm: 3px 3px 0 var(--print-shadow);
  --print-shadow-md: 6px 6px 0 var(--print-shadow);
  --print-shadow-lg: 10px 10px 0 var(--print-shadow);
}

.riso-card {
  background: var(--paper);
  border: 2px solid var(--ink-blue);
  border-radius: 4px;
  box-shadow: var(--print-shadow-md);
  transition: transform var(--dur-instant) var(--ease-out),
              box-shadow var(--dur-instant) var(--ease-out);
}
/* registration shift: the object presses down toward its shadow */
.riso-card:active {
  transform: translate(3px, 3px);
  box-shadow: var(--print-shadow-sm);
}
```

Where it applies: **important cards**, **primary buttons**, **banners/alerts**,
hero objects and stickers, and occasionally large display headings (as a
text-shadow `4px 4px 0 var(--ink-blue)`). Use it **sparingly** — it marks the
few things that matter, not every box. The offset is always blue and always
blurless.

## Do / Don't

**Do**
- Render everything on one continuous `--paper` surface.
- Reserve `--ink-pink` for interaction, selection, active, and focus.
- Structure with `--ink-blue`: text emphasis, headings, outlines, dividers.
- Use the offset print-shadow as the signature depth cue, sparingly.
- Use Space Grotesk; lean on weight and uppercase tracking for poster feel.

**Don't**
- Don't alternate section backgrounds or drop in a pure-white page ground.
- Don't use pink for body text or as a structural color.
- Don't add soft/blurred drop shadows, gradients, glassmorphism, or 3D.
- Don't introduce a third decorative accent (status hues are feedback-only).
- Don't put personality into body copy — keep long text quiet and legible.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/navigation.md" />
