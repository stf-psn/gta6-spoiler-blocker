# gta6-spoiler-blocker

Bookmarklet that blurs GTA VI spoilers on the current page. Built for Samsung Internet (no userscript support), works in any mobile/desktop browser that runs `javascript:` bookmarks.

## Install (Samsung Internet)

1. Bookmark any page.
2. Bookmarks → long-press it → **Edit**.
3. Name: `NoSpoilerGTA`. URL: paste the whole content of [`bookmarklet.txt`](bookmarklet.txt).
4. On a page, open Bookmarks and tap it (or type `NoSpoilerGTA` in the address bar and pick the suggestion).

Tap again to turn it off. Tap a blurred item to reveal it.

## How it works

- **`KW`** (game terms: GTA, GTA 6/VI, Vice City, Leonida, Lucia, Jason, Rockstar…): always blurred.
- **`SP_IT_EN`** (spoiler words in Italian and English: finale/ending, tradimento/betrayal, morte/death, colpo di scena/plot twist…): blurred on every page while `SEMPRE=true`; set `SEMPRE=false` to apply them only on GTA-related pages.
- Blurs the whole card (YouTube, Reddit, X, articles, list items), falls back to the paragraph/heading.
- Checks text, image `alt`, `title`, `aria-label`; keeps watching for content loaded on scroll.

## Limits

- Must be tapped on each page load (bookmarklets can't auto-run).
- Spoilers only inside images/videos with no matching text aren't detected.
- Aggressive by design: lots of false positives with `SEMPRE=true`.

## Development

Edit `src.js`, then regenerate the bookmarklet:

```sh
node -e 'const fs=require("fs");fs.writeFileSync("bookmarklet.txt","javascript:"+fs.readFileSync("src.js","utf8").split("\n").map(l=>l.trim()).join("")+"\n")'
```

`src.js` must not contain `//` comments (the build joins lines).
