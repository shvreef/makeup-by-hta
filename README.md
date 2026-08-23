# Makeup by HTA — website source

This is the source for the site deployed at `roaring-daffodil-aeac06` on Netlify.

## Structure

- `index.html` — the page markup and the site's component code (a `<x-dc>` template
  plus a `<script type="text/x-dc" data-dc-script>` block containing the page's
  logic). This was built with Claude Design, which uses a small custom
  component runtime rather than a build step.
- `js/dc-runtime.js` — the runtime that parses the template above and renders it
  with React. It loads React and ReactDOM from `unpkg.com` at page load
  automatically — no local copies are needed.
- `assets/fonts/` — the Google Fonts (Cormorant Garamond, etc.) used by the
  page, saved locally instead of being fetched from Google Fonts at runtime.
- `assets/images/` — the two photos used on the page.

## Deploying

This is a static site — any static host (Netlify, GitHub Pages, Vercel, etc.)
can serve it as-is. Just point the host at this folder; there's no build step.

## Editing

Content and copy live in the `<x-dc>` block near the top of `index.html`.
Interactive behaviour (state, form handling, etc.) lives in the
`<script type="text/x-dc" data-dc-script>` block near the bottom. Styling is
in the `<style>` block inside the `<helmet>` section at the top of the
`<x-dc>` block.
