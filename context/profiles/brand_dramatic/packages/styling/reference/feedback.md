# Dramatic — Feedback

Dramatic feedback — dark banners/toasts/alerts with glow accents, severity mapped to violet (info) / green (success) / rose (warning) / red (error), all icon+text not color-alone.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />
for Dramatic. Feedback surfaces are **dark panels lit by a severity glow** — a
violet, green, rose, or red edge that names the meaning against the near-black
ground. Tokens are in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/brand.md" />.

## The family

Toasts, alerts, banners, inline validation, loading/progress, and empty states all
sit on `--bd-surface-raised` with a hairline border and a left/edge glow tinted by
severity. Choose by scope and lifespan: toast for a quick "Saved", alert for a
context problem, banner for a system-wide notice.

```css
.bd-feedback {
  background: var(--bd-surface-raised);
  border: 1px solid var(--bd-border);
  border-inline-start: 3px solid var(--bd-fb-color);
  border-radius: var(--bd-radius, 0.5rem);
  padding: 0.875rem 1rem;
  color: var(--bd-text);
  box-shadow: 0 0 24px color-mix(in oklch, var(--bd-fb-color) 18%, transparent);
}
.bd-feedback__title { font-weight: var(--bd-weight-display); } /* 900 heading */
.bd-feedback__body  { font-weight: var(--bd-weight-body); color: var(--bd-text-muted); }
```

## The severity contract

Severity maps to a fixed color and is **consistent everywhere** — and always
paired with an icon and label, never color alone (it must survive color-blindness
and the dark ground).

| Severity | `--bd-fb-color` | Meaning |
|----------|-----------------|---------|
| **Info** | `--bd-accent` (violet) | Neutral notice — the brand's calm spotlight. |
| **Success** | `--bd-success` (#16a34a) | Action completed — a green tuned to read on near-black. |
| **Warning** | `--bd-accent-2` (rose) | Needs attention but not broken. |
| **Error / danger** | `--bd-danger` (#dc2626) | Failed or invalid — direct, corrective. |

```css
.bd-feedback--info    { --bd-fb-color: var(--bd-accent); }
.bd-feedback--success { --bd-fb-color: var(--bd-success); }
.bd-feedback--warning { --bd-fb-color: var(--bd-accent-2); }
.bd-feedback--error   { --bd-fb-color: var(--bd-danger); }
```

Note on the duochrome: info leans on violet (the primary spotlight) and warning on
rose (the secondary), keeping the brand's two stage-lights doing the everyday work,
while success/error reserve green/red so the *failure* and *done* signals stay
unambiguous. Verify each glow's color clears ≥3:1 as a graphical object against
`--bd-surface-raised` — the glow is decoration; the border + icon carry the signal.

## Dismissibility & persistence

- **Auto-dismiss** (toasts) for low-stakes confirmations; give reading time; never
  auto-dismiss anything the user must act on.
- **Manual dismiss** for messages to acknowledge — clear close affordance.
- **Persistent** for unresolved problems (failed sync) — stays until fixed.
- **Never stack** a wall of glowing toasts; queue or collapse them — overlapping
  glows on the dark ground become noise fast.

## Loading & progress

- **Indeterminate** spinner/bar when duration is unknown — a calm violet sweep on
  the dark, linear easing, continuous.
- **Determinate** violet progress fill when measurable; show real progress.
- **Skeletons** matching the final layout (dark blocks on `--bd-surface-raised`)
  for content loading into a known shape — see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/cards.md" />.
- Loading motion is calm and continuous with a reduced-motion fallback; don't make
  the wait *feel* longer.

## Empty states

A meaningful invitation, not a blank stage: explain *why* it's empty, offer the
primary (violet) next action, match the voice. Distinguish "no results for this
search" from "nothing created yet".

## The voice of failure & waiting

Shared with <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/inputs.md" /> validation:

- **Errors explain and direct** — what went wrong and how to fix it; never "Something
  went wrong" with no recourse.
- **Confirmations are brief** — "Publish" → "Published".
- **Warnings state the consequence** so the user can decide.

## Responsibilities

- Feedback for **every** action — success and failure both.
- Consistent severity carried by **icon + text + glow**, not color alone.
- Dismissibility matches stakes; auto-dismiss only the unimportant.
- Announced to assistive tech (live regions — a medium-tier mechanic; the contract
  is that the message is announced, not merely glowed).
- Don't let a glow obscure the content or the triggering control.

## Anti-patterns

- Silent success or silent failure.
- Severity by glow color only (must add icon + label).
- Auto-dismissing an error before it can be read.
- Fake progress bars; a spinner where a skeleton would feel faster.
- A wall of stacked, overlapping toast glows.
- A blank empty state with no explanation or next step.
