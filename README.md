# Design

Interface design doctrine for ctxmod (`github.com/ctxmod/design/context`).

Profiles:

- `core` (default): packages `foundations` (design stack, glossary), `principles`, `components` (abstract taxonomy), `process`.
- `web`: the web medium (package `platform`) — platform primitives, responsive layout, rendering performance, web accessibility, web motion, CSS conventions; extends `core`.
- `documents`: paginated print documents (package `print`), with opt-in document-type packages `academic`, `invoice` and `report`; extends `core`.
- `brand_brutalism`, `brand_dramatic`, `brand_expressive`, `brand_forest`, `brand_riso`, `brand_spacious`, `brand_storytelling`: web brand concretizations (package `styling`); each extends `web`.
- `public_sector_web`: Swedish public-sector web requirements — package `sweden` (DOS-lagen, EN 301 549/WCAG, accessibility statements, DIGG open-source checklist, open data, public design systems, mixed-licence media) and `sign_language_media` (STS media licensing); extends `web`.

Select a profile by its qualified name, e.g. `github.com/ctxmod/design/context/profiles/web`; opt-in packages by `<profile>/packages/<package>`.
