# Privacy Policy — i2pic — Local Image Converter

**Last updated: 2026-08-25**

i2pic is a browser extension that converts images **100% locally on your
device**. This policy explains, in plain language, what data we touch and
what we never touch.

## TL;DR

- We **do not collect** any personal data.
- We **do not transmit** your images or file names anywhere.
- All conversion happens in your browser via WebAssembly, Canvas, and
  built-in decoders.
- No analytics, no tracking, no remote scripts.

## What data the extension processes

| Data | Where it lives | How it's used | Where it goes |
|---|---|---|---|
| Image bytes you drop / right-click | In-memory, current tab | Fed to local decoders and encoders | **Nowhere** — discarded when you close the popup |
| File name of the image | In-memory, current tab | Used to label the converted output file | **Nowhere** |
| `img.src` URL string of images you hover or right-click | In-memory, current tab | Used to detect the file type and pass to the converter | **Nowhere** |
| Last-used converter slug (`lastSlug`) | `chrome.storage.local` on your device | Reopens the popup on the same tool next time | **Nowhere** — never synced, never sent |

## What permissions we ask for and why

- **`contextMenus`** — Adds "Convert with i2pic" entries to the right-click
  menu on images. The menu is built once at install time. No browsing data
  is read.
- **`downloads`** — Saves the converted file(s) to your Downloads folder.
  The bytes saved are produced locally; no remote URLs are fetched.
- **`storage`** — Stores a single preference (the last converter you used)
  in `chrome.storage.local`, plus transient pending-image metadata in
  `chrome.storage.session` (cleared when the browser closes).
- **`offscreen`** — Reserved for offloading heavy decoders (e.g. HEIC / TIFF)
  into a hidden offscreen document so they don't block the popup UI. The
  offscreen document only receives file bytes already in memory.
- **`host_permissions: <all_urls>`** — Lets the content script detect
  images on whatever page you're browsing so the hover badge and right-click
  menu work everywhere. We read only `img.src` strings — no page content is
  sent anywhere.

## What we **never** do

- ❌ Upload your images to any server
- ❌ Send file names, paths, or URLs to any server
- ❌ Track your browsing history
- ❌ Use analytics, fingerprinting, or advertising SDKs
- ❌ Load remote code at runtime
- ❌ Request authentication or sign-in
- ❌ Sell or share any data with third parties

## Third-party libraries (all bundled, all client-side)

The extension ships these open-source libraries inside its package — they
run locally and never make network requests:

- `heic2any` — HEIC/HEIF → JPG/PNG decoding
- `utif` — TIFF decoding
- `imagetracerjs` — bitmap → SVG vector tracing
- `modern-screenshot` — HTML → PNG rendering
- `fflate` — ZIP packaging for multi-file downloads
- `lucide-react`, `sonner`, `clsx`, `tailwind-merge` — UI helpers

No remote code is loaded. The Chrome Web Store "Remote code" attestation
is answered **No**.

## Children's privacy

The extension does not collect any data from anyone, including children
under 13. No age-gated content is involved.

## Changes to this policy

Material changes will be posted in this file with an updated date. The
extension itself does not need to update for this policy to change.

## Contact

- **Support:** [github.com/haskx/i2pic-extension/issues](https://github.com/haskx/i2pic-extension/issues)
- **Email:** support@i2pic.com
- **Homepage:** [www.i2pic.com](https://www.i2pic.com)
