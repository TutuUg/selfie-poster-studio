# Gutsy Poster Studio

A single-page web app for the Gutsy Half Marathon 2027. Runners add a selfie, drag and zoom it into a branded poster, enter their name and download a PNG to share on social media. Every poster carries the official event footer with the date, venue, race fee and a QR code.

Everything runs in the browser. Photos are never uploaded anywhere.

## Features

- Gutsy Half Marathon 2027 logo built into every poster
- Fixed event footer card with tab text, date, venue, race fee and a QR code (not editable on the page)
- Runner's name shown on a label over the photo
- 4 templates: Night Market, Block Party, Sunrise, Gallery Label
- 3 photo shapes: circle, arch, square
- 6 accent colors, starting with Gutsy blue
- 3 export sizes: 1080x1080 (square), 1080x1350 (portrait 4:5), 1080x1920 (story 9:16)
- Drag to move the photo, scroll or pinch to zoom, or drop an image onto the poster
- The logo takes each template's text color so it stays readable. A checkbox keeps its original blue instead.
- Light and dark interface

## Files

- `index.html`: the whole app, including the embedded logo and QR code library
- `gutsy-logo.png`: the trimmed, transparent logo used by the app (kept here for reference)
- `README.md`, `LICENSE`

## Run locally

No build step. Open `index.html` in a browser.

To serve it from a local web server instead:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Publish with GitHub Pages

1. Push this repo to GitHub as a **public** repository.
2. Go to **Settings > Pages**.
3. Under **Build and deployment**, set Source to **Deploy from a branch**, Branch to `main`, folder `/ (root)`, then Save.
4. After a minute the site is live at `https://<your-username>.github.io/<repo-name>/`.

After you push an update, GitHub Pages redeploys on its own within a minute or two. Do a hard refresh to see the change.

## Change the event details

The footer values are the defaults in the `state` object near the top of the script in `index.html`:

```js
date: '23 JAN 2027', venue: 'Metroplex Naalya', fee: 'UGX 70,000',
tagline: 'Chase your best.', qrUrl: 'https://bit.ly/3X5L7Cn',
```

Edit those values and push. The footer is fixed on the page: there are no controls for it, so runners cannot change it. The QR code is generated in the browser from `qrUrl`. Set `qrUrl` to an empty string `''` to hide the QR code.

## Customize

All code lives in `index.html`.

- **Other defaults**: `kicker` (top line) and `name` are in the same `state` object.
- **Accent colors**: edit the `ACCENTS` array. The first entry is the default.
- **Footer colors**: edit `NAVY`, `ORANGE` and `BLUE` above the footer code.
- **Footer layout**: the `drawFooter` function draws the card. Column positions are the fractions in the `colDate`, `colVenue`, `colFee` and `divX` lines.
- **Templates**: the `tplNight`, `tplBlock`, `tplSun` and `tplGallery` functions draw each poster on a canvas. Add a new function, register it in the `TEMPLATES` object, and add a button with a matching `data-val` in the Template group.
- **Sizes**: edit the `SIZES` object and the Size buttons.

### Change the logo

The logo is embedded as a base64 string so the page works as a single file and the Download button works when opened locally.

1. Export a PNG with a transparent background, trimmed of empty margins, about 1600 px wide.
2. Convert it to base64:
   - macOS: `base64 -i logo.png | tr -d '\n'`
   - Linux: `base64 -w0 logo.png`
3. In `index.html`, find the line starting with `logo.src = 'data:image/png;base64,` and replace everything after `base64,` up to the closing quote with the new string.

The recoloring feature turns the logo into a single-color shape. If your new logo has several colors, set `origLogo: true` in the `state` object so it keeps its own colors.

The small runner icon in the middle of the QR code is a second embedded image, set on the line starting with `icon.src = 'data:image/png;base64,`.

## Notes

- Fonts (Archivo, Big Shoulders Display and Montserrat) load from Google Fonts. If they are blocked, the app falls back to system fonts.
- The QR code uses the MIT-licensed `qrcode-generator` library by Kazuhiko Arase, included inline in `index.html`.
- The Take selfie button opens the front camera on phones. On desktop it opens a file picker.

## License

MIT. See `LICENSE`.
