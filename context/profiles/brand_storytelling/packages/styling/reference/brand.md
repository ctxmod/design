# Storytelling — Brand

Storytelling brand essence — narrative arc, three-act structure, restrained editorial palette, the Inter + Abril Fatface pairing, page-turn motion, and pacing through whitespace.

Storytelling treats every interface as a **narrative**: a beginning that draws
the reader in, a middle that does the work, and an end that resolves. The design
exists to present content, not compete with it — color stays quiet, layout
breathes, and dramatic display typography punctuates the journey like
chapter titles. Functional screens should feel like chapters in a book.

The two levers that carry the brand are **typography** (the Inter-to-Abril Fatface
switch — the widest typographic gap in the system) and **pacing through spacing**
(tight reading flow within a section, generous breaks between them). Everything
else is deliberately restrained so those two can be loud.

**Use Storytelling for**: launch and marketing pages, onboarding flows, case
studies, editorial and long-form content, mission-driven and fundraising
products — anything that needs an emotional arc. **Avoid it for** dense,
utilitarian tooling, where pacing and display drama become friction.

## Color palette

The palette is intentionally conventional. Narrative power comes from type and
layout, so color stays a quiet signal layer (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).

```css
:root {
  /* Brand primitives */
  --bs-blue:    #3B82F6; /* "the next step in the story" — primary action */
  --bs-violet:  #8B5CF6; /* marks an important beat — secondary emphasis */
  --bs-success: #16A34A; /* story resolved, goal achieved */
  --bs-warning: #D97706; /* plot tension, pending actions */
  --bs-danger:  #DC2626; /* conflict, destructive actions */

  /* Surfaces & ink */
  --bs-surface: #FFFFFF; /* the blank page */
  --bs-ink:     #111827; /* body text, headings, labels */
  --bs-muted:   #6B7280; /* captions, metadata, the aside voice */
  --bs-hairline: #E5E7EB; /* restrained borders / act dividers */

  /* Semantic wiring (components reference these, never the primitives) */
  --color-surface: var(--bs-surface);
  --color-text:    var(--bs-ink);
  --color-muted:   var(--bs-muted);
  --color-accent:  var(--bs-blue);
  --color-beat:    var(--bs-violet);
  --color-border:  var(--bs-hairline);
}
```

Contrast: `--bs-ink` on `--bs-surface` clears AAA for body. The blue and violet
accents clear 3:1 against white for large text and UI objects but must not be
used for small body text on white — keep them for actions, beats, and large
display moments. Never encode severity in hue alone (pair with icon + label).

**Color supports the acts**: keep the *setup* near-monochrome (ink on white) so
the reader settles; introduce the violet *beat* color sparingly in the *middle*
where attention must spike; let the blue primary appear at the *resolution* as
the single bright "next step." Restraint up front makes the closing accent read
as a climax.

## Typography

The pairing is the soul of the brand.

- **Inter** — the narrator's voice. Body, labels, helper text, UI. Clean,
  invisible, optimized for sustained reading. It carries almost all the words.
- **Abril Fatface** — the chapter title. A high-contrast Didone display face with
  dramatic thick/thin strokes. Used **large and sparingly** for act headings and
  hero moments only — never for body, never for UI labels.

```css
:root {
  --bs-font-body:    "Inter", system-ui, sans-serif;
  --bs-font-display: "Abril Fatface", Georgia, serif;

  /* Editorial scale — perfect-fourth (1.333) for dramatic display contrast */
  --bs-text-caption: 0.833rem;  /* 13px */
  --bs-text-body:    1.125rem;  /* 18px — generous for long-form reading */
  --bs-text-lead:    1.5rem;    /* 24px — opening paragraph */
  --bs-h3:           2rem;      /* 32px */
  --bs-h2:           2.667rem;  /* ~43px */
  --bs-h1:           4.209rem;  /* ~67px — Abril Fatface act title */
  --bs-display:      5.61rem;   /* ~90px — hero chapter title */

  --bs-leading-display: 1.05;   /* big Abril type wants tight leading */
  --bs-leading-body:    1.6;    /* comfortable reading band */
}
```

- **Headings** (`--bs-h1`/`--bs-display`) use `--bs-font-display` at tight
  leading, with letter-spacing slightly negative so the strokes lock together.
- **Body** uses `--bs-font-body` at `--bs-text-body` / `--bs-leading-body`, and
  reading columns are constrained to a **60–70ch measure** — long-form
  readability is non-negotiable (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />).
- Spend personality in the large, short display text; keep the long, small text
  quiet and legible. Putting Abril into body would be a legibility error.

## Motion vocabulary

Motion is narrative pacing — the story *unfolds* (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).

```css
:root {
  --bs-dur-reveal: 600ms;  /* slow scroll reveals — a deliberate beat */
  --bs-dur-page:   400ms;  /* section/page transition — turning the page */
  --bs-ease-page:  cubic-bezier(0.2, 0.0, 0.0, 1.0); /* soft, settling */
}
```

- **Slow reveals** — content fades and rises (~16px translate) as it scrolls into
  view, so each section enters like a new paragraph. Stagger related items by a
  small delay so a group reveals as a sequence, not a flash.
- **Page-turn easing** — transitions settle softly (ease-out family), evoking a
  turned page rather than a mechanical slide.
- **Scroll-tied / gentle parallax** — hero imagery may move slightly slower than
  the text it sits behind; keep it subtle and compositor-only.
- **Reduced motion is mandatory**: under `prefers-reduced-motion`, reveals
  collapse to an instant opacity fade and parallax is disabled. The story must
  still read top-to-bottom with no motion at all.

## Shape & surface

Editorial restraint — the page as a book.

- **Generous margins** frame the content like a printed page; reading regions are
  centered and measure-constrained, not viewport-wide (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/composition.md" />).
- **Restrained chrome** — hairline `--bs-hairline` dividers mark act breaks;
  borders and shadows are minimal. Whitespace, not boxes, does the grouping.
- **Soft, modest radii** (`--bs-radius: 0.5rem`) — present but never playful;
  the drama is in type, not corners.
- The signature is the clean Inter body set against large Abril Fatface display —
  let that contrast be the decoration.

## Three-act structure

Map any page or flow to three acts, pacing each with spacing.

| Act | Maps to | Role | Pacing |
|-----|---------|------|--------|
| **I — Setup** | Hero / opening | Draw the reader in; establish the premise | Largest whitespace; one Abril `--bs-display` title; near-monochrome |
| **II — Confrontation** | Journey / body | Do the work — content, evidence, the case | Tight reading flow within sections, generous `--bs-space-section` breaks between beats; violet beat color appears here |
| **III — Resolution** | Closing / CTA | Resolve; deliver the single next step | Wide breathing room around one blue primary CTA — the climax |

```css
:root {
  --bs-space-flow:    1rem;   /* within a reading block — tight reading flow */
  --bs-space-beat:    2rem;   /* between paragraphs/sub-beats */
  --bs-space-section: 6rem;   /* between acts — the narrative pause */
}
```

Spacing *is* the rhythm: tight within content for flow, wide between sections for
a pause. The acts are differentiated by how much air surrounds them, not by extra
chrome.

## Do / Don't

- **DO** use Abril Fatface sparingly for display drama; **DON'T** set body text in
  the display face.
- **DO** pace with whitespace — tight within sections, generous between;
  **DON'T** cram or fill every region.
- **DO** map each screen to three acts with a clear opening, body, and resolution;
  **DON'T** scatter equal-weight blocks with no arc.
- **DO** keep color quiet and let the blue CTA land as a climax; **DON'T**
  distribute saturated color evenly.
- **DON'T** over-decorate — let typography and spacing carry the story.
</content>

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/buttons.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/inputs.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/cards.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/navigation.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::styling@brand_storytelling/reference/feedback.md" />
- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::platform@web/reference/platform_primitives.md" />
