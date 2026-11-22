# Swedish Sign Language media: what an open repository may use

Licensing landscape for Swedish Sign Language (STS) media in an open
repository — Wikimedia Commons Spread the Sign clips (CC BY / CC BY-SA 3.0)
as the only redistribution-safe bundled pool, the CC BY-NC-SA lexicon and
corpus (link-out only), restrictive authority video terms, and the sector's
WFD/WASLI stance against signing avatars. Verified at source 2026-10-30.
Public institutional contact addresses below are the institutions' own.

## The redistribution-safe pool: Wikimedia Commons

The only verified pool whose clips may be bundled in a permissive open
repository:

- **`Category:Swedish Sign Language - SpreadTheSign`** (21 files): 20 ×
  CC BY-SA 3.0 and 1 × CC BY 3.0 (`File:67329.webm`, "hej"). Uploaded by
  Spread the Sign via the Wikimedia Sverige partnership, covered by VRT
  permission ticket 2013091910008774. Mostly single signs, two full
  sentences, one greeting.
- **`Category:Alphabet in Swedish Sign Language`** (29 files): the manual
  alphabet A–Ö, all CC BY-SA 3.0.
- Commons per-file `extmetadata` carries author, licence, source URL and
  date in machine-readable form — free provenance data for a demo's
  evidence panel. Signers are not named per clip; an honest provenance
  record keeps a `signer: null`/"ej namngiven i källan" field.
- Files are small (320×240, 2–9 s) and several are Theora `.ogv`; a
  container transcode (e.g. to MP4/WebM) of an unmodified work is not a
  licence adaptation (share-alike binds Adapted Material only), but keep
  the original hashes in the metadata.

## Link-out only: CC BY-NC-SA sources

- **Svenskt teckenspråkslexikon**, Stockholms universitet — live at
  `teckensprakslexikon.su.se` (the old `teckensprakslexikon.ling.su.se`
  host fails TLS). Site licence **CC BY-NC-SA 4.0**, with an explicit
  extra-permission route (teckenlexikon@ling.su.se). Stable direct video
  paths exist (`/movies/NN/<word>-<id>-tecken.mp4`, plus full example
  sentences `-fras-N.mp4`), but hotlinking bypasses their player and
  analytics: linking to the `/ord/<id>` pages is the polite route.
  Sentence-level content is everyday-shaped and ideal as material —
  blocked from bundling only by the NC term.
- **Svensk teckenspråkskorpus** (`teckensprakskorpus.su.se`): identical
  CC BY-NC-SA 4.0 statement; full access is behind login.
- **STS Mocap v1, SignSparK (data/checkpoints), SignAvatars, sign.mt**:
  non-commercial, and the STS Mocap addendum extends restrictions to
  derived outputs, synthetic data, model weights and embeddings — these
  kill even indirect use in a public permissive repo.

## Spread the Sign live site

`spreadthesign.com`'s current terms are personal-use-only, requiring a
licence from the European Sign Language Center for other use. The Commons
mirrors of its clips were released there by Spread the Sign themselves
under CC BY(-SA) 3.0, and CC licences are irrevocable for material already
distributed under them: **use the Commons copies with Commons metadata;
never scrape the live site.**

## Public-authority STS video: linking sometimes, redistribution never

| Source | Terms | Verdict |
|---|---|---|
| Riksdagen | Copyright-protected; web TV needs "Källa: Sveriges riksdag" for editorial reuse, permission for editorial films; linking fine, **framing forbidden** | Link out at most |
| MFD | Own videos copyright-protected, no sharing without permission; links and embed codes offered case-by-case via info@mfd.se | No bundling; link or ask |
| SVT / SVT Play | No use outside SVT Play | Out |
| 1177 / UR | Not verified; health/school content, out of a non-clinical demo's scope anyway | Out of scope |

## The NC question for portfolio and commercial-adjacent work

CC's NC definition turns on the **use**, not the reuser's identity: NC
means "not primarily intended for or directed towards commercial advantage
or monetary compensation". A demo built to win paid work, or hosted under a
company domain, is a contested NC reading. Linking out is unconditionally
safe (a link implicates no licence); embedding or bundling NC media is not
clean. The settled posture for portfolio work: bundle only Commons
CC BY(-SA) clips, link out to the lexicon, keep NC material out.

## Sector stance and framing risks

- **WFD/WASLI position against replacing interpreters with signing
  avatars.** Any "AI interpreter" or avatar framing reads as tone-deaf to
  the Deaf community. Retrieval of approved human signing, with visible
  provenance and honest labels (recorded / generated / human-reviewed /
  not validated), is the safe framing.
- **Non-clinical scope.** Emergency information, medical consent and legal
  interpretation are exactly the uses this kind of product must refuse to
  claim; demo content should be general service or visitor information.
- Positioning text around a product built on this material belongs in that
  project's own record, not in this shared reference; nothing here names a
  client or target authority for a product commercially.

See also <ctxmod_link path="ctx:github.com/ctxmod/design/context::shared::sweden@public_sector_web/reference/mixed_licence_media.md" />
for bundling CC-licensed media in a permissively licensed repository.
