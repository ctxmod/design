# Spacious — Brand

Spacious brand essence — whitespace as the primary design element, blue-violet accent on light neutrals, Open Sans + Montserrat, calm motion, generous 8pt-grid defaults.

Spacious is **whitespace-first**. It rests on a single conviction: the most
important element in any interface is the space *between* elements. Everything
else — the conventional palette, the readable type, the calm motion — defers to
that idea. The brand fills the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />
slots, as mapped to the web by `web`, with generous, quiet, room-to-breathe
styling.

## Essence

Whitespace is not leftover space; it is the primary design material (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />). Spacious uses it as the carrier of
**hierarchy**: more space around a thing means it is more important. A generous
layout signals calm, confidence, and a premium, considered product. The feel is
unhurried and clear — never cramped, never anxious.

**Use Spacious for**: enterprise SaaS and dashboards, premium and content-heavy
products, health/wellness, financial services, education, government — anywhere the
goal is calm, clarity, and trust. **Avoid it for** information-dense expert tools
that must maximize data per screen; its generous defaults trade density for
breathing room by design.

## Color palette

Conventional and quiet by intent — color is a *signal*, not decoration (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />). Blue-violet accents sit on a near-white neutral ground.

| Role | Token | Value | Use |
|------|-------|-------|-----|
| Accent (primary) | `--color-accent` | `#3B82F6` | Primary actions, focus, active nav — a clear, trustworthy blue |
| Accent (secondary) | `--color-accent-2` | `#8B5CF6` | Complementary violet, sparing emphasis |
| Success | `--color-success` | `#16A34A` | Confirmations, positive feedback |
| Warning | `--color-warning` | `#D97706` | Caution, pending |
| Danger | `--color-danger` | `#DC2626` | Errors, destructive actions |
| Surface (base) | `--color-surface` | `#FFFFFF` | Expansive white — the hero element |
| Surface (sunken) | `--color-surface-sunken` | `#F9FAFB` | Wells, input rests |
| Border | `--color-border` | `#E5E7EB` | Thin, hairline neutral dividers |
| Text | `--color-text` | `#111827` | Body, headings, labels |
| Text (muted) | `--color-text-muted` | `#6B7280` | Helper text, captions |

```css
:root {
  --color-accent: #3B82F6;
  --color-accent-2: #8B5CF6;
  --color-surface: #FFFFFF;
  --color-surface-sunken: #F9FAFB;
  --color-border: #E5E7EB;
  --color-text: #111827;
  --color-text-muted: #6B7280;
}
```

Light-first. Accent text on white clears WCAG AA for UI components and large text;
use `--color-text` (not the accent) for body. **Restraint is the rule** — most of
the screen is white and neutral; the blue appears only where it carries meaning.
Do not distribute hues evenly, and never use the danger hue decoratively.

## Typography

Two faces, each doing one job (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />):

- **Open Sans** — body and UI text. Humanist sans-serif, highly readable across
  wide columns. Weights 400 (body) / 600 (emphasis).
- **Montserrat** — headings and display. Geometric, confident; its visual weight
  anchors large areas of empty space so the whitespace reads as composed, not
  empty. Weight 600.
- **IBM Plex Mono** — code and technical data.

```css
:root {
  --font-body: "Open Sans", system-ui, sans-serif;
  --font-display: "Montserrat", system-ui, sans-serif;
  --font-mono: "IBM Plex Mono", ui-monospace, monospace;
}
```

Type scale (px): `12 / 14 / 16 / 18 / 24 / 30 / 36`. Line-height runs **generous**
— body at `1.6`, headings at `1.2` — so text itself breathes. Moderate weights
only; the calm comes from space, not from heavy type.

## Motion vocabulary

Calm, smooth, unhurried. Motion confirms, it never performs (see
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

```css
:root {
  --ease-standard: cubic-bezier(0.4, 0, 0.2, 1);
  --dur-fast: 150ms;   /* hover, focus */
  --dur-base: 220ms;   /* state changes, fades */
}
```

Standard eases, medium durations, subtle fades and short slides. **No bounce, no
spring, no decorative animation.** Always honor `prefers-reduced-motion: reduce` by
dropping transitions to near-instant opacity changes.

## Shape & surface

- **Padding is larger than other brands by default.** Component internal padding
  starts at `24px`, not `12–16px` (see the 8pt grid below).
- **Soft radii** — `--radius: 8px` for controls, `--radius-lg: 12px` for cards.
- **Soft, diffused shadows** — Spacious is the one place a gentle shadow is
  welcome; it suggests calm elevation, never a hard edge.
- **Thin neutral borders** — `1px` `--color-border`, used as hairlines, never as
  heavy frames.

```css
:root {
  --radius: 8px;
  --radius-lg: 12px;
  --shadow-soft: 0 1px 3px rgba(17, 24, 39, 0.06), 0 4px 12px rgba(17, 24, 39, 0.05);
}
```

## The 8pt grid

Every margin, padding, and gap is a multiple of 8px. This *is* the brand. The
scale concretizes the umbrella <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />:

```css
:root {
  --space-1: 4px;   /* half-step, tight inline only */
  --space-2: 8px;   /* icon-to-text */
  --space-3: 16px;  /* related items */
  --space-4: 24px;  /* DEFAULT component padding */
  --space-5: 32px;  /* between groups */
  --space-6: 48px;  /* section separation */
  --space-7: 64px;  /* page region break */
  --space-8: 96px;  /* hero / page top */
}
```

The spacious feel comes from **generous defaults**: component padding starts at
`--space-4` (24px) and section separation at `--space-6` (48px), where denser
brands would use 12–16px and 16–24px. When uncertain, choose *more* space, not
less. The 4px half-step exists for tight inline gaps only — everything structural
snaps to 8.

## Do / Don't

**Do**

- Default to more space than feels necessary; let whitespace create hierarchy.
- Keep strictly to the 8pt grid — every gap is a multiple of 8.
- Use the blue-violet accent as a quiet signal, on a mostly-white ground.
- Reach for soft, diffused shadows and thin hairline borders for gentle elevation.

**Don't**

- Cram. Reducing padding below the generous defaults breaks the brand.
- Use loud or evenly-distributed color; color is a scarce accent.
- Add heavy borders, hard shadows, or bouncy motion.
- Put personality into the body font — keep Open Sans quiet, spend Montserrat on
  short headings (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />).

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/navigation.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_spacious/reference/feedback.md" />
