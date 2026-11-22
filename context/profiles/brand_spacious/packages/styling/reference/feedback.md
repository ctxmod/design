# Spacious — Feedback

Spacious feedback styling — calm banners and toasts with generous internal padding, blue-violet info plus severity colors, soft transitions, roomy empty states.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" /> for Spacious.
The slot owns the severity contract, dismissibility, loading/progress, and empty
states; this file supplies the look. The Spacious signature on feedback is **calm
with room** — banners and toasts have generous internal padding, severity colors
are clear but never loud, and everything fades in gently.

## Foundations

Feedback draws from the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/brand.md" />: generous padding from the 8pt
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />, the standard severity colors, and the calm
motion vocabulary (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

```css
.banner, .toast, .alert {
  display: flex;
  gap: var(--space-3);                  /* 16px icon → text */
  align-items: flex-start;
  padding: var(--space-4);             /* 24px — generous internal space */
  border-radius: var(--radius-lg);     /* 12px */
  border: 1px solid var(--color-border);
  box-shadow: var(--shadow-soft);
  font-family: var(--font-body);
  line-height: 1.6;
}
```

## The severity contract

Severity maps to a fixed semantic color, **always paired with an icon** (never
color alone). Spacious tints the surface softly and keeps the text in
`--color-text` for readability.

| Severity | Accent / icon | Soft surface |
|----------|---------------|--------------|
| **Info** | `--color-accent` `#3B82F6` | `#F5F8FF` |
| **Success** | `--color-success` `#16A34A` | `#F0FAF4` |
| **Warning** | `--color-warning` `#D97706` | `#FEF8F0` |
| **Error / danger** | `--color-danger` `#DC2626` | `#FEF4F4` |

```css
.alert--info    { background: #F5F8FF; border-color: var(--color-accent); }
.alert--success { background: #F0FAF4; border-color: var(--color-success); }
.alert--warning { background: #FEF8F0; border-color: var(--color-warning); }
.alert--error   { background: #FEF4F4; border-color: var(--color-danger); }
.alert__icon    { flex: none; inline-size: 20px; block-size: 20px; }
```

Severity also affects prominence: errors get the most visual weight, info the
least — but all stay within the calm Spacious register.

## Dismissibility

- **Toasts** auto-dismiss after enough time to read; they slide and fade in gently,
  never stack into a pile (queue instead).
- **Alerts** offer a clear close affordance with a padded ≥44px hit area.
- **Banners** persist until the underlying condition is resolved.

```css
.toast {
  animation: toast-in var(--dur-base) var(--ease-standard);
}
@keyframes toast-in {
  from { opacity: 0; transform: translateY(8px); }
  to   { opacity: 1; transform: translateY(0); }
}
@media (prefers-reduced-motion: reduce) {
  .toast { animation: none; }
}
```

## Loading and progress

Calm and continuous — a spinner or determinate bar in the accent color, or a
neutral skeleton matching the final layout to avoid reflow. Never a fake crawl;
show real progress. Loading motion is steady, with a reduced-motion fallback.

```css
.progress__bar { background: var(--color-accent); transition: inline-size var(--dur-base) var(--ease-standard); }
```

## Empty states

A Spacious empty state is roomy and inviting, not a blank. Center the content with
generous padding, explain why it is empty, and offer the primary next action.

```css
.empty-state {
  display: flex; flex-direction: column; align-items: center; text-align: center;
  gap: var(--space-3);
  padding: var(--space-7);             /* 64px — lots of room */
  color: var(--color-text-muted);
}
.empty-state__title { font-family: var(--font-display); font-weight: 600;
                      color: var(--color-text); }
```

## Voice

Errors explain and direct (what went wrong, how to fix it); confirmations are brief
and consistent ("Publish" → "Published"); warnings state the consequence. Failure
and emptiness are moments for direction, not mood. See
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" /> for the CSS carriers.

## Anti-patterns (brand-specific)

- Cramped banners/toasts with tight padding — Spacious feedback has internal room.
- Saturated, loud severity fills — tint surfaces softly, keep text readable.
- Severity by color alone — always pair with an icon.
- Jarring or bouncy entrance motion — feedback fades and slides calmly.
- A blank empty state with no explanation or next step.
