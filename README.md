# Agency Platform

Static site. No build step, no dependencies.

## Layout

    index.html                        the site root — copy of v1-indigo.html
    v3-ironwood-green.html            full platform, current design
    v1-indigo.html                    full platform, indigo design
    v2-noir-gold.html                 full platform, dark/gold design
    v1-*.html                         one module per file, indigo design
    docs/                             every PDF the platform references (54 files) + manifest.json
    .nojekyll                         tells GitHub Pages to serve files as-is

## Deploying to GitHub Pages

1. Upload the **contents** of this folder to the repo root — not the folder
   itself, and not a .zip. `index.html` must sit at the top level.
2. Settings -> Pages -> Source: your branch, folder `/ (root)`.
3. Wait for the green check in the Actions tab.

## Rules

Keep every HTML file in the same folder as `docs/`. Each page links to
documents by relative path (`docs/<file>.pdf`); the PDF bytes are not
inside the HTML.

Filenames use lowercase and hyphens. Spaces in filenames become `%20` in
URLs and are a common source of broken links on static hosts — keep new
files in the same style.

To change which design is the landing page, copy the version you want
over `index.html`.

To add a document: drop the PDF into `docs/`, then add one line to the
matching store in the HTML (FARMERS_DECS, RETAIL_DOCS, or the DEC/BINDER/
WC_INFO/COI stores in the client view):

    "policy-id": { fileName:"My-Dec.pdf", url:"docs/My-Dec.pdf" }

`docs/manifest.json` lists every file with its size and SHA-256 — the seed
for a documents table once a backend exists, at which point `url:` becomes
a signed link from object storage and the folder goes away.
