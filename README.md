# cognio-drivers-public

Public repository for completed Cognio device drivers.

## Driver library website

`index.html` is a self-contained, dependency-free page that lists every
released driver and lets you filter by manufacturer, category, and validation
level. It reads `index.json` (regenerated automatically by the release pipeline
in the private `cognio-drivers` repo) and links to each driver's `.cogdriver`
download.

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
- Every **Download** click sends a `file_download` event with `driver_brand`,
  `driver_product` and `driver_version`. Register those three as event-scoped
  custom dimensions in GA Admin to report on them.

Set `PRIVACY_URL` in `index.html` to show a privacy-policy link in the banner and
footer.

## Contents

- `index.html` — the driver library page (hand-written, no build step). Each
  card shows the driver's category, version, minimum supported Cognio Design Ops
  version (`Cognio <minVersion>+`), and validation level as badges. When a
  driver's `index.json` entry includes image URLs it shows the brand logo inline
  next to the brand name and the driver screenshot as a clickable thumbnail that
  opens full size in a lightbox.
- `index.json` — machine-readable catalog of released drivers, regenerated on
  each release. Starts empty until the first driver is released. Each entry
  carries the driver's `version` and `minVersion` (the minimum Cognio Design Ops
  version that supports it), and optionally `brandLogoUrl` and `screenshotUrl`
  (with matching `brandLogoPath` / `screenshotPath`), present only when that
  image was shipped — so an imageless driver still renders cleanly. An entry may
  also carry `productUrl`, a link to the manufacturer's product page for the
  3rd-party device, present only when the driver author filled it in; the card
  renders it as a "Manufacturer product page" link.
- `Drivers/<Brand>/<Product>/` — each released driver's `.cogdriver` bundle and
  `-Info.json` metadata, plus (when provided) the driver screenshot
  `<Slug>.png`. The shared brand logo lives one level up at
  `Drivers/<Brand>/<Brand>.png`. All created and maintained automatically by the
  release pipeline; do not edit by hand.
