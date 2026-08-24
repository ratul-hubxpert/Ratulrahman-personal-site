# Ratulrahman-personal-site

Personal site for Ratul Rahman — B2B Growth & RevOps. A single static page, no build
step, no framework. Deployed to Vercel at https://ratulrahman.com.

## Structure

```
index.html      the whole page (inline styles)
img/            photography and logos referenced by the page
og-image.jpg    1200x630 social share card
favicon.svg
robots.txt
sitemap.xml
vercel.json     clean URLs, cache headers for /img, basic security headers
```

## Local preview

```
python3 -m http.server 8000
```

Then open http://localhost:8000.

## Deploying

Vercel builds this as a static site — no framework preset, no build command, output
directory is the repo root. Pushes to `main` deploy to production; any other branch
gets a preview URL.

## Contact form

The contact form is a HubSpot embedded form (portal `26291308`, region `eu1`), using
HubSpot's "developer code" embed so it can be styled to match the page. The theming
lives in the `#hs-contact-form` block in `index.html`.

HubSpot resolves its styles as `var(--hsf-X, var(--hsf-default-X))`, so setting
`--hsf-X` on the wrapper overrides its defaults without `!important`. Structural rules
are prefixed with the `#hs-contact-form` id, because HubSpot injects its own stylesheet
into `<head>` at runtime and would otherwise win on equal specificity.

Note: checkbox variables fall back to the *text input* variables when unset, so
`--hsf-field-checkbox__*` must be set explicitly or checkboxes inherit the underline
border and vertical padding used by the text fields.

Fields, options and the post-submit behaviour are all edited in HubSpot, not here.

## Images

Photos are served at roughly 2x their display size, which is what retina screens need —
they are not oversized. 19 of them are WebP, re-encoded from the originals at quality
0.88 (mean pixel difference ~2/255, visually lossless). Three photos stayed JPEG because
WebP gave no useful saving on them, and the two colour logos were downscaled from 1400px
to 400px, which is where most of the total saving came from.

## Source

Generated from `Ratul Rahman v6 Ledger Color.dc.html`, a Claude Design canvas export.
The canvas version rendered client-side via React + Babel loaded from unpkg; the build
script compiled it to static HTML (props and conditionals resolved, runtime removed).
