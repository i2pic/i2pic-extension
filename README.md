# i2pic — Local Image Converter

> Convert images 100% in your browser. No upload, no signup, no tracking — your files never leave your device.

[Homepage](https://www.i2pic.com) · [Chrome Web Store](#) · [Report an Issue](https://github.com/i2pic/i2pic-extension/issues) · [Privacy Policy](./PRIVACY.md)

![i2pic](./public/icons/icon-128.png)

---

## What is i2pic?

i2pic is a browser extension that brings 17 image format converters into a single toolbar popup. Every conversion runs entirely on your device — no servers, no accounts, no cloud. Your images stay yours.

## Why i2pic?

- **Truly private.** No uploads, no analytics, no remote code. Conversion happens in your browser using WebAssembly, Canvas, and built-in decoders.
- **Works everywhere.** Right-click any image on any website, or hover any image to convert it in place.
- **17 formats in one tool.** HEIC, TIFF, WebP, SVG, EPS, DNG, ICO, JFIF, HTML, MP4 — all in a single popup.
- **Smart about what you click.** The right-click menu auto-detects the source format and only shows the converters that actually apply.
- **Built for real workflows.** Multi-size ICO favicons, multi-page TIFF, transparent WebP, WebP → SVG tracing, ZIP download for multi-frame output.

## Three Ways to Convert

1. **Toolbar icon** — Click the i2pic icon, drop your files, pick a target format, download.
2. **Right-click any image** — The context menu shows only the converters that match the image's format.
3. **Hover any image** — A small badge appears; click it to open a quick-pick of applicable converters for that file type.

## Supported Conversions

| From | To | Input extensions |
|---|---|---|
| HEIC / HEIF | JPG | .heic .heif |
| WebP | JPG, PNG, ICO, PDF, SVG | .webp |
| TIFF / TIF | PNG (multi-page aware) | .tif .tiff |
| JFIF / JPEG | PNG | .jfif .jpg .jpeg |
| ICO | PNG (extracts every frame) | .ico |
| HTML | PNG (full-page render) | .html .htm |
| EPS | PNG | .eps .ps |
| SVG | JPG | .svg .svgz |
| DNG | JPG | .dng |
| MP4 / MOV / WebM | WebP (first-frame thumbnail) | .mp4 .m4v .webm .mov |
| WebP / JPG | Compress (same format, smaller size) | .webp .jpg .jpeg |
| HEIC | Preview (HEIC Viewer) | .heic .heif |

## Install

### From the Chrome Web Store (recommended)

Install in one click from the Chrome Web Store (link at the top of this README once published).

### Load as an unpacked extension (for testing)

1. Open Chrome → `chrome://extensions`
2. Toggle **Developer mode** on
3. Click **Load unpacked** → select the `dist/` folder
4. The i2pic icon appears in your toolbar

Step-by-step guide: [LOAD-EXTENSION.md](./LOAD-EXTENSION.md)

## Browser Support

- Chrome 116+
- Edge 116+
- Arc, Brave, Opera, Vivaldi (any Chromium 116+)

Firefox and Safari are not supported at this time.

## Privacy

i2pic does not collect, transmit, or store any user data. All image processing happens locally in your browser. Read the full policy: [PRIVACY.md](./PRIVACY.md)

## Contact

- **Homepage:** [www.i2pic.com](https://www.i2pic.com)
- **Issues:** [github.com/i2pic/i2pic-extension/issues](https://github.com/i2pic/i2pic-extension/issues)
- **Email:** support@i2pic.com

## License

MIT License © 2026 [i2pic](https://www.i2pic.com). See [LICENSE](./LICENSE) for details.
