# Spacious — Inputs

Spacious input styling — generous internal padding, thin neutral borders, blue-violet focus ring, large touch targets, calm validation.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" /> for Spacious. The
slot owns the label/helper/error pattern, the state set, and validation timing;
this file supplies the look. The Spacious signature on a field is **internal
space** — text sits well inside a roomy box bounded by a thin hairline, focus is a
quiet blue ring, and choice controls have large, padded targets.

## Foundations

Inputs draw from the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/brand.md" />: generous padding from the 8pt
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />, thin `--color-border`, and the blue-violet
accent reserved for focus and error-fix affordances.

```css
.field {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);                 /* 8px label → control */
  margin-block-end: var(--space-4);    /* 24px between fields */
}
.input {
  font-family: var(--font-body);
  font-size: 16px;                     /* no iOS zoom */
  color: var(--color-text);
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);        /* 8px */
  padding-block: var(--space-3);       /* 16px — generous internal space */
  padding-inline: var(--space-3);      /* 16px */
  min-block-size: 48px;                /* roomy target */
  transition: border-color var(--dur-fast) var(--ease-standard),
              box-shadow var(--dur-fast) var(--ease-standard);
}
```

## Label / helper / error

Per the slot, the label is always visible and associated; placeholders never stand
in for it. Spacious keeps the trio calm and well-spaced.

```css
.field__label  { font-family: var(--font-body); font-weight: 600; color: var(--color-text); }
.field__helper { font-size: 14px; color: var(--color-text-muted); }
.field__error  { font-size: 14px; color: var(--color-danger); }
```

Helper text is muted and persistent; error text replaces it, pairs danger color
with an icon, and says how to fix the problem. Required/optional is stated in
words, not by a bare asterisk.

## States

| State | Treatment |
|-------|-----------|
| **Empty** | Hairline border, sunken-neutral or white fill; label shows expectation |
| **Focus** | Border turns accent + soft `0 0 0 3px` accent ring |
| **Filled** | Resting border; value legible at 16px |
| **Error** | Border + ring in danger color, plus icon and fix-it message |
| **Success** (optional) | Border in success color with a check, where confirmation helps |
| **Disabled** | `--color-surface-sunken` fill, muted text, `not-allowed`; still readable |
| **Read-only** | No border emphasis, no edit affordance — distinct from disabled |

```css
.input:focus-visible      { outline: none; border-color: var(--color-accent);
                            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.35); }
.input[aria-invalid="true"]{ border-color: var(--color-danger);
                            box-shadow: 0 0 0 3px rgba(220, 38, 38, 0.30); }
.input[disabled]          { background: var(--color-surface-sunken); color: var(--color-text-muted); }

@media (prefers-reduced-motion: reduce) { .input { transition-duration: 1ms; } }
```

## Choice controls

Checkboxes, radios, and toggles get **large touch targets** — pad the hit area well
beyond the glyph (≥44px), in keeping with the spacious bias. Selected/checked uses
the accent.

```css
.checkbox, .radio { inline-size: 20px; block-size: 20px; accent-color: var(--color-accent); }
.choice {                       /* padded clickable row wrapping the control + label */
  display: flex; align-items: center; gap: var(--space-3);
  padding: var(--space-3); min-block-size: 44px; border-radius: var(--radius);
}
.choice:hover { background: var(--color-surface-sunken); }
```

## Validation feel

Validate on blur or submit (umbrella rule), not per keystroke. On error, preserve
the user's input and reserve space for the message so the form does not jump —
animate its appearance gently with `--dur-base`. See
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" /> for the underlying
CSS carriers.

## Anti-patterns (brand-specific)

- Cramped fields with `<16px` internal padding — defeats the spacious feel and the
  target size.
- Heavy or dark borders; Spacious borders are thin hairlines.
- A loud, multi-color focus treatment — focus is one quiet blue ring.
- Tiny checkbox/radio hit areas with no surrounding padded row.
