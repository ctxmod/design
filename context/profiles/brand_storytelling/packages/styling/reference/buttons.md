# Storytelling — Buttons

Concrete Storytelling styling for the button slot — restrained editorial hierarchy, Inter labels, generous padding, the primary CTA as the story's climax.

Concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" /> for Storytelling.
A button is restrained and editorial. The **primary CTA is the story's climax** —
it appears at the *resolution* act and is the one bright moment of saturated color
on the page (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/brand.md" />). All other buttons stay quiet so it can land.

## Variants

Labels are always **Inter** (`--bs-font-body`), medium weight, sentence case,
action-named ("Start reading", "Send the gift") — never the display face.

```css
.btn {
  font-family: var(--bs-font-body);
  font-weight: 500;
  font-size: var(--bs-text-body);
  padding-block: 0.75rem;
  padding-inline: 1.75rem;        /* generous — editorial breathing room */
  border-radius: var(--bs-radius, 0.5rem);
  transition: background-color var(--bs-dur-page) var(--bs-ease-page),
              color var(--bs-dur-page) var(--bs-ease-page);
}

/* Primary — the climax. One per view, reserved for the resolution. */
.btn--primary {
  background: var(--color-accent);   /* --bs-blue */
  color: #fff;
}

/* Secondary — sits beside primary; outlined, not filled. */
.btn--secondary {
  background: transparent;
  color: var(--color-text);
  box-shadow: inset 0 0 0 1px var(--color-border);
}

/* Ghost / tertiary — low-stakes, repeated actions. */
.btn--ghost {
  background: transparent;
  color: var(--color-muted);
}

/* Danger — destructive intent, layered on any emphasis. */
.btn--danger { background: var(--bs-danger); color: #fff; }

/* Link-style — reads as inline narrative text. */
.btn--link {
  background: none; padding: 0;
  color: var(--color-accent);
  text-underline-offset: 0.2em;
  text-decoration: underline;
}
```

**One primary per context** (the umbrella rule). In a three-act page there is
exactly one true primary — the resolution CTA. Steps within the body use
secondary or ghost so they don't pre-empt the climax.

## Sizing

Sizes scale padding and type together; the interactive target stays **≥ 44px**
even for small buttons (pad the hit area, don't shrink it). A full-width option
exists for stacked mobile and for the centered resolution CTA.

```css
.btn--sm { font-size: var(--bs-text-caption); padding-block: 0.5rem; padding-inline: 1.25rem; }
.btn--lg { font-size: var(--bs-text-lead);    padding-block: 1rem;    padding-inline: 2.5rem; }
.btn--block { display: block; inline-size: 100%; }
```

## States

Transitions are subtle and unhurried (page-turn easing) — never a decorative
flourish that delays the response.

```css
.btn--primary:hover  { background: color-mix(in oklch, var(--color-accent) 88%, black); }
.btn--primary:active { background: color-mix(in oklch, var(--color-accent) 78%, black); }
.btn:focus-visible {
  outline: 3px solid color-mix(in oklch, var(--color-accent) 60%, transparent);
  outline-offset: 2px;            /* visible keyboard ring, never suppressed */
}
.btn:disabled { opacity: 0.45; cursor: not-allowed; }  /* still legible; explain why via helper/tooltip */
```

- **Hover/active** feedback is in the instant band — fast, so the press feels
  registered.
- **Disabled vs loading are distinct**: disabled can't act yet; loading is acting
  now. The loading state swaps the label for an inline spinner at **stable width**
  (no reflow) and prevents double-submit — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/feedback.md" />.
- Never rely on color alone for danger/disabled; pair with position, icon, or
  copy (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/buttons.md" />).

## Anti-patterns

- More than one filled blue primary on a page — it destroys the climax.
- Abril Fatface on a button label.
- A loud hover animation that delays the actual action.
- A button that merely navigates (use a link); a link that performs a
  destructive action (use a danger button).
- A destructive action with no confirmation step (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/feedback.md" />).
</content>

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
