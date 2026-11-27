# Training Log (PWA)

## Get it on your phone
A PWA has to be served over HTTPS before Android will install it. The easiest way is GitHub Pages:

1. Create a new public repo, for example `training-log`, and upload every file in this folder to it.
2. Go to Settings, then Pages, choose "Deploy from a branch", pick `main` and `/ (root)`, and save.
3. Open `https://<your-username>.github.io/training-log/` in Chrome on your phone.
4. In the Chrome menu, choose "Add to home screen" (or "Install app").

Netlify Drop (drag the folder onto app.netlify.com/drop) also works if you'd rather not set up a repo.

## Data
- Everything is stored in IndexedDB on the phone. Nothing is sent anywhere.
- Use More, then Back up now, once a week. On Android this opens the share sheet, so you can save the backup straight to Drive.
- Restore merges by default. Type REPLACE to wipe the phone first.
- Clearing Chrome's site data or uninstalling the app deletes the logs, so keep backups.

## Future blocks
- **Clone forward**: copies the current block to start the Monday after it ends, then opens the editor.
- **New block**: blank weeks, carrying over the current meal plan.
- **Import block JSON**: `example-block.json` shows the format, which is the Nov to Dec block. Edit a copy in any text editor, or generate one from a script, then import it.
- History and progression are keyed by exercise name, so keep names identical across blocks if you want trends to carry over.

## Files
- `index.html`: the whole app (HTML, CSS and JS, with the seed block embedded)
- `sw.js`: service worker for offline use (network first, falls back to cache)
- `manifest.webmanifest` and the icons: install metadata
- `example-block.json`: block import format
