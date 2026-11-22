# Brutalism — Buttons

Brutalism buttons — thick-bordered solid blocks, terracotta/ochre fills, sharp corners, hard offset-shadow on press, heavy uppercase labels, states via border/fill swaps.

Concrete styling for the umbrella's
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />, in the Brutalism brand. A button is a
**thick-bordered solid block** that looks like it could be pressed with a fist.
Sharp corners, flat material fill, heavy uppercase label. Tokens come from
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/brand.md" />.

## Variants

Emphasis and intent map onto fill and border, never onto radius or shadow blur.

| Variant | Look |
|---------|------|
| **Primary** | Terracotta `--bb-terracotta` fill, `--bb-border-w` ink border, near-black heavy label. The one loud block per view. |
| **Secondary** | Ochre `--bb-ochre` fill, same ink border and weight. |
| **Ghost / tertiary** | White `--bb-surface` fill, `--bb-border-w` ink border — the structure alone carries it. |
| **Danger** | `--bb-danger` fill, ink border; label stays heavy. Intent overrides emphasis. |
| **Link-style** | No fill, no border; heavy underlined ink text. |

```css
.bb-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  border: var(--bb-border-w) solid var(--bb-border);
  border-radius: 0;
  background: var(--bb-surface);
  color: var(--bb-text);
  font-family: var(--bb-font);
  font-weight: var(--bb-w-heavy);
  text-transform: uppercase;
  letter-spacing: var(--bb-track-wide);
  padding-block: 0.6rem;
  padding-inline: 1.25rem;
  min-block-size: 44px;             /* target size — umbrella contract */
  cursor: pointer;
  transition: box-shadow var(--bb-dur-fast) var(--bb-ease-snap);
}
.bb-btn--primary   { background: var(--bb-terracotta); }
.bb-btn--secondary { background: var(--bb-ochre); }
.bb-btn--danger    { background: var(--bb-danger); color: var(--bb-surface); }
```

## Sizing

Padding and type scale together; the hit area never drops below `44px`. Icon-only
buttons keep the square ink border and carry an accessible name.

```css
.bb-btn--sm { padding-block: 0.4rem; padding-inline: 0.85rem; font-size: var(--bb-text-sm); }
.bb-btn--lg { padding-block: 0.85rem; padding-inline: 1.75rem; font-size: var(--bb-text-lg); }
.bb-btn--block { display: flex; inline-size: 100%; }
```

## States

State changes are **fill swaps and border-thickness jumps**, not soft fades. The
one signature move: pressing the button drives a **hard offset block** behind it
(the only "shadow" Brutalism allows — see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/brand.md" /> shape & surface),
then snaps flat on release.

| State | Brutalist expression |
|-------|----------------------|
| **Default** | Flat block, `--bb-border-w` border. |
| **Hover** | Fill darkens one material step (no glow); cursor pointer. |
| **Focus** | `--bb-border-w-bold` (4px) ink border via `:focus-visible` — a thickness jump, not a soft ring. |
| **Active / pressed** | Hard offset block appears, then collapses to flat — a mechanical "clunk". |
| **Disabled** | Fill desaturates to `--bb-concrete`, border stays visible (boundary never disappears), `cursor: not-allowed`. |
| **Loading** | Label swapped for a mechanical step-rotated mark; width held stable; double-submit blocked. |

```css
.bb-btn:hover           { filter: brightness(0.92); }       /* flat darken, no blur */
.bb-btn:focus-visible   { outline: none; border-width: var(--bb-border-w-bold); }
.bb-btn:active          { box-shadow: 4px 4px 0 0 var(--bb-text); transform: translate(-2px, -2px); }
.bb-btn:disabled        { background: var(--bb-concrete); color: #6b7280; cursor: not-allowed; }
```

## Responsibilities

- **Action-named heavy labels** ("PUBLISH", "DELETE"), consistent through the flow.
- **Distinguish disabled from loading** — desaturated-but-bordered vs. a stepped
  working mark.
- **Visible focus** is mandatory: the border thickens, it is never suppressed.
- **Stable layout** — loading and pressed states must not resize the block.

## Anti-patterns

- Rounding the corners or adding a blurred drop shadow on hover.
- A press with no feedback — the offset block *is* the press.
- Multiple terracotta primaries competing in one view.
- A pill-shaped or ghost-on-ghost button that hides its boundary.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/feedback.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
