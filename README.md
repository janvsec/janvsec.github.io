# janvojvoda.tech

Personal portfolio of Ján Vojvoda (janvsec). Plain HTML, CSS and JavaScript – no build step, no dependencies – hosted on GitHub Pages.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole site: markup, styles and script |
| `404.html` | Shown by GitHub Pages for unknown URLs |
| `pgp.asc` | Public PGP key, linked from the contact section |
| `og-image.png` | Social preview image (LinkedIn, Discord, X, …) |
| `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` | Browser and home-screen icons |
| `robots.txt`, `sitemap.xml` | For search engines |
| `CNAME` | Custom domain for GitHub Pages – keep this file |
| `img/` | Your photos for the Talks & media section (create it when you add the first one) |

## Editing content

Everything below is in `index.html`.

**Texts.** Slovak text is written directly in the HTML. Every translatable element has a `data-key` attribute, and its English version lives in `T.en` in the script at the bottom of the file. Edit Slovak in the HTML, English in `T.en`.

**Add a project.** Copy one `<a class="proj">…</a>` block in the Projects section, change the link, name and stack, give the category and description new keys (for example `pc7` and `p7`) and add those keys to `T.en`.

**Add a certificate.** Copy a row in the Certifications list. Use `<a class="cert" href="…">` when it can be verified online and `<div class="cert">` when it can't. The counts above the list update automatically.

**CTF results.** `CONFIG.ctf.solves` lists every solve. The points total, solve count, chart, category breakdown and table are all calculated from it. The rank (`#41`) and success rate are typed in the HTML.

**TryHackMe numbers.** Typed in the HTML (Results section). When you update them, also change the "as of" month next to them (`data-month="YYYY-MM"`).

**Hackathons and other CTFs.** Copy a `<div class="comp">` row in the Results section. Use `class="badge hot"` (red) for a podium place and plain `class="badge"` otherwise. Add the English description to `T.en`.

**Talks and media.** The talk is the `<article class="talk">` block; events and articles are cards in the grid below it. A card that links somewhere is `<a class="proj" href="…">`, one without a link is `<article class="proj">`. Add new English texts to `T.en`.

**Photos.** Every talk/event card has an empty photo slot: `<img src="" …>`. Put the picture next to `index.html` (for example `img/nehejtujem-2026.jpg`) and fill in `src="img/nehejtujem-2026.jpg"`. While `src` is empty, or the file can't be found, the slot stays hidden. Use landscape photos around 1600×1000 px and keep them under ~300 KB (JPG or WebP). The `alt` text describes the photo for screen readers; its English version is the `data-key-alt` key in `T.en`.

**Globe.** `CONFIG.globe` sets the home location and its label, the rotation speed and tilt, how often attacks fire, the share aimed at home (always blocked) and the list of cities.

**Colours.** The CSS variables at the top of the `<style>` block: `--red` (primary, attacks) and `--blue` (secondary, defense). The canvas animations read them too, so changing them recolours everything.

**Footer wordmark.** `CONFIG.wordmark.text`. If you change it, also change `text=` in the Unbounded font link in `<head>`, because that font file only contains those letters.

**Default language.** `CONFIG.defaultLang`. The English version is always available at `/?lang=en`.

## SEO checklist

- **Domain changes:** update `<link rel="canonical">`, the `hreflang` links, `og:url`, `og:image`, `twitter:image`, the JSON-LD block, `robots.txt`, `sitemap.xml` and `CNAME`.
- **Bigger content updates:** change `<lastmod>` in `sitemap.xml`.
- **New look:** regenerate `og-image.png`. Run this in the site folder (it uses Microsoft Edge in headless mode and the page's built-in `?og` card layout):

```powershell
& "${env:ProgramFiles(x86)}\Microsoft\Edge\Application\msedge.exe" --headless=new --disable-gpu --hide-scrollbars --force-device-scale-factor=1 --window-size=1200,630 --virtual-time-budget=10000 --user-data-dir="$env:TEMP\edge-og" --screenshot="$PWD\og-image.png" "file:///$($PWD -replace '\\','/')/index.html?og&lang=en"
```

## Performance

The animations only run while they are on screen and the tab is active. The page measures how long each frame takes and steps down automatically on slow devices (fewer characters, lower frame rate, and finally a still image). With "reduce motion" or data saver turned on, it shows a still image from the start.
