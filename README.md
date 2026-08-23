# Makeup by HTA — website source

This is the source for the site deployed at `roaring-daffodil-aeac06` on Netlify:
<https://roaring-daffodil-aeac06.netlify.app>

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
- `assets/favicon.svg` — the circled "h" mark from the nav, as the browser icon.
- `serve.js` — a dependency-free local preview server.
- `netlify.toml` — Netlify build config (publish this folder, no build step).

## Previewing locally

```
node serve.js
```

Then open <http://localhost:4321>. Pass a port to use a different one
(`node serve.js 8080`). Requires Node; there is nothing to install.

## Deploying

This is a static site — there is no build step. Netlify is linked to the
`main` branch of <https://github.com/shvreef/makeup-by-hta>, so **pushing to
`main` triggers a deploy automatically**. Watch progress under Deploys in the
Netlify dashboard.

Any other static host (GitHub Pages, Vercel, …) can serve the folder as-is.

## Editing

Content and copy live in the `<x-dc>` block near the top of `index.html`.
Interactive behaviour (state, form handling, etc.) lives in the
`<script type="text/x-dc" data-dc-script>` block near the bottom. Styling is
in the `<style>` block inside the `<helmet>` section at the top of the
`<x-dc>` block. The page `<title>`, meta description and favicon links are in
the real `<head>` at the very top of the file.
