# Brutalism — Brand Foundation

Brutalism brand foundation — terracotta+ochre material palette, Darker Grotesque extreme weights, abrupt mechanical motion, sharp corners and thick borders, and the do/don't list.

Brutalism is raw structural honesty. It takes its name and its values from the
1950s architectural movement that celebrated exposed concrete (*béton brut*) and
refused to hide how a building was made. Translated to a UI: the structure is the
style. Borders are thick and visible, type is stark and heavy, corners are sharp,
and nothing is softened to disappear. Every element is honest about what it is.

This is the concrete realization of the umbrella's
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />, and <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />
principles for the Brutalism brand. The component files cross-reference the values
defined here.

## Essence

Think exposed concrete, not polished marble. Brutalist UI rejects the conventions
of polish — the soft drop shadow, the gentle gradient, the carefully rounded
corner trying to vanish. Where mainstream UI smooths everything into a friendly
blur, Brutalism leaves the grid showing, the seams visible, the weight obvious.
Function over decoration; deliberate roughness; the bones on display.

**When to use Brutalism**

- Portfolios and personal sites making a confident, anti-corporate statement.
- Developer tools, dashboards, and editorial products where directness and
  legibility beat ornament.
- Brands that want to signal craft, honesty, or counter-cultural edge.

**When not to**

- Soft, reassuring consumer products (wellness, finance-for-anxious-users,
  children's apps) where the visual aggression works against trust.
- Dense enterprise tables that need calm neutrality over confrontation.

## Color palette

A deliberately **non-digital** palette: terracotta and ochre feel like fired
clay, iron oxide, and aged stone — they exist in the physical world. Surfaces are
raw white like unpainted concrete; text is near-black. Borders are a *primary*
structural element, not a hairline afterthought.

```css
:root {
  /* Brand primitives — material world */
  --bb-terracotta: #DD614C;  /* fired clay — primary action/link/active */
  --bb-ochre:      #DAA144;  /* brick & sandstone — supporting accent */

  /* Status (kept honest, high-contrast) */
  --bb-success: #16A34A;
  --bb-warning: #D97706;
  --bb-danger:  #DC2626;

  /* Surfaces & ink */
  --bb-surface:  #FFFFFF;    /* raw white — backgrounds, cards */
  --bb-concrete: #F4F2EE;    /* sunken/well — faint warm grey */
  --bb-text:     #111827;    /* near-black — body, headings, labels */

  /* Borders are the identity */
  --bb-border:        var(--bb-text);   /* default border ink */
  --bb-border-w:      3px;              /* default structural weight */
  --bb-border-w-thin: 2px;
  --bb-border-w-bold: 4px;

  /* Semantic wiring (components reference these, never primitives) */
  --color-accent:            var(--bb-terracotta);
  --color-accent-foreground: var(--bb-surface);
  --color-accent-2:          var(--bb-ochre);
  --bg-surface:              var(--bb-surface);
  --bg-sunken:               var(--bb-concrete);
  --text-primary:            var(--bb-text);
  --border:                  var(--bb-border);
}
```

Contrast notes: terracotta `#DD614C` and ochre `#DAA144` are mid-lightness — use
near-black `--bb-text` on them for fills, and reserve white text for the darker
terracotta only where it clears 4.5:1. Borders are always full-ink `--bb-text`
against white, so component boundaries are unambiguous (this is Brutalism's
accessibility win — see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> contrast thresholds). Status hues are
reserved: terracotta is *brand*, danger red `#DC2626` is *error*; never mix them.

## Typography

**Darker Grotesque** for everything — a condensed grotesque with a tall x-height
and an extreme weight range (100–900). Hierarchy comes from raw contrast, not
refinement: pair a very light weight against a very heavy one (binary contrast,
per <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />: use the extremes, not adjacent weights).

```css
:root {
  --bb-font: "Darker Grotesque", system-ui, sans-serif;
  --bb-font-mono: "JetBrains Mono", ui-monospace, monospace;

  --bb-w-light: 300;   /* eyebrows, captions — the quiet extreme */
  --bb-w-body:  500;
  --bb-w-heavy: 800;   /* headings, button labels — the loud extreme */
  --bb-w-black: 900;   /* display */

  /* Aggressive scale (~1.333 perfect fourth) — big and confrontational */
  --bb-text-sm:  0.875rem;
  --bb-text-base: 1rem;
  --bb-text-lg:  1.5rem;
  --bb-h3: 2rem;
  --bb-h2: 2.75rem;
  --bb-h1: 3.75rem;
  --bb-display: 5.5rem;

  --bb-track-tight: -0.02em;  /* heavy display */
  --bb-track-wide:  0.08em;   /* uppercase labels/eyebrows */
}
```

Display and headings run **heavy and uppercase** with tight tracking; eyebrows
and labels run **light and uppercase** with wide tracking. Leading is tight on
big type (1.0–1.1) so headlines read as solid blocks.

## Motion vocabulary

Motion is **abrupt, mechanical, snappy** — no soft easing curves. Brutalism cuts
rather than fades; state changes are hard swaps or border-thickness jumps, not
gentle transitions. This is a deliberate brand voice over the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" /> principle.

```css
:root {
  --bb-ease: steps(1, end);   /* hard cut — the brutalist default */
  --bb-ease-snap: linear;     /* when a transition must move, keep it mechanical */
  --bb-dur-instant: 0ms;      /* most state changes: hard swap */
  --bb-dur-fast: 80ms;        /* the rare animated property */
}

@media (prefers-reduced-motion: reduce) {
  /* Already near-instant; hard cuts are an honest reduced-motion fallback. */
  * { transition-duration: 0ms !important; }
}
```

Animate only border thickness, fill color, and offset-shadow position — never
opacity fades or scale springs. Durations stay in the instant band; a brutalist
press *snaps*.

## Shape & surface

- **Corners are sharp.** `border-radius: 0` everywhere. No exceptions.
- **Borders are thick and solid.** Default `3px`, `2px` for dense controls, `4px`
  for emphasis. Always solid, full-ink.
- **No soft shadows, ever.** The only permitted "shadow" is a **hard offset
  block** — a solid color offset with zero blur, reading as a second pane behind
  the element, not a glow.

```css
.bb-surface { border: var(--bb-border-w) solid var(--bb-border); border-radius: 0; }
.bb-offset  { box-shadow: 6px 6px 0 0 var(--bb-text); } /* hard block, no blur */
```

The grid is exposed: dividers between regions are real `--bb-border-w` rules, not
faint hairlines.

## Do / Don't

- **DO** show borders and the underlying grid; let structure be the decoration.
- **DON'T** round corners or add blurred drop shadows — both betray the aesthetic.
- **DO** use extreme weight contrast (300 vs. 800/900) for hierarchy.
- **DON'T** use gradients of any kind; fills are flat and material.
- **DO** let elements feel heavy, blocky, and honest about their function.
- **DON'T** soften interactions with easing; cut hard and snap.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/navigation.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/feedback.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
