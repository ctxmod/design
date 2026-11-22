# Forest — Inputs

Forest concrete input styling — deep-surface fields with hairline border, lime focus ring, body-colored labels, warm-red error that contrasts on green; states, padding, radius tokens.

Concrete Forest styling for the **inputs** slot. Fills the umbrella
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" /> — the label/helper/error pattern, the
full state set, validation feedback — with Forest values. Tokens from
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />.

Forest inputs sit as **sunken wells** on the green ground: a slightly darker
deep-surface fill, a hairline border, generous rounding (`--forest-radius-sm`,
6px), and flat (no shadow). The label is always visible (placeholder is never the
label).

## Field anatomy & colors

| Part | Color | Notes |
|------|-------|-------|
| Field fill | `--forest-surface-deep` (`#1F3400`) | Sunken vs the page surface |
| Border (rest) | `--forest-border` (`#4C7A05`) | 1px hairline |
| Typed value | `--forest-heading` (`#F4FAE8`) | High contrast for legibility |
| Placeholder | `--forest-body` @ 60% | Hint only — not a label |
| Label | `--forest-body` (`#C9D6B0`) | Always present, above the field |
| Helper text | `--forest-body` @ 80% | Calm, persistent, format hints |
| Error text | `--forest-danger` (`#FF5C49`) | Warm red — cuts through green |
| Required mark | `--forest-brand-medium` | Plus an explicit "required" convention |

Error red is a **warm hue** deliberately distinct from the green ground and the
lime accent, so failure never reads as success (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/brand.md" />).

## States

| State | Treatment |
|-------|-----------|
| **Empty** | deep-surface fill, hairline border, label + optional placeholder |
| **Focus** | border → `--forest-brand`; 2px ring `--forest-brand-medium`, 1px offset |
| **Filled** | value in `--forest-heading`, border at rest color |
| **Error** | border → `--forest-danger`; error icon + message below; **color is never the only signal** |
| **Success** (optional) | border → `--forest-brand` + check icon, where confirmation helps (e.g. unique username) |
| **Disabled** | fill `color-mix(in oklch, var(--forest-surface-deep) 70%, var(--forest-surface))`, text 55%, `cursor: not-allowed` — still readable |
| **Read-only** | no border or muted border, plain text — visibly distinct from disabled |
| **Loading** (async) | inline spinner in the field (validating / fetching options) |

Distinguish **disabled** (temporarily not editable) from **read-only** (value
matters, won't change).

## Family specifics

- **Checkbox / radio** — 18px box, `--forest-radius-sm` (radio is pill); checked
  fill `--forest-brand` with a `--forest-on-brand` glyph. Pad the hit area to
  ≥ 44px beyond the small glyph.
- **Toggle / switch** — `--forest-radius-pill` track; off = `--forest-surface-deep`
  with border, on = `--forest-brand` track with a light knob. Use only for
  immediate-effect settings, not submit-gated values.
- **Select** — same field shell; lime chevron; menu on `--forest-surface-raised`,
  active option highlighted with a lime-tinted background.
- **Slider** — track `--forest-surface-deep`, filled portion `--forest-brand`,
  thumb `--forest-brand-medium` with focus ring.

## Validation feedback

- **Validate on blur or submit**, not every keystroke; re-validate as the user
  fixes so the error clears the moment it resolves.
- **Errors at the field**, inline and adjacent, with icon + specific message
  ("Enter a date in the future", not "Invalid"); preserve the user's input.
- Reserve space for the error line (or animate gently, ~150ms) so showing it
  doesn't shove the form (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).
- Error voice is shared with <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_forest/reference/feedback.md" />: explain and direct, don't
  apologize.

## CSS tokens

```css
.forest-input {
  --forest-input-bg: var(--forest-surface-deep);
  --forest-input-border: var(--forest-border);
  --forest-input-fg: var(--forest-heading);
  --forest-input-radius: var(--forest-radius-sm);   /* 6px */
  --forest-input-ring: var(--forest-brand-medium);

  background: var(--forest-input-bg);
  color: var(--forest-input-fg);
  border: 1px solid var(--forest-input-border);
  border-radius: var(--forest-input-radius);
  padding-block: 9px;
  padding-inline: 12px;
  transition: border-color var(--forest-dur-fast) var(--forest-ease);
}
.forest-input::placeholder { color: color-mix(in oklch, var(--forest-body) 60%, transparent); }
.forest-input:focus-visible {
  border-color: var(--forest-brand);
  outline: 2px solid var(--forest-input-ring);
  outline-offset: 1px;
}
.forest-input[aria-invalid="true"] { border-color: var(--forest-danger); }
.forest-input__error { color: var(--forest-danger); }
```

## Anti-patterns (Forest-specific)

- Placeholder used as the label (vanishes, fails contrast on the deep green).
- A green-on-green error state — error must use the warm `--forest-danger`, with
  icon + text, never color alone.
- A flat field with no border *and* no fill contrast — it disappears into the
  ground; keep the deep-surface step or the hairline.
- Validating on every keystroke and reddening the field mid-typing.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />
