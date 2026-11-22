# Dramatic — Buttons

Dramatic buttons — violet-glow primary on near-black with 900 labels, rose secondary/danger, focus rings that survive the dark, and state-by-glow-intensity.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />
for Dramatic. A button on this brand is a lit object on a dark stage: its label is
**900-weight Outfit**, and the primary action carries a violet glow that reads as a
spotlight. See <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/brand.md" /> for the tokens referenced below.

## Variants

| Variant | Look |
|---------|------|
| **Primary** | Filled violet (`--bd-accent`) with `--bd-on-accent` 900 label; soft violet glow. The one spotlit action per view. |
| **Secondary** | Transparent fill, `--bd-border` hairline, `--bd-text` 900 label; rose-tinted on hover. Sits beside primary. |
| **Ghost / tertiary** | No border, no fill; `--bd-text-muted` 900 label; surface lifts to `--bd-surface-raised` on hover. |
| **Danger / destructive** | Filled rose (`--bd-accent-2`); 900 label; rose glow. Destructive intent overrides emphasis. |
| **Link-style** | Inline, `--bd-accent` text, 400 weight, underline on hover. |

Labels are **always 900** on filled and emphasis buttons — the shout. Only the
link-style variant drops to 400 so it reads as inline text. One primary per
context.

```css
.bd-btn {
  font-family: var(--bd-font);
  font-weight: var(--bd-weight-display); /* 900 */
  font-size: var(--bd-text-body);
  letter-spacing: var(--bd-track-display);
  border-radius: var(--bd-radius, 0.5rem);
  padding-block: 0.625rem;
  padding-inline: 1.25rem;
  min-block-size: 2.75rem; /* ≥44px target */
  transition: background-color var(--bd-dur-press) var(--bd-ease-out),
              box-shadow var(--bd-dur-fast) var(--bd-ease-out);
}

.bd-btn--primary {
  background: var(--bd-accent);
  color: var(--bd-on-accent);
  box-shadow: 0 0 0 0 transparent;
}
.bd-btn--secondary {
  background: transparent;
  color: var(--bd-text);
  border: 1px solid var(--bd-border);
}
.bd-btn--danger {
  background: var(--bd-accent-2);
  color: var(--bd-on-accent);
}
```

## Sizing

Small / medium / large scale padding and type together; the interactive target
stays **≥44px** even for the small size (pad the hit area, don't shrink it). A
full-width option exists for stacked mobile contexts. Icon-only buttons carry an
accessible name and meet the same target.

## States — drama by glow intensity

The press/hover band stays **instant** (`--bd-dur-press`); only the glow bloom uses
the fast band. State is carried by **glow intensity and fill**, never glow alone.

| State | Treatment |
|-------|-----------|
| **Default** | Resting fill; no glow (primary) / hairline border (secondary). |
| **Hover** | Glow blooms — `box-shadow: 0 0 24px color-mix(in oklch, var(--bd-accent) 55%, transparent)`; fill brightens slightly. |
| **Focus** | Visible ring that survives the dark — `outline: 2px solid var(--bd-on-accent); outline-offset: 2px`, plus an outer accent halo. Never suppressed (≥3:1). |
| **Active / pressed** | Glow tightens, fill darkens a step — immediate, tactile. |
| **Disabled** | Fill drops to `--bd-surface-raised`, label to `--bd-text-subtle`; no glow; still legible, not invisible. Pair with a tooltip explaining *why*. |
| **Loading** | Label swapped for a spinner; width held stable; glow steady; double-submit prevented. Distinct from disabled. |

```css
.bd-btn--primary:hover {
  background: color-mix(in oklch, var(--bd-accent) 90%, white);
  box-shadow: 0 0 24px color-mix(in oklch, var(--bd-accent) 55%, transparent);
}
.bd-btn:focus-visible {
  outline: 2px solid var(--bd-on-accent);
  outline-offset: 2px;
  box-shadow: 0 0 0 4px var(--bd-border-glow);
}
.bd-btn--danger:focus-visible {
  box-shadow: 0 0 0 4px color-mix(in oklch, var(--bd-accent-2) 45%, transparent);
}
@media (prefers-reduced-motion: reduce) {
  .bd-btn { transition: none; }
}
```

## Responsibilities

- **Action-named, 900 labels** ("Save changes", "Delete") that stay consistent
  through the flow; result feedback via
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/feedback.md" />.
- **Stable layout** — width never jumps between label, loading, and success.
- **Keyboard operable** with the visible focus ring above; the glow is decoration,
  the outline is the real focus signal.
- Color is never the sole carrier of danger/disabled — fill, weight, and
  position back it up.

## Anti-patterns

- Two violet primaries glowing in one view.
- A middle-weight (600/700) label — labels are 900 or, for link-style, 400.
- Glow as the only focus indicator (always keep the outline).
- A press with no instant feedback because the slow reveal timing leaked onto it.
- Disabled buttons faded into invisibility on the dark ground.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_accessibility.md" />
