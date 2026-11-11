# ae-motion-bundle

The motion layer for the Artist Evolve website (artistevolve.io): one script that runs the falling-collage hero, the scroll beat where the stickers spread into a ring around the brain, auto-advancing feature lists, lines that write themselves on, rendered loops that play only while on screen, sections that rise into place on first view, and a site-wide pause-motion button. Since v0.3.0 it also runs the hero's title (letters that drop in, a chrome sheen, letters that swell near the pointer, a rotating last word), a dot field and a marker-dot cursor under the pointer, figures that count up, a halftone photo, a peelable sticker, and a feature list's media as a pile of paper cards that arrive through dots. Since v0.3.1 it can also turn a form into one field at a time. It hooks onto `data-ae-*` attributes on plain Webflow markup, so every section still works with no script.

This repository only publishes the built script so a CDN can serve it. The source lives in Artist Evolve's private workspace.

## Files

| File | What it is |
|---|---|
| `dist/ae-site.min.js` | The script the site loads (about 154 KB, about 52 KB gzipped). Includes Matter.js 0.20.0 for the physics and code adapted from React Bits |
| `NOTICE.md` | Third-party notices: Matter.js (MIT) and React Bits (MIT + Commons Clause) |

From v0.3.0 only the minified build is published. Tags up to v0.2.1 also carry a readable `dist/ae-site.js`.

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

Since v0.3.0: `data-ae-count` on a figure counts it up on first view; `data-ae-halftone` on a photo's wrapper prints it as halftone (with `-cell`, `-lift`, `-contrast`); `img[data-ae-peel]` (with `data-ae-peel-rotate`) is a sticker to peel and throw inside its parent; on a title line, `data-ae-letters` drops the letters in, `data-ae-sheen` sweeps a sheen across them and `data-ae-swell` swells them near the pointer; `data-ae-rotate="a|b|c"` cycles a line's last word (the line's own word stays the real copy); on a section, `data-ae-dots` wakes its dot grid under the pointer and `data-ae-blob` adds a three-dot cursor; on a feature list's media panel, `data-ae-deck` piles the media as paper cards and `data-ae-dissolve` brings each one in through dots. The page's head code carries the few CSS rules these need. With motion off (reduced motion, low power, or the pause button) each is the plain HTML.

Since v0.3.1: `data-ae-steps` on a `<form>` asks one field at a time (a row of dots, Back and Next, Enter moves on, each field checked before the next shows) and shows the form's own submit button on the last step, so the form posts exactly as before. Without the script every field shows.

A video card is a link with `data-ae-video` set to a YouTube id. It shows the thumbnail until clicked, then swaps in the YouTube player (youtube-nocookie.com); with no script the link opens the video on YouTube.

## Rights

The Artist Evolve code and everything about the Artist Evolve brand in this repository are Artist Evolve brand property. All rights reserved; no licence is granted to copy, modify or reuse them. See `LICENSE`. Matter.js keeps its own MIT licence, and the code adapted from React Bits keeps its MIT + Commons Clause licence (`NOTICE.md`).
