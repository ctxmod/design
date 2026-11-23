# Accessibility: DOS-lagen and tillgänglighetslagen

The legal and standards backdrop that Swedish public-sector organisations
measure web work against, plus the EU Accessibility Act law that reaches
private services the public sector procures, integrates or competes with.
Verified against primary sources 2026-11-23 (earlier pass 2026-10-30);
re-verify the load-bearing clauses before they shape a deliverable.

## DOS-lagen (public sector)

- **DOS-lagen** (Lag 2018:1937 om tillgänglighet till digital offentlig
  service) implements the EU Web Accessibility Directive (2016/2102). It is
  most recently amended by SFS 2026:1625, whose new § 4 wording takes effect
  2027-01-01 (it extends the list of social-services laws whose activities
  fall in scope). It requires the accessibility rules in DIGG's föreskrifter
  plus a **tillgänglighetsredogörelse** (accessibility statement).
- The supervisory authority is "den myndighet som regeringen bestämmer"
  (§ 16) — designated by ordinance, not named in the act, which is why the
  2027 agency merger below changes the supervisor without amending the act.
- The legal conformance bar is **EN 301 549 V3.2.1**, which maps to
  **WCAG 2.1 level A + AA** (DIGG, page updated 2026-05-08). Swedish
  public design systems commonly aim higher: FKUI states WCAG 2.2 AA.
  Work that targets **WCAG 2.2 AA** and documents 2.1 AA conformance is
  both honest and ahead of the legal minimum.

## The standard is moving: EN 301 549 V4.1.1

- **EN 301 549 V4.1.1** was published on 2026-09-02. It adopts **WCAG 2.2
  Level AA** for web content, non-web documents and software, and adds
  requirements beyond WCAG (notably reworked real-time communication and
  user-preference clauses) — WCAG 2.2 AA alone does not establish V4.1.1
  conformance.
- It gives presumption of conformity only once the European Commission cites
  it in the Official Journal. As of 2026-11-23 it is **not cited**; published
  expectations range from late November 2026 to January 2027. Until then
  V3.2.1 — cited under the Web Accessibility Directive through Implementing
  Decision (EU) 2018/2048 as amended in 2021 — remains the reference.
- Practical stance: build and test to WCAG 2.2 AA now, keep the statement's
  conformance claim against the cited edition, and plan the switch of the
  claim to V4.1.1 when citation and DIGG's guidance follow.

## Supervision: DIGG today, Digitaliseringsmyndigheten from 2027

- **DIGG** supervises DOS-lagen. It monitors (an automated review of about
  400 sites started 2026-04-27, focused on schools and regions, alongside
  reviews of a service against EN 301 549 and of its statement), and opens
  supervision cases from monitoring or from public complaints (the *anmälan*
  route on digg.se).
- Outcomes escalate from a **påpekande** (notice, no deadline) to a
  **föreläggande** (order with a deadline) and, if an order is ignored, a new
  order carrying a **vite** (conditional fine sized to the estimated cost of
  remediation). Fines cannot be imposed on the state, though agencies are
  expected to comply.
- **From 2027-01-01 DIGG and PTS merge into Digitaliseringsmyndigheten**
  (government decision reported 2026-05-18). Statements, complaint routes and contact
  details that name DIGG — and the PTS supervision described below — should
  be re-checked after the merger; the web presence of the new agency is
  being built out during 2027.

## Tillgänglighetslagen (EAA, private services)

- **Lag (2023:254) om vissa produkters och tjänsters tillgänglighet**
  implements the European Accessibility Act (2019/882) and has applied since
  **2025-06-28**. It covers products and services such as e-commerce,
  consumer banking, electronic communications, e-books, access to
  audiovisual media and passenger-transport service elements — including
  their websites and apps.
- Supervision is split by förordning (2023:676): **PTS** is the market
  surveillance authority for products and supervises e-commerce, banking and
  electronic-communications services (and coordinates); **Mediemyndigheten**
  audiovisual-media access; **Myndigheten för tillgängliga medier** e-books;
  **Konsumentverket** and **Transportstyrelsen** passenger-transport elements.
  PTS's part moves to Digitaliseringsmyndigheten with the 2027 merger.
- No harmonised standard is yet cited under the EAA; EN 301 549 V4.1.1
  carries the EAA mapping annexes and is the expected route to presumption of
  conformity once cited. A public authority's site is under DOS-lagen, but an
  e-service or app it builds for a regulated private actor, or procures from
  one, may be under this law instead — name the applicable law per surface.

## The tillgänglighetsredogörelse

A tillgänglighetsredogörelse is public and structured:

- the method used (automated plus manual sampling, screen readers such as
  NVDA, browsers);
- how the content meets the criteria;
- known accessibility problems and what is being done about them;
- how to report problems (with the authority's response duty);
- the tillsynsmyndighet — DIGG (Digitaliseringsmyndigheten from 2027-01-01).

Published authority statements that report their gaps honestly are the
format to model; a demo or prototype can ship its own statement in that
format.

## The EU frame

The Web Accessibility Directive's formal review was completed in 2022
(evaluation SWD(2022) 410 and its supporting study); no revision proposal
followed. Member States report monitoring results every three years (reports
for 2020–2021 and 2022–2024 are published), so the next national monitoring
report falls due in 2027.

## Sources

- https://data.riksdagen.se/dokument/sfs-2018-1937.html — DOS-lagen consolidated text, amended through SFS 2026:1625 (§ 4 wording in force 2027-01-01), § 16 supervisory authority designated by government; accessed 2026-11-23
- https://www.digg.se/kunskap-och-stod/digital-tillganglighet/rattslig-vagledning/10.-tillsynsarbete-och-overvakning — DIGG supervision: review against EN 301 549, påpekande / föreläggande / vite, no fines on the state (page updated 2026-01-16); accessed 2026-11-23
- https://www.digg.se/om-oss/nyheter/digital-tillganglighet/nyheter/2026-04-27-nu-startar-arets-automatiska-granskning-av-digital-offentlig-service — 2026 automated review start (~400 sites), 2026-04-27; accessed 2026-11-23
- https://digitaliseringsmyndigheten.se/ — PTS and DIGG become Digitaliseringsmyndigheten on 2027-01-01; accessed 2026-11-23
- https://www.dagensnaringsliv.se/20260518/290452/regeringen-bildar-ny-digitaliseringsmyndighet — report of the government's merger decision, 2026-05-18; accessed 2026-11-23
- https://data.riksdagen.se/dokument/sfs-2023-254.html — Lag (2023:254), EAA implementation, applies from 2025-06-28; accessed 2026-11-23
- https://data.riksdagen.se/dokument/sfs-2023-676.html — Förordning (2023:676) §§ 25–31: supervisory authorities per service and product (amended through SFS 2026:290); accessed 2026-11-23
- https://nda.ie/news/en301549-published — EN 301 549 V4.1.1 published 2026-09-02, WCAG 2.2 AA, binding only after OJEU citation; accessed 2026-11-23
- https://www.deque.com/blog/en-301-549-v4-1-1-is-final-what-changed-what-it-means-and-what-you-should-do/ — V4.1.1 additions beyond WCAG and moving citation estimate (2026-09-08, updated); accessed 2026-11-23
- https://digital-strategy.ec.europa.eu/en/policies/web-accessibility — Web Accessibility Directive: 2022 review (SWD(2022) 410/411), three-yearly monitoring reports, EN 301 549 V3.2.1 as cited basis (page updated 2026-06-23); accessed 2026-11-23
