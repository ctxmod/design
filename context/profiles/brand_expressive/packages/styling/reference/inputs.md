# Expressive — Inputs

Expressive inputs — IBM Plex Mono fields and labels, thick ink borders, pink/blue dual focus, playful but legible entry, full label/helper/error pattern and state set.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" /> for Expressive.
Fields are mono, chunky, and outlined in ink, with a pink-or-blue focus that pops —
playful but always legible. Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/brand.md" />; native form controls
per <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />.

## Field shape

```css
.be-field {
  font: var(--be-weight-body) var(--be-text-body)/1.4 var(--be-font);
  color: var(--be-ink);
  background: var(--be-surface);
  border: 2px solid var(--be-border);
  border-radius: var(--be-radius, 14px);
  padding: 12px 14px;
  min-height: 44px;
  transition: border-color var(--be-dur-fast) var(--be-ease-out),
              box-shadow var(--be-dur-fast) var(--be-ease-out);
}
.be-field::placeholder { color: var(--be-ink-muted); font-weight: var(--be-weight-quiet); }
```

## Label / helper / error pattern

Labels are always-visible mono, never placeholder-as-label (umbrella rule). Weight
carries the hierarchy: label strong, helper quiet.

```css
.be-label  { display: block; margin-bottom: 6px;
             font: var(--be-weight-strong) var(--be-text-caption)/1 var(--be-font);
             letter-spacing: 0.02em; color: var(--be-ink); }
.be-help   { margin-top: 6px; font-size: var(--be-text-caption);
             font-weight: var(--be-weight-quiet); color: var(--be-ink-muted); }
.be-error  { margin-top: 6px; font-size: var(--be-text-caption);
             font-weight: var(--be-weight-strong); color: var(--be-danger);
             display: flex; gap: 6px; align-items: center; } /* icon + text, not color alone */
.be-label[data-required]::after { content: " *required"; color: var(--be-pink);
                                  font-weight: var(--be-weight-quiet); }
```

Reserve vertical space for the error line so showing it doesn't shove the form
(umbrella stable-layout rule).

## States

Focus is the signature: a thick accent ring. Pink is the default focus accent; blue
focus (`.be-field--accent-blue:focus`) is available so dual-accent forms can alternate
sections.

```css
.be-field:focus {
  outline: none;
  border-color: var(--be-pink);
  box-shadow: 0 0 0 3px var(--be-pink-soft);
}
.be-field--accent-blue:focus { border-color: var(--be-blue); box-shadow: 0 0 0 3px var(--be-blue-soft); }
.be-field[aria-invalid="true"] { border-color: var(--be-danger);
                                 box-shadow: 0 0 0 3px #fde2e2; }
.be-field:disabled  { background: #f3f4f6; color: #9ca3af; border-color: #d1d5db;
                      cursor: not-allowed; } /* visibly inert, still readable */
.be-field[readonly] { background: var(--be-surface-2); border-style: dashed; } /* distinct from disabled */
```

State coverage: **empty** (placeholder quiet-weight), **focus** (accent ring ≥ 3:1),
**filled** (ink body), **error** (red border + icon + fix-it copy), **success**
(optional `--be-success` border where confirmation helps), **disabled**,
**read-only** (dashed border, tint surface), **loading** (async select shows a
spinner in the field).

## Choice controls

Checkboxes, radios, and toggles get chunky ink outlines and accent fills with ≥ 44px
padded targets.

```css
.be-check  { width: 22px; height: 22px; border: 2px solid var(--be-border);
             border-radius: 6px; accent-color: var(--be-pink); }
.be-radio  { border-radius: 9999px; accent-color: var(--be-blue); }
.be-switch[aria-checked="true"] { background: var(--be-pink); }
.be-switch .knob { transition: transform var(--be-dur-fast) var(--be-ease-spring); } /* springy slide */
```

Use a **toggle** only for settings that apply immediately, a **checkbox** for
submit-time choices (umbrella rule). Radio = blue accent, checkbox = pink — leaning
on the dual accent to differentiate single vs multi select.

## Validation feedback

Validate on blur/submit, not every keystroke; re-validate as the user fixes so the
red border clears the moment it resolves. Preserve input on error. Error copy
directs ("Enter a date in the future"), never just "invalid" — shared voice with
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/feedback.md" />.

## Anti-patterns

- Placeholder used as the label, or thin-weight labels that vanish.
- Color-only error with no icon/message.
- Validation that reddens the field mid-typing.
- Hairline field borders — Expressive fields are 2px ink.
- Toggle for a submit-time choice (use checkbox).
