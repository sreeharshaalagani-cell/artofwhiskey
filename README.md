# artofwhiskey.org

A plain static website. No build step, no framework, no database. Every deck page from
the Google Drive links is published exactly as designed — rendered to image and laid out
one after another, so nothing was redrawn or re-typeset.

## Pages

| File | What's on it |
|---|---|
| `index.html` | Home — big logo, event dates, and a tile for each event |
| `2027-los-angeles.html` | AOW 2027, Los Angeles — the current event deck (15 pages) |
| `2026-silicon-valley.html` | AOW 2026, Silicon Valley (17 pages) |
| `2025-new-orleans.html` | AOW 2025 M.S. Rau (12) + Big Game Big Give (17) + host overview (3) |
| `2025-monaco.html` | Monaco Yacht Show 2025 (11 pages) |
| `2024-las-vegas.html` | AOW 2024, Las Vegas (18 pages) |

The home page is the only hand-built page. Its event tiles use the cover slide of each deck
(`assets/tiles/`), so adding an event means: drop the pages into `assets/decks/`, make a tile
from page 1, and copy an existing event page as the template.

Everything site-wide that isn't a deck page — the top bar, the contact block, the footer
disclaimer — is in each HTML file, so editing one page never breaks another.

## How to publish

Upload the whole folder (both HTML files and `assets/`) to any web host and point
www.artofwhiskey.org at it. `index.html` is the home page.

- **Netlify / Cloudflare Pages** — drag the folder onto app.netlify.com/drop, then add the
  domain in Site settings. Free, fastest option.
- **GoDaddy / cPanel / any shared host** — upload the folder's contents into `public_html`.
- **Squarespace / Wix / Wordpress.com** — these don't host raw HTML well; use one of the above.

## Updating a deck

Replace the JPEGs in `assets/decks/<event>/`. They are named `01.jpg`, `02.jpg`, … and
display in that order. To regenerate from a new PDF:

```bash
pdftoppm -jpeg -r 150 -jpegopt quality=90 NEWDECK.pdf out/x
# then resize each to 1500px wide, quality 76
```

If the new deck has a different number of pages, add or remove the matching `<img>` lines
in that event's HTML file.

## Assets

- `assets/logo.png`, `assets/logo-transparent.png` — original brand logos from Drive
- `assets/logo-mark.png` — the transparent logo, whitespace trimmed; used in the
  top bar and the hero
- `assets/logo-plate.jpg`, `assets/logo-gold.jpg` — plate and gold-foil lockups,
  kept for link previews and social
- `assets/favicon.png` — browser tab icon
- `assets/tiles/` — event cover thumbnails for the home page
- `assets/decks/` — 93 deck pages across five events, ~20 MB total

## Before go-live — worth a look

1. **The 2025 Big Game Big Give and 2024 Las Vegas decks belong to The Giving Back Fund**,
   not to Art of Whiskey. The 2024 PDF is titled "CONFIDENTIAL" and both carry sponsorship
   pricing, celebrity attendee lists and Marc Pollick's personal cell number. Confirm with
   Sean (and ideally with GBF) that these are cleared for a public website before publishing
   those two pages — the files are built and ready either way.
2. **The 3-page "host partner overview"** at the bottom of the 2025 page reads as a private
   one-to-one pitch to a homeowner. Same call.
3. **Venue for Feb 11, 2027 is still TBD** on the deck. Once it's set, the deck page changes
   and so does the site.
4. **Ticketing** — there is no ticket or RSVP flow. Every button goes to
   `star@artofwhiskey.org`. If Sean wants ticket sales, that needs Eventbrite or similar.

## The look

Bright poster palette, pulled from the decks themselves rather than invented: the Hollywood
street-sign blue (`#123A9E`), the neon magenta (`#FF2E86`), the LA sunset orange (`#FF7A18`),
on warm white (`#FFFDF9`) with near-black text. Type is Anton for headlines and Archivo for
everything else, both from Google Fonts.

All of it lives in one place — the `:root` block at the top of every page's `<style>`. Change
a colour there and it changes across that page. The decks are images, so nothing in the CSS
touches their design.
