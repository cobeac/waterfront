# RFID Check-In — PWA

A wristband check-in scanner that installs as a standalone app on Android tablets.
Works fully offline once installed. Scan log auto-saves to the device after every scan.

---

## Files

```
checkin-app/
├── index.html      ← The app (edit this to change anything)
├── sw.js           ← Service worker (offline caching — don't touch)
├── manifest.json   ← PWA metadata (name, icon, colors)
├── icons/
│   ├── icon-192.png
│   └── icon-512.png
└── README.md
```

---

## Deploying to GitHub Pages (one-time setup)

1. Create a free account at github.com if you don't have one
2. Create a new repository — name it anything (e.g. `checkin-app`)
3. Upload all the files in this folder (drag and drop in the GitHub web UI)
4. Go to **Settings → Pages → Source** and set it to `main` branch, `/ (root)`
5. GitHub gives you a URL like `https://yourname.github.io/checkin-app`

That's your app URL. It updates automatically whenever you push changes.

---

## Installing on the Android tablet (one-time per tablet)

1. Open Chrome on the tablet
2. Go to your GitHub Pages URL
3. Tap the **⋮ menu → "Add to Home screen"** (or Chrome may show an install banner)
4. Name it "Check-In" and confirm
5. An icon appears on the home screen — open it to launch as a standalone app

The app is now cached locally. **WiFi no longer required.**

---

## First-time use on the tablet

1. Open the app (tap the home screen icon)
2. You'll see a setup screen — tap **"Choose wristband list"** and pick the `.xlsx` file
3. The app remembers the list. Next time it opens straight to scanning.

---

## Daily use

- Open the app → already loaded, scan immediately
- Scans auto-save to the device after every scan (visible as "Saved ●" in the header)
- At end of day, tap **"Export log"** in the footer to save a CSV to Downloads

---

## Updating the wristband list

When you get a new attendee file:
1. Email/transfer the new `.xlsx` to the tablet
2. Open the app
3. Tap **"Update wristband list"** (footer) and pick the new file
4. Done — the new list is cached and ready

---

## What happens if the app is closed mid-day?

Nothing bad. Reopen it and it picks up exactly where it left off:
- Same scan log
- Same in/out status for every wristband
- Same wristband list

The log is stored in the browser's local database (IndexedDB) and persists until you tap "Clear log" or uninstall the app.

---

## Updating the app itself

If you change `index.html`:
1. Push the updated file to GitHub
2. Bump the cache version in `sw.js`: change `checkin-v1` to `checkin-v2`
3. Push `sw.js` too
4. On the tablet, open Chrome (not the app), go to the URL, and do a hard refresh
5. The new version is cached — reopen the app icon to get it
