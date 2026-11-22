# Dramatic — Inputs

Dramatic inputs — sunken near-black fields with light text, violet focus glow, minimal borders, 400 labels and 900 field-group headers, rose error state.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />
for Dramatic. A field is a **sunken pool of dark** (`--bd-surface-sunken`) on the
stage; the value is light text, and focus lights it with a violet glow. Tokens are
defined in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/brand.md" />.

## The field family

Text, textarea, select, checkbox, radio, toggle, and slider all share the dark
sunken treatment and the violet focus glow. Checkboxes/radios use the violet fill
when checked; the toggle slides to a violet track; the slider's fill and thumb are
violet.

## Label / helper / error pattern

- **Label** — always present and visible, **400 weight** `--bd-text`. Placeholder
  is never a label (it vanishes and fails contrast). Programmatically associated
  with the control.
- **Field-group header** — the one place 900 appears in a form: a section heading
  ("Billing", "Account") set in 900 to anchor a group of 400-labelled fields.
- **Helper text** — `--bd-text-muted` 400, calm and persistent.
- **Error text** — `--bd-accent-2` (rose) 400 with an icon; says what's wrong and
  how to fix it. Replaces/accompanies helper text.
- **Required/optional** — communicated explicitly, not by a bare asterisk.

```css
.bd-field-label  { font-weight: var(--bd-weight-body); color: var(--bd-text); }
.bd-field-group  { font-weight: var(--bd-weight-display); /* 900 section header */
                   letter-spacing: var(--bd-track-display); }

.bd-input {
  font-family: var(--bd-font);
  font-weight: var(--bd-weight-body);
  font-size: var(--bd-text-body);
  color: var(--bd-text);
  background: var(--bd-surface-sunken);
  border: 1px solid var(--bd-border);
  border-radius: var(--bd-radius, 0.5rem);
  padding-block: 0.625rem;
  padding-inline: 0.875rem;
  min-block-size: 2.75rem;
  caret-color: var(--bd-accent);
  transition: border-color var(--bd-dur-fast) var(--bd-ease-out),
              box-shadow var(--bd-dur-fast) var(--bd-ease-out);
}
.bd-input::placeholder { color: var(--bd-text-subtle); } /* hint only, not a label */
```

## States

| State | Treatment |
|-------|-----------|
| **Empty** | Sunken dark field; subtle placeholder hint; hairline border. |
| **Focus** | Violet focus glow + brightened border — the spotlight on the active field. |
| **Filled** | Light value, legible against the sunken dark. |
| **Error** | Rose border + rose icon + rose helper message — color plus icon plus text. |
| **Success** (optional) | Subtle violet/green check where confirmation helps. |
| **Disabled** | Border and text drop to subtle; visibly inert, still readable. |
| **Read-only** | No border emphasis, `--bd-text-muted` value; distinct from disabled. |
| **Loading** (async) | Inline spinner for validating/fetching options. |

```css
.bd-input:focus-visible {
  outline: none;
  border-color: var(--bd-accent);
  box-shadow: 0 0 0 3px var(--bd-border-glow),
              0 0 18px color-mix(in oklch, var(--bd-accent) 35%, transparent);
}
.bd-input[aria-invalid="true"] {
  border-color: var(--bd-accent-2);
  box-shadow: 0 0 0 3px color-mix(in oklch, var(--bd-accent-2) 35%, transparent);
}
.bd-input:disabled { color: var(--bd-text-subtle); border-color: var(--bd-border); }
@media (prefers-reduced-motion: reduce) { .bd-input { transition: none; } }
```

## Validation feedback

- Validate on **blur or submit**, not every keystroke; re-validate as the user
  fixes so the rose state clears the moment it's resolved.
- Show errors **at the field**, inline and adjacent — rose color *plus* icon *plus*
  message, never color alone (the rose error must clear ≥3:1 against the sunken
  field; the icon guarantees it survives color-blindness).
- **Preserve input** on error; never clear the form.
- Error copy directs ("Enter a date in the future"), doesn't apologize (shared
  voice with <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/feedback.md" />).

## Responsibilities

- Visible, associated **400 label** and accessible name.
- Visible **violet focus glow** and full keyboard operability (radio groups
  arrow-navigate; selects open by keyboard).
- **≥44px targets** for checkboxes/radios/toggles — pad beyond the glyph.
- **Stable layout** — showing a rose error message reserves space, doesn't shove
  the form (gentle, reduced-motion-safe).

## Anti-patterns

- Placeholder used as the label.
- A 900-weight field *label* (900 is reserved for group headers, not every label).
- Validation that turns the field rose on every keystroke.
- Color-only error indication (must pair rose with icon + text).
- A focus glow so faint it's lost on the dark — keep the border brighten too.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_accessibility.md" />
