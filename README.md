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
