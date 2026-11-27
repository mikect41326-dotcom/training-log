# Training Log (PWA)

## Get it on your phone
A PWA has to be served over HTTPS before Android will install it. The easiest way is GitHub Pages:

1. Create a new public repo, for example `training-log`, and upload every file in this folder to it.
2. Go to Settings, then Pages, choose "Deploy from a branch", pick `main` and `/ (root)`, and save.
3. Open `https://<your-username>.github.io/training-log/` in Chrome on your phone.
4. In the Chrome menu, choose "Add to home screen" (or "Install app").

Netlify Drop (drag the folder onto app.netlify.com/drop) also works if you'd rather not set up a repo.

## Android APK (built by GitHub)
This repo also builds an installable APK on GitHub's servers every time you upload changes. Nothing needs installing on your computer.

1. **Upload everything in this folder**, including the hidden `.github` folder and `.gitignore`. On a Mac, press Cmd+Shift+. in Finder to show hidden files. If the `.github` folder won't upload, use Add file, then Create new file, type `.github/workflows/build-apk.yml` as the name, and paste the file's contents in.
2. **Add the signing key** (one off): in the repo go to Settings, Secrets and variables, Actions, New repository secret. Name it `DEBUG_KEYSTORE_B64` and paste in the whole contents of `DEBUG_KEYSTORE_B64.txt`. Keep that file somewhere safe and don't upload it. The same key on every build is what lets updates install over the top without losing data.
3. **Wait for the build**: the Actions tab shows "Build Android APK" running. It takes a few minutes. You can also start it by hand there with Run workflow.
4. **Install on your phone**: open `https://github.com/YOUR-USERNAME/YOUR-REPO/releases/latest` in Chrome on the phone, tap `training-log.apk`, then open it. Android will ask you to allow installs from Chrome the first time. Play Protect may warn that the developer is unknown, because the app isn't from the Play Store. Choose to install anyway.
5. **Move your data across**: the APK keeps its own data, separate from the browser version. In the browser version go to More, Back up now. Then in the APK go to More, Restore, and pick that file.

Every later upload produces a new release (1.0.2, 1.0.3 and so on). Install it over the top, and your data stays.

Differences from the browser version: backups open Android's share sheet (save to Drive, Files, email), the rest timer uses the phone's vibration motor, and exercise photos need a signal the first time you open them.

## Data
- Everything is stored in IndexedDB on the phone. Nothing is sent anywhere.
- Use More, then Back up now, once a week. On Android this opens the share sheet, so you can save the backup straight to Drive.
- Restore merges by default. Type REPLACE to wipe the phone first.
- Clearing Chrome's site data or uninstalling the app deletes the logs, so keep backups.

## Weekly check-in (Thursday)
- Thursday's page shows a check-in button. The check-in covers the 7 days ending that Thursday (Fri to Thu), which takes in all five sessions and all three AM classes.
- Measurements: neck, shoulders, chest, waist, hips, left and right biceps (flexed), forearms, thighs and calves, plus optional body fat %. Each one has a note on where to measure, and shows your last reading and the change.
- Insights shows first against latest for every measurement in the block, plus a trend chart. More lets you export check-ins as CSV.
- To use a different check-in day for a block, change it in the block editor.

## Updating an installed copy
Upload the new files over the old ones in the repo. Your data stays on the phone and is migrated automatically. Close and reopen the app once (with signal) to pick up the new version.

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
- `catalog.json`: the exercise catalogue (876 exercises from Free Exercise DB, public domain). Photos load from the dataset on GitHub when you open an exercise and are then cached for offline use.
