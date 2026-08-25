# Load the unpacked extension (Chrome / Edge / Arc)

1. Install & build:
   ```bash
   pnpm install
   pnpm build
   ```
2. Open `chrome://extensions` (or `edge://extensions`).
3. Toggle **Developer mode** on.
4. Click **Load unpacked** → select this folder's `dist/` directory.
5. Pin the i2pic icon from the toolbar.

## Dev loop

Run `pnpm dev` (watch build), then click the reload button on the
extension's card in `chrome://extensions` after each change.

## What the extension does

- **Popup (toolbar icon)** — pick a converter, drop files, convert, download
  individually or as a ZIP.
- **Right-click an image on any page** → convert it with any tool listed.
- **Floating button on image hover** → opens a small picker of all 17 tools.
- 17 tools shared with i2pic.com website core; all conversion happens 100%
  locally in your browser (no upload, no signup, no server).
