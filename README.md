# Zenzen IoT — placeholder landing page

A single-page static site for **zz-iot.org**, built to live on GitHub Pages.

## Files

- `site/index.html` — the page itself (no build step, no Jekyll required)
- `site/CNAME` — domain pointer for GitHub Pages
- `site/404.html` — minimal 404 that matches the page's typography
- `site/.nojekyll` — tells GitHub Pages to serve files as-is (no Jekyll processing)

## Hosting on GitHub Pages

The simplest path:

1. Put the contents of `site/` at the root of your `zz-iot.github.io` repo (or whichever repo you'll publish from).
2. In repo Settings → Pages, set source to the appropriate branch / `/` (root).
3. The `CNAME` file points the deploy at `zz-iot.org`. Add the matching DNS records on your registrar (an `A`/`AAAA` set or `CNAME` to `<user>.github.io`).
4. The `.nojekyll` file disables Jekyll's underscore-folder rules — useful if you ever reference assets in `_assets/` etc.

No build, no dependencies. Edit `index.html` directly.

## Email obfuscation

Three layers, all in `index.html`:

1. The address never appears as a literal string in source — pieces are base64'd and assembled at render.
2. The visible form is the `[at]` / `[dot]` convention (still readable to humans, hostile to naive regex scrapers).
3. The actual `mailto:` is only constructed when the user clicks — and only then is the `@` character produced (via `String.fromCharCode(64)`).

A `<noscript>` fallback shows the obfuscated form for readers without JS.

## Logo

The chevron mark is inline SVG in `index.html`. It also serves as the favicon (also inline, as a data URL). Swap by editing both the masthead `<svg>` and the `<link rel="icon">` data URL.
