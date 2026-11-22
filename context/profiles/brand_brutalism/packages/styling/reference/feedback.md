# Brutalism — Feedback

Brutalism feedback — thick-bordered banners/alerts/toasts, sharp corners, severity via material palette + mandatory icon, hard-cut appearance, blocky loading and empty states.

Concrete styling for the umbrella's
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" />, in the Brutalism brand. Status
messages are **thick-bordered blocks** with sharp corners that appear by hard cut,
not by fade-in. Severity is carried by the material palette **plus a mandatory
icon/label** — never color alone. Tokens from <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/brand.md" />.

## The block

Toasts, alerts, and banners share one bordered-block shape; they differ by scope
and lifespan, not by softness.

```css
.bb-feedback {
  display: flex;
  gap: 0.75rem;
  align-items: flex-start;
  border: var(--bb-border-w) solid var(--bb-border);
  border-radius: 0;
  background: var(--bb-surface);
  padding: 0.85rem 1rem;
  font-family: var(--bb-font);
  /* Severity shows as a thick leading bar, plus an icon. */
  border-inline-start-width: var(--bb-border-w-bold);
}
.bb-feedback__icon  { font-weight: var(--bb-w-black); }   /* blocky glyph */
.bb-feedback__title { font-weight: var(--bb-w-heavy); text-transform: uppercase;
                      letter-spacing: var(--bb-track-wide); }
```

## The severity contract

Each severity maps to a fixed palette value and is **always** paired with an icon
and a heavy label (umbrella contract — survives color-blindness and low contrast).

| Severity | Border/bar | Icon |
|----------|-----------|------|
| **Info** | `--bb-text` (ink) | ℹ blocky |
| **Success** | `--bb-success` | ✓ blocky |
| **Warning** | `--bb-warning` (ochre family) | ▲ blocky |
| **Error / danger** | `--bb-danger` | ✕ blocky |

```css
.bb-feedback--info    { border-inline-start-color: var(--bb-text); }
.bb-feedback--success { border-inline-start-color: var(--bb-success); }
.bb-feedback--warning { border-inline-start-color: var(--bb-warning); }
.bb-feedback--error   { border-inline-start-color: var(--bb-danger); }
```

Severity is consistent everywhere: error is always danger-red, success never
borrows the ochre warning hue. Brand terracotta is *not* a severity — it stays an
action color, distinct from danger.

## Dismissibility and appearance

- **Hard cut, no fade.** Feedback blocks appear and disappear instantly (or in the
  `--bb-dur-fast` band, mechanical) — honoring the brutalist motion vocabulary and
  doubling as a clean reduced-motion path.
- **Auto-dismiss** toasts for low-stakes confirmations; **manual dismiss** (a
  square bordered close block) for messages to acknowledge; **persistent** banners
  for unresolved problems.
- Never stack a wall of toasts — queue them; the block must not obscure the action
  that produced it.

## Loading and progress

Waiting is feedback, kept **blocky and mechanical**:

- **Indeterminate** — a stepped/segmented bar that advances in hard ticks, not a
  smooth crawl.
- **Determinate** — a bordered track with a flat terracotta fill block showing
  real progress.
- **Skeletons** — concrete-grey solid blocks matching the final layout (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/cards.md" />); no shimmer.

```css
.bb-progress { border: var(--bb-border-w) solid var(--bb-border); border-radius: 0;
               block-size: 1.25rem; }
.bb-progress__fill { background: var(--bb-terracotta); block-size: 100%; }
```

## Empty states

A bordered block, not a blank: a heavy uppercase line explaining *why* it's empty
(first use? filtered to nothing?), and the primary action block to fix it. Voice
is an invitation in the interface's tone, not an apology.

## Inline validation

Field-level feedback is the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_brutalism/reference/inputs.md" /> bold-border-swap pattern; the
voice of failure is shared — errors explain what went wrong and how to fix it,
specific not vague.

## Responsibilities

- Feedback for **every** action — success and failure both.
- **Severity icon + heavy label**, never color alone.
- **Dismissibility matches stakes** — auto-dismiss only the unimportant; never
  auto-dismiss an error.
- Announce status to assistive tech (live regions are a `web` concern; the
  contract is that the message is announced).

## Anti-patterns

- Silent success or silent failure.
- Generic "Something went wrong" with no cause and no fix.
- Severity by color only; soft fade-in/out on banners.
- Shimmer skeletons or a fake-crawl progress bar.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
