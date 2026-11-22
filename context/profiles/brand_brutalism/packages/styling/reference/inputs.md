# Brutalism — Inputs

Brutalism inputs — thick ink borders, sharp corners, heavy uppercase labels, focus via border thickness/color swap (no soft ring), error as bold border + danger ink.

Concrete styling for the umbrella's
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />, in the Brutalism brand. Every field is a
**thick-bordered box** with sharp corners — a visible container the user types
into, not a soft underlined ghost. Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/brand.md" />.

## The field box

```css
.bb-field {
  display: block;
  inline-size: 100%;
  background: var(--bb-surface);
  border: var(--bb-border-w) solid var(--bb-border);
  border-radius: 0;
  color: var(--bb-text);
  font-family: var(--bb-font);
  font-weight: var(--bb-w-body);
  font-size: var(--bb-text-base);
  padding-block: 0.6rem;
  padding-inline: 0.85rem;
  min-block-size: 44px;
  caret-color: var(--bb-terracotta);   /* big, material cursor */
}
```

The text input, textarea, and select share this box. Checkboxes and radios become
small thick-bordered squares (radios stay square too — Brutalism does not round).

## The label / helper / error pattern

Labels are **always visible, heavy, and uppercase** — placeholder text is never a
label (umbrella contract). Helper text is light; error text is danger-ink and
paired with a mark.

```css
.bb-label  { font-weight: var(--bb-w-heavy); text-transform: uppercase;
             letter-spacing: var(--bb-track-wide); font-size: var(--bb-text-sm); }
.bb-helper { font-weight: var(--bb-w-light); color: #4b5563; }
.bb-error  { font-weight: var(--bb-w-heavy); color: var(--bb-danger); }
```

Required/optional is stated in words next to the heavy label, not by a bare
asterisk. The label is programmatically associated with the control.

## States

Focus and error are **border events** — a thickness or color swap, never a soft
glow ring. This is the brutalist signature for inputs.

| State | Brutalist expression |
|-------|----------------------|
| **Empty** | Bordered box, heavy label above. |
| **Focus** | Border swaps to `--bb-terracotta` *and* jumps to `--bb-border-w-bold` (4px). No outline ring. |
| **Filled** | Plain box; value in body weight. |
| **Error** | Border swaps to `--bb-danger` at bold weight, danger-ink message + icon below. |
| **Success** (optional) | Border swaps to `--bb-success` bold; used only where confirmation helps. |
| **Disabled** | `--bb-concrete` fill, border stays visible, readable, not editable. |
| **Read-only** | White fill, border thinned to `--bb-border-w-thin`, no caret — visibly distinct from disabled. |
| **Loading** (async) | Mechanical stepped mark inline at the field end. |

```css
.bb-field:focus-visible { outline: none; border-color: var(--bb-terracotta);
                          border-width: var(--bb-border-w-bold); }
.bb-field[aria-invalid="true"] { border-color: var(--bb-danger);
                                 border-width: var(--bb-border-w-bold); }
.bb-field:disabled { background: var(--bb-concrete); cursor: not-allowed; }
.bb-field[readonly] { border-width: var(--bb-border-w-thin); }
```

## Validation feedback

- Validate on **blur or submit**, not every keystroke; re-validate as the user
  fixes so the bold danger border clears the instant the value is valid.
- Errors render **at the field** — bold danger border plus a heavy danger-ink
  message that says how to fix it (shared voice with
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/feedback.md" />).
- **Never color alone** — the border-weight jump and the leading mark carry the
  error for color-blind users.
- **Preserve input** on error; the box keeps its value.

## Responsibilities

- Visible, associated **heavy label** and accessible name.
- Visible focus via the border swap; full keyboard operability.
- **≥ 44px** targets for the square checkbox/radio glyphs — pad beyond the box.
- Stable layout: reserve space for the error line so it does not shove the form.

## Anti-patterns

- Underline-only fields with no box — Brutalism wants the visible container.
- A soft focus ring or rounded corners.
- Placeholder used as the label; color-only error state.
- Rounded checkboxes/radios — keep them square.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
