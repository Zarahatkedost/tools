# Sahil's tools — tools.sahilshaikh.org

27 free, 100% client-side tools. No server, no database, nothing leaves the visitor's device. Hosted as static files on Cloudflare Pages.

## Structure

```
index.html            <- the hub / homepage (search + category groups)
<tool-name>/index.html   <- one folder per tool -> clean URL /<tool-name>/
```

## The 27 tools

Make & share: qr-generator, contact-card, scanner, poster-maker
PDF: pdf-toolkit
Images: image-compressor, background-remover, exif-remover
Text: text-studio, email-validator
Converters: unit-converter, color-studio, encoder-decoder, data-converters, csv-json, phone-formatter
Developer: dev-tools, crypto-id, markdown-html, password-strength
Calculators: shipping-calculator, petty-cash, math-studio, invoice-generator, expense-splitter
Time: world-clock, timers-studio

## How to add a new tool

1. Create a folder, e.g. `word-counter/`, put the tool HTML in it as `index.html`.
2. Open the root `index.html`, find `var TOOLS = [ ... ]` near the top of the script.
3. Add one line:
   {title:"Word counter", desc:"Live word counts.", cat:"text", path:"/word-counter/", icon:"type", live:true},
   - cat: make, pdf, image, text, convert, dev, calc, time
   - icon: a key from the IC object (or add a new one)
   - live:false shows a greyed "soon" card instead
4. Commit + push. Cloudflare Pages redeploys automatically.

## Deploy (first time)

1. Create a GitHub repo and push the CONTENTS of this folder (index.html at repo root).
2. Cloudflare dashboard -> Workers & Pages -> Create -> Pages -> Connect to Git.
3. Pick the repo. Leave build command and output directory BLANK (raw static HTML).
4. Save and Deploy.
5. Custom domains tab -> add tools.sahilshaikh.org (Cloudflare adds DNS automatically).

## Testing notes

Some tools only fully work over HTTPS (i.e., once deployed, not from a local file):
- scanner: camera needs HTTPS (image-upload mode works locally)
- background-remover: loads its AI model from a hosted origin
- contact-card: share links build from the page URL, so they need the real domain

Petty cash tracker: entries live in the browser only - export CSV/PDF before closing the tab.
