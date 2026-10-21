# ae-motion-bundle

The motion layer for the Artist Evolve website (artistevolve.io): one script that runs the falling-collage hero, plays rendered loops only while they are on screen, raises sections into place on first view, and shows a site-wide pause-motion button. It hooks onto `data-ae-*` attributes on plain Webflow markup, so every section still works with no script.

This repository only publishes the built script so a CDN can serve it. The source lives in Artist Evolve's private workspace.

## Files

| File | What it is |
|---|---|
| `dist/ae-site.min.js` | The script the site loads (about 95 KB, about 32 KB gzipped). Includes Matter.js 0.20.0 for the physics |
| `dist/ae-site.js` | The same build, not minified, for reading |
| `NOTICE.md` | Third-party notice for Matter.js (MIT) |

No images, video or fonts are in this repository. The collage stickers and the loops are served from the site's own asset host.

## Loading it

Always load a tagged version, never a branch:

```
https://cdn.jsdelivr.net/gh/sound-of-genesis/ae-motion-bundle@<tag>/dist/ae-site.min.js
```

The page tells the script where the stickers are with a map from sticker file name to full URL, set before the script runs:

```html
<script>window.AE_STICKER_URLS = { "brain-420.webp": "https://...", "brain-260.webp": "https://..." };</script>
```

Without the map, stickers load from `<data-ae-assets>stickers/<file>` (default `assets/`).

## Rights

The Artist Evolve code and everything about the Artist Evolve brand in this repository are Artist Evolve brand property. All rights reserved; no licence is granted to copy, modify or reuse them. See `LICENSE`. Matter.js keeps its own MIT licence (`NOTICE.md`).
