# Spacious — Buttons

Spacious button styling — generous 24px+ padding, blue-violet primary, soft 8px radius, soft shadow on hover, calm transitions, full state set.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" /> for Spacious. The
slot owns the variants, the sizing contract, and the full state set; this file
supplies the look. The Spacious signature on a button is **generous padding** — a
button is given room, not squeezed to its label — plus a quiet blue-violet primary
and calm, instant feedback.

## Foundations

Buttons draw from the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/brand.md" />: the 8pt
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />, `--color-accent`, `--radius`, and the calm
motion vocabulary. Padding is the load-bearing choice — Spacious buttons pad to
`--space-4` (24px) horizontally where other brands use 12–16px.

```css
.btn {
  font-family: var(--font-body);
  font-weight: 600;
  border-radius: var(--radius);            /* 8px, soft */
  padding-block: var(--space-3);           /* 16px */
  padding-inline: var(--space-4);          /* 24px — generous */
  min-block-size: 44px;                    /* target floor */
  transition: background-color var(--dur-fast) var(--ease-standard),
              box-shadow var(--dur-fast) var(--ease-standard);
}
```

## Variants

| Variant | Fill | Text | Border |
|---------|------|------|--------|
| **Primary** | `--color-accent` (blue) | `#FFFFFF` | none |
| **Secondary** | `--color-surface` | `--color-accent` | `1px --color-border` |
| **Ghost / tertiary** | transparent | `--color-text` | none |
| **Danger** | `--color-danger` | `#FFFFFF` | none |
| **Link-style** | none | `--color-accent`, underline on hover | none |

One primary per view (umbrella rule). The accent is the only saturated color a
button uses; secondary and ghost stay neutral so the primary reads clearly.

```css
.btn--primary   { background: var(--color-accent); color: #fff; }
.btn--secondary { background: var(--color-surface); color: var(--color-accent);
                  border: 1px solid var(--color-border); }
.btn--ghost     { background: transparent; color: var(--color-text); }
.btn--danger    { background: var(--color-danger); color: #fff; }
```

## Sizing

Sizes scale padding and type together so the text-to-edge proportion holds; even
the small size keeps a generous feel and the ≥44px target.

```css
.btn--sm { padding-block: var(--space-2); padding-inline: var(--space-3); font-size: 14px; }
.btn--md { padding-block: var(--space-3); padding-inline: var(--space-4); font-size: 16px; }
.btn--lg { padding-block: var(--space-4); padding-inline: var(--space-5); font-size: 18px; }
.btn--block { inline-size: 100%; }
```

## States

| State | Treatment |
|-------|-----------|
| **Default** | Resting fill per variant |
| **Hover** | Slightly deeper accent + `--shadow-soft` gently appears — calm lift, instant |
| **Focus** | Visible ring: `0 0 0 3px` accent at low opacity, never suppressed |
| **Active/pressed** | Deepest accent, shadow removed — tactile, immediate |
| **Disabled** | `opacity: 0.5`, no shadow, `cursor: not-allowed`; reason discoverable |
| **Loading** | Spinner replaces label; width held stable; double-submit prevented |

```css
.btn--primary:hover  { background: #2F6FDB; box-shadow: var(--shadow-soft); }
.btn--primary:active { background: #2862C7; box-shadow: none; }
.btn:focus-visible   { outline: none; box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.4); }
.btn[disabled]       { opacity: 0.5; box-shadow: none; cursor: not-allowed; }

@media (prefers-reduced-motion: reduce) {
  .btn { transition-duration: 1ms; }
}
```

The soft shadow on hover is the single brand flourish — diffused, never hard. See
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" /> for the CSS carriers
(custom properties, `:focus-visible`, `box-shadow`).

## Anti-patterns (brand-specific)

- Tightening padding below `--space-3` / `--space-4` to fit more buttons — breaks
  the spacious feel; let them wrap or stack instead.
- A hard, dark drop shadow on hover — Spacious shadows are soft and diffused.
- Bouncy or springy press animation — the press is calm and instant.
- Two saturated variants competing; keep secondary/ghost neutral.
