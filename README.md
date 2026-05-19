# MD Forge
<img width="3731" height="1053" alt="image" src="https://github.com/user-attachments/assets/63804023-0047-4baa-becf-360958598857" />

A dual-pane Markdown editor that runs entirely in the browser — no build step, no dependencies to install.

## Features

- **Open & Save** `.md` files directly from/to disk via the File System Access API
- **Live dual-pane sync** — edit raw Markdown on the left, see rendered HTML on the right (and vice-versa)
- **Editable preview** — click anywhere in the right pane to edit rendered content; changes sync back to Markdown automatically
- **WYSIWYG controls** — format preview text with headings, bold, italic, lists, quotes, code blocks, and links
- **Copy for Confluence** — copies rich HTML to the clipboard so tables, headings, and code blocks paste cleanly into Confluence
- **Copy for Word** — copies Word-friendly rich HTML with document styling for cleaner paste results
- **Drag-to-resize** the split between panes
- `Cmd/Ctrl+S` to save, `Cmd/Ctrl+O` to open

## Tech

| Library | Purpose |
|---|---|
| [marked.js](https://github.com/markedjs/marked) v9 | Markdown → HTML (left to right sync) |
| [Turndown](https://github.com/mixmark-io/turndown) v7 | HTML → Markdown (right to left sync) |

Both loaded from cdnjs — no npm, no bundler.

## Deploy to Netlify

### Option A — Netlify Drop
Ready made for an instant deploye via a drag & drop of the project folder onto [app.netlify.com/drop](https://app.netlify.com/drop)

### Option B — Git-connected deploy
```bash
git init
git add .
git commit -m "init: MD Forge"
git remote add origin <your-repo-url>
git push -u origin main
```
Then connect the repo in the Netlify dashboard. The `netlify.toml` sets the publish directory and the security headers needed for the File System Access API and rich clipboard copy.

### Option C — Netlify CLI
```bash
npm install -g netlify-cli
netlify deploy --dir . --prod
```

## Browser Support

| Feature | Chrome | Edge | Firefox | Safari |
|---|---|---|---|---|
| File System Access API (open/save) | ✅ | ✅ | ❌ (falls back to download) | ❌ (falls back to download) |
| Rich clipboard (Confluence copy) | ✅ | ✅ | ✅ | ✅ 13.1+ |

Firefox and Safari can still open files and copy for Confluence — they just can't save back to the original file directly (a download is triggered instead).

## Local Development

No build step — just open `index.html` in a browser, or serve locally:

```bash
npx serve .
# or
python3 -m http.server
```

> **Note:** The File System Access API requires a secure context (HTTPS or localhost). It won't work opening `index.html` directly as a `file://` URL.
