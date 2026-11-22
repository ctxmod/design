# Expressive — Feedback

Expressive feedback — bright color-blocked banners and toasts across info/success/warning/danger severity, mono copy with icon+label, hard-bordered surfaces, spring entrances, with dismissibility and reduced-motion rules.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" /> for Expressive.
Feedback is bright and unmissable: color-blocked surfaces with thick ink borders,
mono copy, an icon+label per severity, and a springy entrance. Tokens from
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/brand.md" />. Severity color is reserved — green/amber/red never decorate,
and the two brand accents only appear in the **info** severity (blue).

## Severity tokens

Each severity pairs a color with an **icon and label**, never color alone (umbrella
rule), so it survives color-blindness and low contrast.

```css
.be-alert {
  display: flex; gap: 10px; align-items: flex-start;
  padding: 12px 14px;
  border: 2px solid var(--be-border);
  border-radius: var(--be-radius, 14px);
  box-shadow: 4px 4px 0 var(--be-ink);
  font: var(--be-weight-body) var(--be-text-body)/1.5 var(--be-font);
}
.be-alert__title { font-weight: var(--be-weight-strong); }

.be-alert--info    { background: var(--be-blue-soft); }   /* blue accent — calm FYI */
.be-alert--success { background: #dcfce7; }               /* --be-success family */
.be-alert--warning { background: #fef3c7; }               /* --be-warning family */
.be-alert--danger  { background: #fee2e2; }               /* --be-danger family */
.be-alert--info    .be-alert__icon { color: var(--be-blue); }
.be-alert--success .be-alert__icon { color: var(--be-success); }
.be-alert--warning .be-alert__icon { color: var(--be-warning); }
.be-alert--danger  .be-alert__icon { color: var(--be-danger); }
```

Severity is consistent everywhere: error is always the danger family and always means
failure; success never borrows warning. Prominence scales with severity — danger gets
a stronger color block and may add a left accent bar; info stays quiet.

## The feedback family

- **Toast / snackbar** — transient "Saved" confirmation, bottom-corner, auto-dismiss
  ~4s, spring entrance. Queue, never stack into a pile.
- **Alert** — context-bound message tied to a region; persists until resolved.
- **Banner** — app-level notice across the top, full-width color block, persistent
  until addressed.
- **Inline validation** — field-level, owned by <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/inputs.md" />.
- **Loading / progress** — see below.
- **Empty state** — a card-shaped invitation with a primary action, not a blank box
  (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_expressive/reference/cards.md" />).

## Spring entrances

The signature: feedback pops in with overshoot from its spatial origin.

```css
@keyframes be-pop-in {
  0%   { transform: translateY(12px) scale(0.96); opacity: 0; }
  100% { transform: translateY(0)    scale(1);    opacity: 1; }
}
.be-toast { animation: be-pop-in var(--be-dur-pop) var(--be-ease-spring); }

@media (prefers-reduced-motion: reduce) {
  .be-toast { animation: be-fade 120ms linear; }     /* calm fallback, no spring */
}
@keyframes be-fade { from { opacity: 0; } to { opacity: 1; } }
```

Reduced-motion is mandatory — collapse the spring/scale to a plain opacity fade (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/web_motion.md" />).

## Dismissibility and persistence

- **Auto-dismiss** only low-stakes confirmations (toasts); give time to read.
- **Manual dismiss** for messages the user should acknowledge — provide a clear close
  affordance.
- **Persistent** for unresolved problems (failed sync, required action); never
  auto-dismiss an error or a required action.

## Loading and progress

```css
.be-progress      { height: 10px; border: 2px solid var(--be-border);
                    border-radius: 9999px; overflow: hidden; background: var(--be-surface-2); }
.be-progress__bar { height: 100%; background: var(--be-pink);
                    transition: width var(--be-dur-fast) var(--be-ease-out); }
.be-spinner       { animation: be-spin 800ms linear infinite; color: var(--be-blue); }
```

Determinate bars show real progress (never a fake crawl); indeterminate spinner when
duration is unknown; skeletons (card-shaped) for content loading into a known layout;
keep loading motion calm and continuous despite the brand's playfulness.

## Voice

Mono copy, brief and direct. Errors explain and direct ("Couldn't save — check your
connection and retry"), don't apologize or blame, never vague. Confirmations are
consistent ("Publish" → "Published"). Empty states invite, not apologize.

## Anti-patterns

- Severity by color only — always icon + label.
- Auto-dismissing an error or required action before it can be read.
- Toasts stacking into an unreadable pile.
- Fake progress bars; spinners where a skeleton feels faster.
- A blank empty state with no explanation or next step.
- Using pink/blue brand accents to signal danger/success — status colors are reserved.
