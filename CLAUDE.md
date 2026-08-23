# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this is

A static site served at **briefs.ainsof.io** (GitHub Pages — `CNAME` at the repo
root is the only deploy config; there is no CI, no build step, no package
manager). Every page is a single hand-written `index.html` with all CSS inlined
in one `<style>` block and the AINSOF logo embedded as a base64 PNG data URI.
Editing a file and pushing to `main` is the whole deploy.

Content is private-by-convention, not by access control: the pages are
unlisted, and the root `index.html` is a stub that says "Private — restricted
access." Nothing links to the individual briefs. Don't add an index, sitemap,
or cross-links between briefs.

## Layout

```
index.html                        stub landing page
<composer-slug>/index.html        one composer brief per directory
submit-invoice/index.html         composer payment portal
assets/og_thumb.png               250x250 link-preview image (site-wide)
submit-invoice/assets/            logo, hero banner, own og_thumb
favicon.*, *manifest*             site icons
```

Current briefs: `elram-bokser`, `idan-zion`, `roman-marin`,
`roman-marin-run-it-back`, `tom-goldstein`. The slug is the URL — a composer
with a second album gets a second directory (`roman-marin-run-it-back`), not a
second page inside the first.

Unreferenced files, safe to ignore but don't delete without asking:
`assets/og_card.png` and `submit-invoice/assets/og_card.png` (superseded by
`og_thumb.png` when previews moved to compact cards), and
`submit-invoice/covers/` (18 album covers, not used by any page).

## Brief page structure

Briefs share a template, copied per page rather than shared. Sections are
numbered `01 —` upward in a `.section-eyebrow` div; pages differ in whether they
include a "Sonic Direction" section, so **the numbers are per-page, not fixed**.
Renumber the rest if you insert or remove one.

```
hero            eyebrow "Composer Brief", "AIN-CAT NNN — Composer",
                title, italic gold tagline, meta line
01 The Brief    concept prose
02 Sonic Identity   tags & instruments
(  Sonic Direction  production notes — present on some briefs only )
   References   two anchor tracks, linked out to audiomachine /
                epidemicsound / sourceaudio
   Track List   one .track div per track, named
                "AIN-CAT NNN_trkNN_Title"
   The Deal     .deal-table: Album Code, Composer, Type, Tracks, Rate,
                Total Fee, Deadline, Sync, Performance
   Delivery     .delivery-card linking to https://delivery.ainsof.io/
footer          AINSOF logo, info@ainsof.io, search.ainsof.io
```

Delivery specs live at delivery.ainsof.io, not in this repo — briefs link out
rather than restating WAV/stem/loudness requirements.

## House style

Briefs use the dark/gold palette declared as CSS custom properties at the top of
each file:

```
--bg #0A0A0C   --surface #111117   --gold #D4AF5A   --text #F0ECE3   --muted #7A7570
```

Headings are Georgia serif; body and eyebrows are Arial with wide uppercase
letter-spacing. The hero has an SVG `feTurbulence` grain overlay.
`submit-invoice/` is a deliberately separate, brighter system (Inter from Google
Fonts, `--accent #E8C547`, near-black `#08080A`) — don't unify the two.

When creating a new brief, copy the closest existing brief and edit it. Match
the source file's formatting; these are hand-maintained documents, not generated
output.

## Link previews

Every page carries Open Graph + Twitter card meta tuned for WhatsApp/Telegram:
`twitter:card=summary` with a **250x250** `og_thumb.png` (deliberately under
WhatsApp's 300px threshold, so the compact preview renders instead of a wide
banner). Keep the `og:image:width`/`height` tags in sync with the actual file,
and set `og:url` to the page's own absolute URL.

## Facts worth not re-deriving

- Album codes are `AIN-CAT NNN`; art briefs use `AIN-ART`.
- Terms on current briefs are buyout, sync 100% AINSOF, performance split
  50/50 — but every brief states its own; never carry numbers across.
- Contact is `info@ainsof.io` in brief footers, `or@ainsof.io` on the invoice
  page.
- The invoice portal is a landing page in front of a Google Form; it collects
  nothing itself.
