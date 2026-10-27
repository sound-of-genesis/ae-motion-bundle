# ae-motion-bundle

The motion layer for the Artist Evolve website (artistevolve.io): one script that runs the falling-collage hero, the scroll beat where the stickers spread into a ring around the brain, auto-advancing feature lists, lines that write themselves on, rendered loops that play only while on screen, sections that rise into place on first view, and a site-wide pause-motion button. It hooks onto `data-ae-*` attributes on plain Webflow markup, so every section still works with no script.

This repository only publishes the built script so a CDN can serve it. The source lives in Artist Evolve's private workspace.

## Files

| File | What it is |
|---|---|
| `dist/ae-site.min.js` | The script the site loads (about 104 KB, about 34 KB gzipped). Includes Matter.js 0.20.0 for the physics |
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

The scroll beat is a section with `data-ae-constellation` holding a stage (`data-ae-constellation-stage`), the brain image (`data-ae-constellation-core`) and the sentence (`data-ae-constellation-text`); the script adds the stickers from the same map. A feature list is `data-ae-features` around items marked `data-ae-feature`, each with a trigger (`data-ae-feature-tab`), a body (`data-ae-feature-body`) and a progress fill (`data-ae-feature-bar`), plus one `data-ae-feature-media` slot per item. A line marked `data-ae-draw` gets `is-drawn` when it comes into view; the page's CSS does the wipe. While motion is allowed and not paused the root element carries `ae-motion-on`.

A video card is a link with `data-ae-video` set to a YouTube id. It shows the thumbnail until clicked, then swaps in the YouTube player (youtube-nocookie.com); with no script the link opens the video on YouTube.

## Rights

The Artist Evolve code and everything about the Artist Evolve brand in this repository are Artist Evolve brand property. All rights reserved; no licence is granted to copy, modify or reuse them. See `LICENSE`. Matter.js keeps its own MIT licence (`NOTICE.md`).
