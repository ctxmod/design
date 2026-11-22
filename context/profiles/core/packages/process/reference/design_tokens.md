# Design Tokens

The theory of the token model — the primitive/semantic/component three-layer model, tier ownership, token categories, and process.

Design tokens are named, reusable design decisions — the single source of truth for
every spacing value, color, type size, radius, shadow, and duration in a product.
Instead of literal values scattered through components, each component references a
token. This is what makes a design system *consistent* (one source per value),
*themable* (swap values to reskin), and *brand-swappable* (a new brand profile
repopulates the tokens). This document is the **theory** of the token model; the
delivery layer is elsewhere.

> **Scope boundary.** The concrete delivery of tokens for the web — CSS custom
> properties, Tailwind theme config, and the shadcn theming variables — lives in
> the **`shadcn`** (typescript module) profile (see its reference under
> the `shadcn` profile's references in `github.com/ctxmod/typescript/context`). Do not duplicate that here. This file defines the
> *layered model and the umbrella's contract*; `shadcn` (typescript module) defines *how it is
> wired in code*.

## The three-layer model

Tokens are organized into three layers, each referencing the one below it. (Other
literature calls these global/semantic/component or primitive/alias/component; the
structure is the same.)

> **Vocabulary Rosetta (synonym map).** This profile says **Primitive / Semantic /
> Component**. External docs use different names for the same three layers — resolve
> them here:
>
> | This profile | Synonyms |
> |--------------|----------|
> | **Primitive** | Option (Fowler), Reference (W3C / Material), global |
> | **Semantic** | Decision (Fowler), System (W3C / Material), alias |
> | **Component** | Component (Fowler / W3C / Material), component |

```
Layer 1: Primitive  →  Layer 2: Semantic   →  Layer 3: Component
"brand-600 = <value>"  "accent = brand-600"    "button-bg = accent"
"grey-100 = <value>"   "surface = grey-100"    "card-bg = surface"
raw palette/scales     meaning/roles           component-specific
```

### Layer 1 — Primitive (global) tokens

The raw, context-free values: the full color ramps, the complete spacing scale,
every type size, the radius and shadow scales. They have **no inherent meaning** —
`brand-600` is just a color, not "the action color."

- Named by *what they are*, not *what they're for* (`grey-100`, `space-4`,
  `text-lg`, `brand-600`).
- This is the layer a **brand profile populates** — it supplies the actual palette,
  the chosen type sizes, the radius values that express the brand.

### Layer 2 — Semantic (alias) tokens

Roles that map meaning onto primitives: `color-bg-surface`, `color-text-primary`,
`color-text-muted`, `color-border`, `color-accent`, `color-accent-foreground`, and
the status roles `success` / `warning` / `danger` / `info`. Spacing and type get
semantic aliases too where useful (`space-section`, `text-body`).

- Named by *purpose*: `accent`, not `teal-500`.
- This is the layer the **umbrella owns as a contract.** The umbrella declares
  *which semantic roles exist and what they mean* (this is the same contract the
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> and component docs reference); brand
  profiles decide which primitive each role resolves to.
- **Theming happens here.** Light and dark are two sets of semantic→primitive
  mappings over the *same* role names. A component using `color-text-primary` works
  in both themes without change (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).

### Layer 3 — Component tokens

Optional, component-specific aliases that reference semantic tokens:
`button-primary-bg`, `card-padding`, `input-border-focus`. They give a component a
stable hook to tune without editing the component, and let one component diverge
from the semantic default deliberately.

- Use sparingly. Most components should reference semantic tokens directly;
  introduce a component token only when a component genuinely needs its own
  controllable value.
- Named `component-property[-variant][-state]`.

## Modes (orthogonal axis)

The three token layers above (primitive / semantic / component) are **unchanged** by
this section. Modes are an **orthogonal axis** that cuts across the layers — they are
**not a fourth layer**.

A **mode** is an axis over which the **semantic → primitive** mappings re-resolve. The
role name stays constant; only the primitive it points to changes. Three modes:

- **theme** (light / dark) — semantic *color* tokens swap their primitive reference per
  theme. `color-text-danger` resolves to one primitive in light, another in dark.
- **density** (compact / comfortable / spacious) — semantic *spacing / sizing* tokens
  resolve to different primitives per density. `space-component-pad` resolves to a
  tighter primitive in compact, a looser one in spacious.
- **locale** (language / region) — semantic *typography* tokens (family, weight,
  line-height, letter-spacing) resolve per locale. E.g. a CJK locale lacks a true bold
  weight, so `font-weight-emphasis` overrides to a heavier-available primitive, and
  line-height widens for ideographic scripts.

**The key rule: modes are NOT new layers.** A semantic role name
(`color-text-danger`, `space-component-pad`, `font-family-body`) is constant across every
mode; only its primitive reference changes per mode. **Components change nothing** — a
component referencing `color-text-danger` works in every theme, density, and locale
without edits, exactly as it works across brand swaps.

|                          | theme (light/dark) | density (compact/…/spacious) | locale (lang/region) |
|--------------------------|--------------------|------------------------------|----------------------|
| **Primitive** (Layer 1)  | full ramps / scales (mode-independent values) | full spacing/size scale | full type scale + weight set |
| **Semantic** (Layer 2)   | *re-resolves* — color roles swap primitive | *re-resolves* — spacing/size roles swap primitive | *re-resolves* — type roles swap primitive |
| **Component** (Layer 3)  | unchanged | unchanged | unchanged |

> **DTCG status.** As noted under "Canonical format" above, theming/modes are *not yet*
> native to the W3C DTCG spec (GitHub Issue #210). Modes therefore live at the **system
> layer** — a set of alternate semantic→primitive mappings over the same role names — not
> inside the interchange format.

The three concrete modes are each documented as *modes* in their principle files:
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />,
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" />, and
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/internationalization.md" />.

## Who owns which layer (the tier contract)

This mapping is the crux of the three-tier architecture (see the
<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::components@core/reference/taxonomy.md" />):

| Layer | Owned by | Defines |
|-------|----------|---------|
| Primitive | **Brand profile** | The actual palette, type, radius, shadow values |
| Semantic | **Umbrella (this profile)** | The role names and their meaning (the contract) |
| Component | Umbrella or brand | Per-component hooks where needed |
| Delivery (CSS/Tailwind/shadcn) | **`shadcn`** (typescript module) | How tokens are expressed and consumed in code |

Because the umbrella fixes the semantic contract, a brand can swap the entire look
by repopulating primitives, and every component — which only knows semantic
tokens — follows automatically.

## What a token is (vs. a CSS variable)

A **token is an abstract design decision** — a value bound to a role (`color-text-danger`
*means* "text that signals a destructive or error state," resolving to some primitive).
A **CSS custom property is one *implementation* of that decision** for the web; the same
token can equally be emitted as a Swift constant, an Android resource, or a Figma style.
Tokens are not "just CSS variables" — CSS variables are one delivery target (owned by
`shadcn` (typescript module), see the scope boundary above) for a format-neutral decision that lives above
any single platform.

## Canonical format: W3C DTCG

The canonical interchange format for tokens is the **W3C Design Tokens Format Module
(DTCG), v2025.10 stable**. It is the cross-medium standard: author tokens once in DTCG
JSON and translate them to every platform's delivery format. Its core:

- **`$value` / `$type` / `$description`.** Every token is an object with a `$value`, a
  `$type` declaring its kind, and a `$description` explaining its role.
- **`{group.token}` references** express aliases — a semantic token references a primitive
  by path (`"$value": "{color.brand.600}"`), which is exactly the Layer 2 → Layer 1
  mapping above.
- **Typed values** — DTCG defines composite and primitive types including `dimension`,
  `duration`, `cubicBezier`, and `fontFamily` (per §8.5 / §8.6), so a value carries its
  own semantics rather than being an untyped string.

```json
{
  "color": {
    "brand": { "600": { "$type": "color", "$value": "#1d4ed8" } },
    "text": {
      "danger": {
        "$type": "color",
        "$value": "{color.brand.600}",
        "$description": "Text that signals a destructive or error state."
      }
    }
  }
}
```

> **Modes are not native to DTCG.** Theming/modes (theme, density, locale) are *not yet*
> part of the spec — this is unresolved (DTCG GitHub Issue #210). So modes are handled at
> the **system layer**, not inside the token format: a mode is a different set of
> semantic→primitive mappings over the *same* role names. See the Modes subsection of the
> medium charter (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/medium_charter.md" />), and the mode-axis treatments in
> <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/information_density.md" /> and
> <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/internationalization.md" />.

## Cross-platform delivery

One DTCG source feeds every medium. The established pattern (Amazon's **Style
Dictionary**, Microsoft's **Fluent UI Token Pipeline**) is: a single
**DTCG-compatible JSON source** runs through **transform groups** — each group a
named pipeline of transforms (name flattening, value coercion, unit handling) plus
a formatter — to emit a per-medium artifact:

| Medium | Emission target |
|--------|-----------------|
| Web | CSS custom properties (delivery owned by `shadcn` (typescript module)) |
| iOS | Swift constants |
| Android | XML resources |
| CLI | ANSI escape sequences |
| Print | LaTeX lengths / colors |

The umbrella's **semantic contract is the source of truth**; the media are
*emission targets*, not authorities. A token decision (`color-text-danger` *means*
"text that signals a destructive or error state") is authored once in DTCG and
projected onto each platform's format. **Adding a medium is adding a transform
group, never editing the umbrella** — the role names and meanings stay fixed; a new
group teaches the pipeline how to render the existing contract for one more target.

This is the forward-compat guarantee: the semantic layer is medium-independent, so
new platforms attach at the delivery edge without touching the contract every
component already depends on.

> **Web stays in `shadcn` (typescript module).** The concrete CSS-custom-property / Tailwind
> delivery is the web transform group's output and lives in the **`shadcn`** (typescript module)
> profile (see the scope boundary above and the `shadcn` profile's references in `github.com/ctxmod/typescript/context`). This section
> describes the *shape of the pipeline*, not web specifics — do not duplicate
> CSS/Tailwind wiring here.

Each medium's transform group must satisfy the obligations defined in the
Medium Profile Charter (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/reference/medium_charter.md" />) — that charter fixes what every medium
is required to provide so the same semantic contract renders coherently across all
of them.

## Naming semantic tokens

Semantic tokens follow the template **`category-property-role-state`** (e.g.
`color-text-danger`, `color-border-focus`, `space-inset-compact`). The non-negotiable rule:

**Name by purpose/role, never by appearance.** A token's name says *what it is for*, not
*what it looks like* — so a brand can change the appearance without the name becoming a lie.

| Don't (appearance) | Do (role) |
|--------------------|-----------|
| `color-text-red`   | `color-text-danger` |
| `color-bg-blue-light` | `color-bg-accent-subtle` |
| `space-16`         | `space-section` |

**Mandate `$description` on every semantic token.** The role is what makes a semantic token
useful, and the name alone cannot fully carry it. The `$description` is the disambiguation
tool — it tells a downstream brand agent (human or model) what the role *means* so it maps
the right primitive (`color-text-danger`: "Text that signals a destructive or error state,"
not "red text"). A semantic token without a `$description` is underspecified.

### Two naming stages, not two rivals

Authoring and output use complementary conventions for the same token:

- **Dot-notation for authoring** — DTCG JSON nests by group (`color.text.danger`), matching
  the `{group.token}` reference syntax.
- **Flat semantic kebab-case for output** — delivery flattens the path to a single name
  (`--color-text-danger`).

These are two stages of one pipeline (author → translate → emit), not competing schemes.

## Token categories

A complete token system covers (each ties to a principle doc):

- **Color** — surface ramp, text ramp, border, accent, status; light + dark
  mappings (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).
- **Spacing** — the base-unit scale (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />).
- **Typography** — font families, the modular size scale, weights, line heights,
  letter-spacing (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />).
- **Radius** — a small radius scale (larger elements, larger radius).
- **Shadow / elevation** — an elevation ladder (and its dark-mode counterpart).
- **Motion** — duration bands and easing curves (see
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).
- **Layout** — content max-widths and breakpoints (medium-tier specifics).

## Process

1. **Check what already exists** before defining anything — extend, don't replace.
2. **Define the semantic contract first** (this profile's job): the role names and
   meanings every component will reference.
3. **Populate primitives** from the brand (the brand profile's job): the actual
   values for each scale and ramp.
4. **Generate both light and dark** semantic mappings — intentional, not inverted
   (see <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" />).
5. **Wire delivery** via `shadcn` (typescript module) — express the tokens as CSS variables /
   Tailwind config / shadcn theme.
6. **Components reference tokens, never literals** (see the
   <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::process@core/rules/token_usage.md" />).

## Anti-patterns

- Hardcoded literal values in components instead of tokens.
- Primitive tokens used directly in components (skipping the semantic layer), which
  breaks themability.
- Duplicating the `shadcn` (typescript module) delivery details here.
- A dark theme built by inverting values rather than remapping semantic roles.
- An explosion of component tokens for values that should be semantic.

## Rule Companion: Token Usage — Full Rule and Rationale

*Companion to the `token_usage` rule: its full rule set, worked examples and rationale.*

### The rule

- **No magic numbers.** A `13px` margin, a one-off `#3a7bd5`, a bespoke `400ms`
  duration are defects. Use the nearest token (`space-3`, `color-accent`,
  `duration-fast`).
- **Reference semantic tokens, not primitives.** Components use `color-accent`,
  never `teal-500`; `text-body`, never `15px`. The semantic layer is the contract;
  the primitive layer is the brand's to fill.
- **Every value traces to a scale.** Spacing → the
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/spacing_scale.md" />. Type → the
  <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/typography.md" />. Color → the
  semantic <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/color.md" /> roles. Motion → the
  duration/easing bands (<ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::principles@core/reference/motion.md" />).
- **If no token fits, fix the scale, not the call site.** A genuinely needed new
  value means the scale has a gap — add the step to the system so it's reusable.
  Don't hardcode a one-off.
- **Declare each semantic token's scope: public or private.** A semantic token is
  either **public/consumable** — part of the stable contract other tiers build on,
  the role names a brand or component is allowed to depend on — or
  **private/internal** — an implementation detail of the system layer, free to be
  renamed or re-mapped at any time. The obligation: every semantic token's scope is
  declared, and **only public tokens may be depended on across tiers.** A tier
  reaching for a private token has reached into another tier's internals; treat it
  the way you'd treat importing an `internal/` symbol from another package.

### Why

- **Consistency** — one source of truth per value; the same gap, color, and timing
  everywhere. Ad-hoc values are how a design quietly drifts out of alignment.
- **Themability** — light/dark and density variants are just different mappings of
  the same token names; hardcoded values can't switch.
- **Brand-swappability** — a brand profile reskins the entire product by
  repopulating tokens, *because* components reference tokens rather than literals.
  Every hardcoded value is a place the swap breaks.

Tokens are what turn a pile of styled components into a coherent, portable design
system. Treat a literal value in a component the way you'd treat a hardcoded
constant in code that should reference a shared definition.

## Related

- <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::foundations@core/reference/glossary.md" />
