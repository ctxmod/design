# Storytelling — Feedback

Concrete Storytelling styling for the feedback slots — calm editorial banners and toasts, severity in the restrained palette, non-jarring transitions that never interrupt the story.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/feedback.md" /> for
Storytelling. Feedback is **calm and editorial** — it informs without breaking
the narrative spell. Severity uses the restrained palette (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />), transitions are gentle (the story shouldn't be
interrupted), and copy directs rather than apologizes.

## The severity contract

Each severity pairs its color with an **icon and label** — never color alone —
and tints a quiet surface rather than shouting in full saturation.

```css
.alert {
  font-family: var(--bs-font-body);
  font-size: var(--bs-text-body);
  display: flex; gap: 0.75rem; align-items: flex-start;
  padding: 1rem 1.25rem;
  border-radius: var(--bs-radius, 0.5rem);
  border-inline-start: 3px solid var(--_sev);   /* a quiet margin rule */
  background: color-mix(in oklch, var(--_sev) 8%, var(--color-surface));
  color: var(--color-text);
}
.alert--info    { --_sev: var(--color-accent); }  /* blue — calm FYI */
.alert--success { --_sev: var(--bs-success); }     /* story resolved */
.alert--warning { --_sev: var(--bs-warning); }     /* plot tension, pending */
.alert--error   { --_sev: var(--bs-danger); }      /* conflict / failure */
.alert__icon { color: var(--_sev); flex: none; }   /* icon carries severity with the color */
```

Severity is **consistent everywhere**: error is always the danger color and
always means failure; success never borrows the warning hue. Errors carry more
visual weight than info, but even an error stays editorial, not alarmist.

## Family and lifespan

| Slot | Storytelling treatment | Lifespan |
|------|------------------------|----------|
| **Toast** | Slim, bottom-anchored, gentle fade-up | Auto-dismiss (read time + buffer) |
| **Alert** | Inline `.alert`, tied to its region | Until resolved/dismissed |
| **Banner** | Full-width, hairline-bounded page notice | Persistent until addressed |
| **Inline validation** | Field-level, <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/inputs.md" /> | Until the field is valid |
| **Loading / progress** | Calm spinner or determinate bar / skeleton | Duration of the operation |
| **Empty state** | Editorial: a line of Abril + an invitation | Until content exists |

```css
.toast { animation: bs-rise var(--bs-dur-page) var(--bs-ease-page); }
@keyframes bs-rise { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: none; } }
@media (prefers-reduced-motion: reduce) { .toast { animation: none; } }  /* instant, no jarring motion */
```

## Dismissibility and persistence

- **Auto-dismiss** only low-stakes confirmations ("Saved"); give enough read
  time and never auto-dismiss anything the user must act on.
- **Manual dismiss** for messages to acknowledge (clear close affordance).
- **Persistent** for unresolved problems — the message stays until the condition
  is fixed; dismissing would hide a real problem.
- **Never stack** a wall of toasts — queue or collapse them; transient feedback
  must not obscure the content or the action that produced it.

## Loading and empty states

- Indeterminate spinner when duration is unknown; **determinate** bar with real
  progress when measurable (never a fake crawl); **skeletons** matching the final
  layout to prevent reflow (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/cards.md" />). Loading motion is calm and
  continuous with a reduced-motion fallback (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).
- An **empty state** is a narrative opportunity, not a blank: a short Abril
  Fatface line, a sentence explaining *why* it's empty, and one primary action to
  begin — an invitation, not an apology.

## The voice of failure

Copy is design material (shared with <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/inputs.md" /> validation): errors
explain what went wrong and how to fix it, specifically; confirmations are brief
and consistent ("Publish" → "Published"); warnings state the consequence
honestly. Treat failure and emptiness as moments for **direction, not mood**.

## Anti-patterns

- Silent success or silent failure.
- Generic "Something went wrong" with no cause and no fix.
- Severity by color only, or full-saturation banners that shatter the calm.
- Auto-dismissing an error or a required action before it can be read.
- Fake progress bars; spinners where a skeleton would feel faster.
- A blank empty state with no explanation or next step.
</content>

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/brand.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
