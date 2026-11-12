# Selfie Poster Studio

A single-page web app that fits a selfie into a social-media poster. Upload or take a photo, drag and zoom it into place, edit the text, pick a template and download a PNG.

Everything runs in the browser. Photos are never uploaded anywhere.

## Features

- 4 templates: Night Market, Block Party, Sunrise, Gallery Label
- 3 photo shapes: circle, arch, square
- 6 accent colors
- 3 export sizes: 1080x1080 (square), 1080x1350 (portrait 4:5), 1080x1920 (story 9:16)
- Drag to move the photo, scroll or pinch to zoom, drop an image onto the poster
- Headline, tag line, name and details fields update the poster live
- Light and dark interface

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

## Customize

All code lives in `index.html`.

- **Templates**: the `tplNight`, `tplBlock`, `tplSun` and `tplGallery` functions draw each poster on a canvas. Add a new function and register it in the `TEMPLATES` object, then add a button with a matching `data-val` in the Template group.
- **Accent colors**: edit the `ACCENTS` array.
- **Sizes**: edit the `SIZES` object and the Size buttons.
- **Default text**: edit the `state` object near the top of the script.

## Notes

- Fonts (Archivo and Big Shoulders Display) load from Google Fonts. If they are blocked, the app falls back to system fonts.
- The Take selfie button opens the front camera on phones. On desktop it opens a file picker.

## License

MIT. See `LICENSE`.
