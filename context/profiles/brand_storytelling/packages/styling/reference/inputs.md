# Storytelling — Inputs

Concrete Storytelling styling for the input slots — calm, readable Inter fields, generous spacing, minimal borders, subtle focus, the label/helper/error contract.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" /> for Storytelling.
Inputs are **calm and readable** — a form is part of the narrative, not an
interrogation. Inter throughout, generous spacing, minimal chrome, and a focus
state that draws attention gently rather than alarming.

## Field styling

```css
.field {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;                    /* label → control → helper, tight reading flow */
  margin-block-end: var(--bs-space-beat, 2rem); /* generous between fields */
}

.field__label {
  font-family: var(--bs-font-body);
  font-weight: 500;
  font-size: var(--bs-text-caption);
  color: var(--color-text);
}

.input {
  font-family: var(--bs-font-body);
  font-size: var(--bs-text-body);
  color: var(--color-text);
  background: var(--color-surface);
  padding-block: 0.75rem;
  padding-inline: 1rem;           /* generous, comfortable to read */
  border: none;
  border-block-end: 1.5px solid var(--color-border); /* a single editorial underline */
  border-radius: 0;
  transition: border-color var(--bs-dur-page) var(--bs-ease-page);
}
```

A minimal **bottom-rule** treatment reads as a writing line on a page — restrained
chrome consistent with the brand. (Use a boxed variant only for dense forms.)

## The label / helper / error contract

Every field carries a **visible, associated label** (placeholder is never the
label). Helper text is calm and persistent; error text replaces it and says what
to fix, in Inter, specific not vague (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />).

```css
.field__helper { font-size: var(--bs-text-caption); color: var(--color-muted); }
.field__error  { font-size: var(--bs-text-caption); color: var(--bs-danger); display: flex; gap: 0.4rem; }
.field__error::before { content: "⚠"; } /* icon + text — never color alone */
```

Required/optional state is communicated explicitly in words, not by a lone
asterisk.

## States

```css
.input:focus-visible {
  border-block-end-color: var(--color-accent);   /* subtle: the line warms, no harsh ring */
  outline: 3px solid color-mix(in oklch, var(--color-accent) 25%, transparent);
  outline-offset: 2px;
}
.input[aria-invalid="true"] { border-block-end-color: var(--bs-danger); }
.input:disabled { color: var(--color-muted); cursor: not-allowed; }      /* inert but readable */
.input[readonly] { border-block-end-style: dotted; }                     /* distinct from disabled */
```

- **Empty / focus / filled / error / disabled / read-only** are all designed;
  disabled (can't edit now) is visually distinct from read-only (won't edit).
- Checkboxes, radios, and toggles get padded hit areas (**≥ 44px**) beyond the
  small glyph; the toggle reflects an immediate setting, the checkbox a
  submit-time choice.

## Validation feedback

- **Validate on blur or submit**, not every keystroke; re-validate as the user
  fixes so the error clears the moment it resolves.
- Show the error **at the field**, inline; preserve the user's input on error.
- Reserve space for the error line so showing it doesn't shove the form around
  (stable layout) — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/feedback.md" /> for the shared voice of failure.

## Anti-patterns

- Placeholder used as the label.
- A jarring red border that fires before the user finishes typing.
- "Invalid input" with no fix instruction.
- Tiny checkbox/radio targets; color-only error indication.
- Cramped field spacing that breaks the calm reading rhythm.
</content>

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/brand.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
