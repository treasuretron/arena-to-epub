# I VIBECODED THIS
and did not check the code. Yolo. Run at your own risk. Works on my machine. Yes you could have vibe coded it yourself but I figured I'd save you the tokens :)

Claude sez, with some of my edits:

# Are.na to EPUB

A single-page, client-side tool that converts an [Are.na](https://www.are.na) channel into an EPUB file optimized for Xteink X3 e-readers.

Paste in a channel URL, hit Generate, and get a downloadable EPUB. No server required (beyond serving the HTML file itself).

## What it does

- **Image blocks** are resized to fit 528x792 (XTEINK X3 screen resolution), automatically rotated 90 degrees if that would make them larger on screen, converted to grayscale, and [Atkinson dithered](https://en.wikipedia.org/wiki/Atkinson_dithering) to 1-bit black and white.
- **Text blocks** are rendered as XHTML pages. The e-reader handles pagination.
- **Link blocks** become a composite page: the cached preview image, the link title, and a QR code pointing to the URL.
- **Media blocks** (YouTube, Vimeo, etc.) get the same treatment: poster frame, title, and a scannable QR code to the video.
- **Attachments** (PDFs, etc.) are skipped.

## Usage

The page needs to be served over HTTP (not opened as a `file://` URL) because it fetches from the Are.na API.

**Option 1: Local server**

```sh
cd arena-to-epub
python3 -m http.server 8080
# open http://localhost:8080
```

**Option 2: Host it**

Upload `index.html` to any static host (GitHub Pages, Netlify, your own server, etc.). It's a single file with no build step -- just CDN dependencies (JSZip, FileSaver.js, qrcode-generator).

Then paste a public Are.na channel URL and click Generate.

## Limitations

- Only works with **public** channels (the Are.na API returns 404 for private ones).
- If the Are.na image CDN or a CORS proxy is down, some images may be skipped.
- Very large channels (500+ blocks) will work but take a while -- images are processed sequentially to keep memory usage bounded.

## Credits

Atkinson dithering algorithm ported from [hyperdither](https://github.com/mildmojo/hyperdither).

## License

MIT
