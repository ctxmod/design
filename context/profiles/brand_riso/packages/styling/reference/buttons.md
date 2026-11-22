# Riso — Buttons

Riso button styling — pink primary with offset print-shadow, blue secondary outline, full state set with the registration-shift press, Space Grotesk uppercase labels.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" /> for Riso. Because **pink
drives interaction**, the primary action is a solid `--ink-pink` button wearing
the signature offset print-shadow. Everything else is flat blue ink on paper.
Labels are Space Grotesk, medium-to-bold, with uppercase tracking on primary for
the poster feel.

## Variants

| Variant | Fill | Text | Border | Shadow |
|---------|------|------|--------|--------|
| **Primary** | `--ink-pink` | `#fff` | none | `--print-shadow-sm` |
| **Secondary** | `--paper` | `--ink-blue` | `2px solid --ink-blue` | none |
| **Ghost / tertiary** | transparent | `--ink-blue` | none | none |
| **Danger** | `--danger` | `#fff` | none | `--print-shadow-sm` |
| **Link-style** | none | `--ink-pink` | none (underline) | none |

- **One primary per view** (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />): pink is
  scarce, so a second pink button reads as a second "most important action" and
  must be demoted to secondary.
- **Danger** keeps the offset shadow (it is a real, weighty action) but swaps the
  fill to `--danger`; pair with an icon, never color alone, and confirm
  destructive actions (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/feedback.md" />).
- Pink is white-on-pink for the label (the ~5:1 needed for the button label is met
  at the white-text end, unlike pink-on-paper text).

```css
.btn { font-family: var(--font-sans); font-weight: 600;
  border-radius: 4px; padding-block: 10px; padding-inline: 18px;
  min-block-size: 44px; cursor: pointer;
  transition: transform var(--dur-instant) var(--ease-out),
              box-shadow var(--dur-instant) var(--ease-out),
              background-color var(--dur-instant) var(--ease-out); }

.btn--primary { background: var(--ink-pink); color: #fff;
  border: none; box-shadow: var(--print-shadow-sm);
  text-transform: uppercase; letter-spacing: 0.04em; }

.btn--secondary { background: var(--paper); color: var(--ink-blue);
  border: 2px solid var(--ink-blue); }

.btn--ghost { background: transparent; color: var(--ink-blue); border: none; }
```

## States

| State | Primary (pink) | Secondary (blue outline) |
|-------|----------------|--------------------------|
| **Default** | pink fill + `--print-shadow-sm` | paper + 2px blue outline |
| **Hover** | shadow grows to `--print-shadow-md` (lifts off the page) | fill `--paper-deep` |
| **Focus** | `--ink-pink` focus ring via `:focus-visible`, ≥3:1 | same pink ring |
| **Active / pressed** | registration shift: `translate(3px,3px)`, shadow → none | `translate(2px,2px)` |
| **Disabled** | desaturated pink, no shadow, `cursor: not-allowed`; reason discoverable | muted blue outline |
| **Loading** | inline spinner, label held, width frozen, double-submit blocked | same |

```css
.btn--primary:hover { box-shadow: var(--print-shadow-md); }
.btn:focus-visible { outline: 3px solid var(--ink-pink); outline-offset: 2px; }
.btn--primary:active { transform: translate(3px, 3px); box-shadow: none; }
.btn:disabled { opacity: 0.45; box-shadow: none; cursor: not-allowed; }
```

The **active state is the signature gesture**: the button presses *into* its
offset shadow — `translate(3px,3px)` consumes exactly the `--print-shadow-sm`
offset, so the ink and paper momentarily register. Instant band (`--dur-instant`)
so the press never feels laggy. Hover does the inverse on primary — the shadow
*grows*, lifting the sticker off the page. Under reduced-motion the transform is
dropped and the shadow toggles instantly.

## Responsibilities & anti-patterns

- **Action-named labels** in the interface voice ("Save changes", "Publish"), never
  "Submit" / "Go" / "Click here".
- **Stable layout** through loading and label changes — freeze the width.
- **Keyboard operable** with a visible pink focus ring; never suppress it.
- Don't use a second pink button as a faux-primary; don't replace the offset
  shadow with a blurred drop shadow; don't shrink the hit area below 44px; don't
  rely on pink-vs-blue alone to mark danger (add an icon).

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/brand.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/inputs.md" />
