# cognio-drivers-public

Public repository for completed Cognio device drivers.

## Driver library website

`index.html` is a self-contained, dependency-free page that lists every
released driver and lets you filter by manufacturer, category, and validation
level. A short key under the Validation filter explains each level
(Spec-built, Hardware-verified, Field-validated). It reads `index.json`
(regenerated automatically by the release pipeline in the private
`cognio-drivers` repo) and links to each driver's `.cogdriver` download.

Once GitHub Pages is enabled (Settings → Pages → Deploy from a branch →
`main` / root), the library is published at:

**https://symetrix-audio.github.io/cognio-drivers-public/**

## Analytics and consent

The page reports to Google Analytics 4 (measurement ID `G-99Z52XH46H`) using
Consent Mode v2:

- **EEA / UK / Switzerland:** analytics is off by default. No GA cookies are
  set until the visitor clicks **Accept** in the consent banner.
- **Everywhere else:** analytics is on by default. **Decline** opts out.
- Advertising features (ad storage, Google signals, ad personalization) are
  always off. GA cookies are host-only, so they're never shared with
  www.symetrix.co.
- The visitor's choice is saved in their browser. **Cookie settings** in the
  footer reopens the banner so they can change it.
- **Global Privacy Control (GPC)** is honoured. If the browser sends the GPC
  opt-out signal (`navigator.globalPrivacyControl`), the page treats it as
  **Decline**: analytics is off, the banner isn't shown, and any existing GA
  cookies are removed. The signal overrides an earlier Accept for as long as the
  browser sends it. **Cookie settings** then explains that GPC is on instead of
  offering a choice.
- Every **Download** click sends a `file_download` event with `driver_brand`,
  `driver_product` and `driver_version`. Register those three as event-scoped
  custom dimensions in GA Admin to report on them.
- Download counts are a **lower bound**. Left click, Ctrl/Cmd+click, Enter and
  middle-click are counted. Right-click → "Save link as…" can't be seen by the
  page, so those downloads are missed. Read the numbers as trends, not exact
  totals.
- Downloads also show up as **outbound clicks**, because the files are served
  from `raw.githubusercontent.com` and GA4's enhanced measurement logs clicks to
  other domains automatically. When reporting outbound clicks, filter out
  `link_domain = raw.githubusercontent.com` so each download isn't counted twice.
  Outbound clicks stay on so that "Manufacturer product page" clicks are still
  tracked.

The banner and footer link to the Symetrix privacy policy, set by `PRIVACY_URL`
in `index.html`.

## Contents

- `index.html` — the driver library page (hand-written, no build step). Each
  card shows the driver's category, version, minimum supported Cognio Design Ops
  version (`Cognio <minVersion>+`), validation level, and author as badges. When a
  driver's `index.json` entry includes image URLs it shows the brand logo inline
  next to the brand name and the driver screenshot as a clickable thumbnail that
  opens full size in a lightbox.
- `index.json` — machine-readable catalog of released drivers, regenerated on
  each release. Starts empty until the first driver is released. Each entry
  carries the driver's `version` and `minVersion` (the minimum Cognio Design Ops
  version that supports it), `author` (`symetrix` | `manufacturer` |
  `community`; the page adds an Author filter once more than one kind is
  published), and optionally `brandLogoUrl` and `screenshotUrl`
  (with matching `brandLogoPath` / `screenshotPath`), present only when that
  image was shipped — so an imageless driver still renders cleanly. An entry may
  also carry `productUrl`, a link to the manufacturer's product page for the
  3rd-party device, present only when the driver author filled it in; the card
  renders it as a "Manufacturer product page" link.
  Each entry also carries `releaseNotes` — the driver's version history,
  newest first, as `[{ "version": "1.0.1", "date": "2026-12-01", "notes": ["…"] }, …]`.
  The card shows it as a collapsible **Release notes** section with each
  version's publish date (the newest entry is tagged *Latest*); an entry without it renders no section.
- **Linking to a driver.** Every card has an anchor named after the driver's
  file slug, lowercased — e.g.
  `https://drivers.symetrix.co/#shure-ulxd4q` for
  `Drivers/Shure/ULXD4Q/Shure-ULXD4Q.cogdriver`. Opening that link scrolls to
  the card and briefly highlights it (clearing any filters that would hide it).
  Each card's **Copy link** button (shown when you hover over the card)
  puts that URL on the clipboard. The slug
  doesn't change between driver versions, so links stay valid across releases;
  a link to a driver that is no longer listed just opens the full catalog.
- `Drivers/<Brand>/<Product>/` — each released driver's `.cogdriver` bundle and
  `-Info.json` metadata, plus (when provided) the driver screenshot
  `<Slug>.png`. The shared brand logo lives one level up at
  `Drivers/<Brand>/<Brand>.png`. All created and maintained automatically by the
  release pipeline; do not edit by hand.
