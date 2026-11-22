# Dramatic — Cards

Dramatic cards — raised near-black surface steps with subtle accent-edge glow, the spotlight feel, 900 titles / 400 body, and interactive hover-glow states.

Concretizes the <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/cards.md" />
for Dramatic. A card is a **raised slab lifted off the stage** — one step lighter
than the base (`--bd-surface-raised`), edged with a hairline or a subtle accent
glow so it reads as spotlit. Tokens are in <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/brand.md" />.

## Surface & elevation

Because shadows barely read on near-black, a card's elevation comes from being
*lighter* than the ground plus a faint border — optionally an accent-tinted edge
glow for a hero/featured card. Don't reuse light-mode drop shadows.

```css
.bd-card {
  background: var(--bd-surface-raised);
  border: 1px solid var(--bd-border);
  border-radius: var(--bd-radius, 0.5rem);
  padding: 1.5rem; /* comfortable density */
  color: var(--bd-text);
  transition: border-color var(--bd-dur-fast) var(--bd-ease-out),
              box-shadow var(--bd-dur-fast) var(--bd-ease-out),
              transform var(--bd-dur-fast) var(--bd-ease-out);
}
.bd-card--featured {
  border-color: var(--bd-border-glow);
  box-shadow: 0 0 40px color-mix(in oklch, var(--bd-accent) 18%, transparent);
}
```

## Header / body / footer contract

- **Header** — identity: a **900** title, optional 400 eyebrow/category, optional
  media or overflow action. The 900 title is the card's shout.
- **Body** — primary content in **400** `--bd-text` / `--bd-text-muted`; the reason
  the card exists.
- **Footer** — actions (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/buttons.md" />) and metadata. At most one primary
  (violet) action per card.

Across a collection, the regions stay in the same slots so the grid scans as a
rhythm. 900 titles and 400 bodies establish the in-card hierarchy without a middle
weight.

```css
.bd-card__title { font-weight: var(--bd-weight-display); font-size: var(--bd-text-h2);
                  letter-spacing: var(--bd-track-display); }
.bd-card__body  { font-weight: var(--bd-weight-body); color: var(--bd-text-muted);
                  line-height: var(--bd-leading-body); }
```

## Interactive vs. static

- **Static card** — a presentation container; only its inner buttons/links are
  interactive.
- **Interactive card** — the whole card is a target. It gets hover, focus, active,
  and (if selectable) selected states, a visible focus ring, and keyboard
  operability. Resolve the nested-action conflict deliberately: one primary card
  target plus clearly separated inner controls.

## States

| State | Treatment |
|-------|-----------|
| **Default** | Raised surface, hairline border. |
| **Hover** (interactive) | Edge glow blooms + a 2px lift (`transform: translateY(-2px)`); the spotlight finds it. |
| **Focus** (interactive) | Visible violet ring (`box-shadow: 0 0 0 3px var(--bd-border-glow)`). |
| **Active / pressed** | Lift settles, glow tightens. |
| **Selected** | Persistent violet border + steady glow. |
| **Loading / skeleton** | Skeleton matching the card's shape (dark blocks on `--bd-surface-raised`) to prevent reflow. |
| **Empty** | Meaningful empty state, not a blank slab (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_dramatic/reference/feedback.md" />). |
| **Disabled** | Muted surface; not selectable. |

```css
.bd-card--interactive:hover {
  border-color: var(--bd-border-glow);
  box-shadow: 0 0 28px color-mix(in oklch, var(--bd-accent) 28%, transparent);
  transform: translateY(-2px);
}
.bd-card--interactive:focus-visible {
  outline: none;
  box-shadow: 0 0 0 3px var(--bd-border-glow);
}
@media (prefers-reduced-motion: reduce) {
  .bd-card { transition: none; }
  .bd-card--interactive:hover { transform: none; } /* glow only, no lift */
}
```

## Density

**Comfortable** (1.5rem padding) for spacious/marketing layouts; **compact**
(1rem) for dense grids. Density is a systematic token swap; one collection shares a
density.

## Responsibilities

- Group genuinely related content; assert "these belong together" truthfully.
- Consistent region usage across a collection; one primary action at most.
- Resolve interactive/static; if interactive, provide the full control state set,
  the violet focus ring, and keyboard support.
- Borders/glows earn their keep — drop them where the dark + spacing already group.

## Anti-patterns

- Every region wrapped in a glowing card until the page is a wall of boxes.
- A clickable card that swallows its inner buttons.
- Inconsistent title/media/action placement across a grid.
- Two competing primary actions in one card.
- A loading state that pops content in and reflows (use a matching skeleton).
- Reusing light-mode drop shadows instead of the lighter-surface + glow idiom.
