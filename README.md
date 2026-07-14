# PUB Viewer

A **single-file, best-effort** Microsoft Publisher (`.pub`) viewer. Publisher's
format is proprietary and undocumented, so this doesn't reconstruct the page
layout — instead it reads the file's **document metadata and text** so you can
see what's inside. It's a **viewer** — no accounts, no uploads. Everything runs
locally in your browser.

🔗 **Live:** <https://pub-viewer.us/>

![Single file](https://img.shields.io/badge/build-single%20HTML%20file-success) ![No build step](https://img.shields.io/badge/build%20step-none-success) ![License](https://img.shields.io/badge/license-MIT-blue)

> Part of the **[File Viewer](https://file-viewer.us/) family** — HTML, Markdown,
> ePUB, PDF, Data, DOCX, Sheets, EML, PPTX, Log, Cert, and PUB each have their
> own dedicated viewer. Use the **☰ menu** in the header to jump between them.

## What it can (and can't) do

Microsoft Publisher `.pub` files are **OLE/Compound-File** binaries in a closed,
undocumented format. There is no reliable way to reproduce their layout, images,
or fonts in a browser. So this viewer is **honest about being best-effort**:

- ✅ **Document metadata** — Title, Author, Subject, Keywords, Company, created /
  last-saved dates, and page / word / character counts, read from the file's
  `SummaryInformation` / `DocumentSummaryInformation` property sets.
- ✅ **Extracted text** — the readable text recovered from the document's streams.
- ❌ **Not** the page layout, images, colors, or fonts. For a faithful copy,
  open the file in Publisher and **Save As → PDF** (then read it in
  [pdf-viewer.us](https://pdf-viewer.us/)).

## Features

- 🪶 **One file, no build, no dependencies** — works offline, even from `file://`.
- ☰ **Family menu** · 🫥 **auto-hiding header** · 🎨 **pick any background color**.
- 🔒 **Local only** — your files never leave your device.
- 📊 **Privacy-friendly analytics** — self-hosted, cookieless [Plausible](https://plausible.io/).

## Supported file types

`.pub` (Microsoft Publisher). The same OLE parser also reads metadata from other
Compound-File documents, but those have dedicated viewers elsewhere in the family.

## Quick start

**Just open it.** Download [`index.html`](index.html), double-click it — no
server, no build, no internet needed.

```sh
python3 -m http.server 8080   # then open http://localhost:8080
```

## Deploy to Cloudflare Pages

Connect the repo (**Workers & Pages → Create → Pages → Connect to Git**),
framework preset **None**, build command blank, output directory `/`. The
[`_headers`](_headers) file applies a strict CSP automatically. Add the custom
domain **pub-viewer.us** under the project's Custom domains tab.

## How it works

Everything is in [`index.html`](index.html) — **no third-party libraries.** A
small reader (written for this project) detects the OLE/Compound-File container,
locates the `SummaryInformation` property set by its format GUID and parses the
property values, and scans the document's streams for readable UTF-16 / ASCII
text. The viewer's CSP stays strict (`default-src 'none'`, no external assets).

## Credits

No bundled libraries — the OLE / property-set reader is original to this project.
The icon is by the author. Analytics by [Plausible](https://plausible.io/).

## License

[MIT](LICENSE) © 2026 Michal Ferber, aka **TechGuyWithABeard**.
