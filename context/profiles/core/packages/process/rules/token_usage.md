---
paths:
  - "*.tsx"
  - "*.jsx"
  - "*.css"
  - "*.scss"
  - "*.vue"
  - "*.svelte"
  - "*.html"
---

# Token Usage

Use design tokens — named steps on the spacing, type, color, radius, shadow, and motion scales — instead of literal magic numbers. Every value in an interface should trace back to a scale: a `13px` margin, a one-off `#3a7bd5`, or a bespoke `400ms` duration is a defect — use the nearest token (`space-3`, `color-accent`, `duration-fast`).

- **Reference semantic tokens, not primitives.** Components use `color-accent`, never `teal-500`; `text-body`, never `15px` — the semantic layer is the contract, the primitive layer is the brand's to fill. If no token fits, fix the scale, not the call site: a genuinely needed new value means the scale has a gap, so add the step to the system — don't hardcode a one-off.
- **Declare each semantic token's scope: public or private.** A semantic token is either **public/consumable** — part of the stable contract other tiers build on — or **private/internal** — an implementation detail of the system layer, free to be renamed or re-mapped at any time. Every semantic token's scope is declared, and **only public tokens may be depended on across tiers** — a tier reaching for a private token has reached into another tier's internals; treat it the way you'd treat importing an `internal/` symbol from another package.

- the three-layer model, naming, and delivery, plus the full rule and its rationale (consistency, themability, brand-swappability) — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/design_tokens.md" />
- the spacing scale every spacing value traces to — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />
- the type scale — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />
- the semantic color roles — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />
- the duration/easing bands — <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />

Related:

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
