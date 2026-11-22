# Expressive — Buttons

Expressive buttons — pink primary + blue secondary dual-accent, mono labels with weight emphasis, thick ink borders and chunky radii, springy scale+rotate hover and slam-into-shadow press, full state set.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" /> for the Expressive
brand. Buttons are loud, chunky, and tactile: pink for the main action, blue for its
co-equal partner, mono labels carrying weight, thick ink borders, and a springy
press. Rendered as native `<button>` per
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />. Tokens from
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/brand.md" />.

## Variants (dual-accent)

```css
.be-btn {
  font: var(--be-weight-strong) var(--be-text-body)/1 var(--be-font);
  letter-spacing: 0.02em;
  padding: 12px 20px;
  border: 2px solid var(--be-border);
  border-radius: var(--be-radius, 14px);
  cursor: pointer;
  transition: transform var(--be-dur-instant) var(--be-ease-spring),
              background-color var(--be-dur-fast) var(--be-ease-out),
              box-shadow var(--be-dur-fast) var(--be-ease-out);
}

/* Primary — hot pink */
.be-btn--primary   { background: var(--be-pink); color: #fff;
                     box-shadow: 4px 4px 0 var(--be-ink); }
/* Secondary — the co-equal blue */
.be-btn--secondary { background: var(--be-blue); color: #fff;
                     box-shadow: 4px 4px 0 var(--be-ink); }
/* Ghost / tertiary — outline only */
.be-btn--ghost     { background: transparent; color: var(--be-ink); box-shadow: none; }
/* Danger — reserved red, never an accent */
.be-btn--danger    { background: var(--be-danger); color: #fff;
                     box-shadow: 4px 4px 0 var(--be-ink); }
/* Link-style — inline, weight does the lifting */
.be-btn--link      { border: none; background: none; padding: 0;
                     color: var(--be-pink); font-weight: var(--be-weight-strong);
                     text-decoration: underline; box-shadow: none; }
```

One primary per view (umbrella rule). Pink reads as *the* action; blue secondary
sits beside it without competing. Pill option (`border-radius: 9999px`) for
high-energy CTAs.

## Sizing

Padding and type scale together; hit target stays ≥ 44px.

```css
.be-btn--sm { padding: 8px 14px;  font-size: var(--be-text-caption); }
.be-btn--md { padding: 12px 20px; font-size: var(--be-text-body); }
.be-btn--lg { padding: 16px 28px; font-size: var(--be-text-lead);
              font-weight: var(--be-weight-display); }
.be-btn--block { width: 100%; }
```

Icon-only buttons keep a square ≥ 44px footprint and an `aria-label`.

## States

The signature press: the offset shadow collapses as the button physically moves into
it, plus a playful tilt on hover.

```css
.be-btn--primary:hover,
.be-btn--secondary:hover { transform: translate(-1px, -1px) rotate(-1deg) scale(1.03);
                           box-shadow: 5px 5px 0 var(--be-ink); }
.be-btn:focus-visible    { outline: 3px solid var(--be-blue); outline-offset: 3px; }
.be-btn:active           { transform: translate(4px, 4px); box-shadow: 0 0 0 var(--be-ink); }
.be-btn--primary:active  { background: var(--be-pink-strong); }
.be-btn[disabled]        { background: #e5e7eb; color: #9ca3af; border-color: #d1d5db;
                           box-shadow: none; transform: none; cursor: not-allowed; }
.be-btn[aria-busy="true"]{ color: transparent; } /* spinner overlay; width stays fixed */
```

- **Hover** — lift + 1° tilt + slight scale (instant band; never gates the click).
- **Focus** — 3px blue ring at 3px offset, contrasts against pink/blue fills.
- **Active** — slams into its shadow (`translate(4px,4px)`), tactile and immediate.
- **Disabled** — neutral grey, no shadow, no tilt; reason surfaced via tooltip.
- **Loading** — `aria-busy`, label swapped for a spinner, width frozen, double-submit
  blocked (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/feedback.md" />).

Labels are action-named ("Save changes", not "OK") and mono-cased; use
`--be-weight-display` on `lg` for emphasis rather than ALL-CAPS noise.

## Anti-patterns

- Two pink primaries competing — demote one to blue or ghost.
- Soft blurred drop-shadows — Expressive uses the hard offset shadow.
- Hairline borders — always ≥ 2px ink.
- Rotation/scale so large the press feels unstable; keep tilt ≤ 1° and scale ≤ 1.03.
- Color-only disabled state with no explanation.
