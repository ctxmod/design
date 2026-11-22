# Riso — Inputs

Riso input styling — blue outlines on paper, blue labels, pink focus ring (with optional offset shadow), full state set and validation feedback in the two-color logic.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" /> for Riso. Inputs are blue
ink drawn on paper: a **2px `--ink-blue` outline**, a blue label above, and a
**pink focus** that announces "this field is active." Blue structures the field;
pink marks the interaction. Space Grotesk throughout (labels 500, values 400).

## The label / helper / error pattern

- **Label** — always visible, `--ink-blue`, 14px / weight 500, sits above the
  control and is programmatically associated. Placeholder is never the label.
- **Helper text** — `--text` at reduced size, calm and persistent below the field.
- **Error text** — `--danger` with a leading icon, replacing helper text; says
  what's wrong *and* how to fix it (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/feedback.md" />).
- **Required/optional** — stated explicitly in the label ("Email (required)"), not
  an unexplained asterisk.

```css
.field-label { font-family: var(--font-sans); font-weight: 500;
  color: var(--ink-blue); font-size: 14px; margin-block-end: 6px; display: block; }

.input { font-family: var(--font-sans); color: var(--text);
  background: var(--paper); border: 2px solid var(--ink-blue);
  border-radius: 4px; padding-block: 10px; padding-inline: 12px;
  min-block-size: 44px;
  transition: box-shadow var(--dur-fast) var(--ease-out),
              border-color var(--dur-fast) var(--ease-out); }
```

## States

| State | Treatment |
|-------|-----------|
| **Empty** | paper fill, 2px blue outline, blue label; placeholder muted |
| **Focus** | pink ring (`:focus-visible`) + outline shifts to `--ink-pink`; optional `--print-shadow-sm` lift |
| **Filled** | value in `--text`, blue outline retained |
| **Error** | outline `--danger` + danger icon + fix-it message; not color alone |
| **Success** (optional) | outline `--success` + check icon where confirmation helps |
| **Disabled** | `--paper-deep` fill, muted blue outline, readable but inert |
| **Read-only** | no outline or hairline blue, paper fill — visibly not editable, distinct from disabled |
| **Loading** | inline spinner (async validation / option fetch) |

```css
.input:focus-visible { outline: none;
  border-color: var(--ink-pink);
  box-shadow: 0 0 0 3px color-mix(in oklch, var(--ink-pink) 35%, transparent),
              var(--print-shadow-sm); }
.input[aria-invalid="true"] { border-color: var(--danger); }
.input:disabled { background: var(--paper-deep); opacity: 0.7; }
```

The **focus is pink**: the outline recolors to `--ink-pink`, a soft pink ring is
laid via `color-mix` (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />),
and an optional blurless `--print-shadow-sm` lifts the field as if pressed into
focus. Checkbox, radio, and toggle follow the same logic — blue box on paper,
**pink fill when checked/on**, ≥44px padded targets.

## Validation feedback & responsibilities

- **Validate on blur or submit**, not every keystroke; re-validate as the user
  fixes so the error clears the moment it resolves.
- **Errors at the field**, inline and adjacent; preserve the user's input on
  failure — never clear the form.
- **Never color alone** — danger outline always pairs with an icon and message.
- **Stable layout** — reserve space for the error line so showing it doesn't shove
  the form (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />).
- Visible, associated label; visible pink focus; full keyboard operability; padded
  targets for checkboxes/radios/toggles.

**Anti-patterns:** placeholder-as-label; keystroke-validation that reddens a field
mid-typing; "invalid" with no fix; pink used for a resting (non-interactive) input
border; blurred focus glow instead of the hard ring.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/brand.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/buttons.md" />
