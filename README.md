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

## Contents

- `index.html` — the driver library page (hand-written, no build step).
- `index.json` — machine-readable catalog of released drivers, regenerated on
  each release. Starts empty until the first driver is released.
- `Drivers/<Brand>/<Product>/` — each released driver's `.cogdriver` bundle and
  `-Info.json` metadata. Created and maintained automatically by the release
  pipeline; do not edit by hand.
