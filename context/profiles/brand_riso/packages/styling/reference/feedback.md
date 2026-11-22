# Riso — Feedback

Riso feedback styling — severity mapped onto reserved status hues (success/warning/danger) plus info-as-blue, banners/alerts with blue outline and offset shadow, icon-plus-text severity, loading and empty states in the two-color logic.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" /> for Riso. Feedback is
the **one place Riso sanctions colors beyond blue and pink**: the reserved status
hues (`--success`, `--warning`, `--danger`) carry severity. Everything else stays
true to the two-color logic — paper surface, blue outline, the offset
print-shadow, pink only where the user can act (e.g. an "Undo" in a toast).

## The severity contract

Severity maps to a fixed meaning, color, and icon — **never color alone** (it must
survive color-blindness and low contrast, see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />):

| Severity | Color token | Icon | Tone |
|----------|-------------|------|------|
| **Info** | `--ink-blue` | ℹ circle | Calm — info stays in the brand ink, no extra hue |
| **Success** | `--success` `#16A34A` | ✓ check | Affirming, brief |
| **Warning** | `--warning` `#D97706` | △ triangle | Cautioning |
| **Error / danger** | `--danger` `#DC2626` | ✕ / ! | Direct, corrective |

- **Info uses blue** — it is a neutral notice, so it borrows the structural ink
  rather than introducing a fourth color. Success / warning / danger are the only
  non-blue/pink hues in the system, and only here.
- Severity is consistent everywhere: danger always means failure; success never
  borrows warning. Severity drives prominence (errors interrupt more than info).

## Banners and alerts

Page/region messages are paper panels outlined in the severity color, lifted by the
offset shadow — a printed notice pinned to the sheet:

```css
.banner { background: var(--paper);
  border: 2px solid var(--ink-blue);          /* severity color overrides below */
  border-radius: 4px; box-shadow: var(--print-shadow-sm);
  padding-block: 12px; padding-inline: 16px;
  display: flex; gap: 12px; align-items: start;
  font-family: var(--font-sans); color: var(--text); }

.banner--success { border-color: var(--success); }
.banner--warning { border-color: var(--warning); }
.banner--error   { border-color: var(--danger); }
.banner__icon    { color: inherit; flex: none; }   /* matches the border severity */
```

The shadow stays **blue and blurless** even on a colored banner — the misregister
is a property of the paper, not the severity. A banner's optional dismiss/action
uses the pink interaction color.

## The feedback family

| Slot | Riso treatment | Lifespan |
|------|----------------|----------|
| **Toast / snackbar** | small paper chip, severity outline, `--print-shadow-sm`; optional pink "Undo" | auto-dismiss (seconds) |
| **Alert** | inline severity banner tied to a region | until resolved/dismissed |
| **Banner** | page/app-level severity banner | persistent until addressed |
| **Inline validation** | field-level (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/inputs.md" />) — danger outline + icon | until field valid |
| **Loading / progress** | blue spinner / blue determinate bar on paper | duration of op |
| **Empty state** | paper card, blue illustration, pink primary "create" action | until content exists |

## Loading, progress, empty states

- **Indeterminate** — blue spinner (linear-eased, continuous) when duration is
  unknown; **determinate** — a blue fill bar showing *real* progress, never a fake
  crawl; **skeletons** — paper blocks matching the final layout to prevent reflow
  (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/cards.md" />).
- **Empty state** — explains *why* it's empty and offers the next step as a single
  **pink** primary action; an invitation, not an apology. Distinguish "no results"
  (suggest broadening) from "nothing created yet" (offer to create).
- Respect <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/brand.md" />: loading motion is calm and continuous, with a
  reduced-motion fallback.

## Voice & responsibilities

- **Errors explain and direct** — what went wrong and how to fix it, specifically;
  no blame, no vague "Something went wrong."
- **Confirmations are brief and consistent** — "Publish" → "Published".
- Feedback for **every** action (success and failure); **icon + text** severity,
  never color alone; **dismissibility matches stakes** (auto-dismiss only the
  unimportant; persist unresolved problems); announce to assistive tech; don't
  obscure the content or the triggering control.

**Anti-patterns:** silent success/failure; severity by color alone; introducing a
non-status decorative color; auto-dismissing an error before it can be read;
blurred shadows on banners; fake progress bars; a blank empty state with no next
step; toasts stacking into a pile.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_riso/reference/buttons.md" />
