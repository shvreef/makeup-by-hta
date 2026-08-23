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
- `assets/images/` — the photos used on the page. CMS uploads land in
  `assets/images/uploads/`.
- `assets/favicon.svg` — the circled "h" mark from the nav, as the browser icon.
- `content/site.json` — every image path on the site, plus the Recent looks and
  portfolio entries. The page fetches this at load, so editing it changes the
  site without touching `index.html`.
- `admin/` — the Decap CMS editor (see "Editing content" below).
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

## Editing content (the CMS)

Go to <https://roaring-daffodil-aeac06.netlify.app/admin/> and log in with
GitHub. Every photo on the site is editable there: the homepage hero, the two
"artist" photos, the three service cards, the portfolio grid, and the Recent
looks row. Saving commits `content/site.json` (plus any uploaded images) to
`main`, which deploys automatically.

- Uploaded images land in `assets/images/uploads/`.
- **Hero focus** — the hero is cropped differently on each device: short and wide
  on desktop, narrow and tall on a phone (where only about 60% of the image's
  width fits). The two "Focus" numbers say which part to keep. Because the photo
  is landscape, desktop is width-constrained so only *down* bites there, and a
  phone is height-constrained so only *across* bites. Point *across* at the face
  after swapping the hero photo.
- Any image slot left empty falls back to the striped placeholder, so the
  layout never collapses.
- Recent looks shows the first 5 photos, newest first. The whole section hides
  itself when the list is empty.
- **Logging in requires the GitHub OAuth provider to be configured once** on the
  Netlify project, under Project configuration → Access control → OAuth.

The runtime seeds its own copy of the defaults and deep-merges the fetched file
over them, so a missing or half-written `content/site.json` degrades to the
built-in content rather than blanking a section.

## Contact form

The enquiry form posts to Netlify Forms. Submissions appear under Forms in the
Netlify dashboard and are emailed to the address configured there (Forms →
Settings and usage → Form notifications).

The hidden `<form name="contact">` at the bottom of `index.html` is what Netlify
parses at deploy time to register the field names — the visible form is rendered
by React, which Netlify's build-time scan cannot see, so **that static twin must
stay in place**. Spam is filtered with a `bot-field` honeypot.

## Editing markup

Content and copy live in the `<x-dc>` block near the top of `index.html`.
Interactive behaviour (state, form handling, etc.) lives in the
`<script type="text/x-dc" data-dc-script>` block near the bottom. Styling is
in the `<style>` block inside the `<helmet>` section at the top of the
`<x-dc>` block. The page `<title>`, meta description and favicon links are in
the real `<head>` at the very top of the file.
