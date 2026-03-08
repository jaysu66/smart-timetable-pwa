# PWA Usage

## What this is

This project is now an installable PWA.

You do not need a backend server.
You do need to serve these files over HTTP or HTTPS.

For real phone installation and offline cache:

- `https://...` works
- `http://localhost:...` works on the same device
- `http://192.168.x.x:...` is fine for preview, but PWA install and service worker are usually blocked on phones because it is not a secure context

## Files

- `index.html`: main app page
- `schedule-data.js`: generated timetable data
- `manifest.webmanifest`: PWA manifest
- `sw.js`: service worker for offline cache
- `icons/`: app icons

## Local preview on the computer

Run:

```powershell
cd C:\Users\su200\Desktop\手机课表开发
python -m http.server 4173
```

Then open:

```text
http://127.0.0.1:4173
```

## Fastest way to use it on your phone

Deploy these files to any static hosting that gives you HTTPS.

Examples:

- GitHub Pages
- Cloudflare Pages
- Vercel
- Netlify
- your own Nginx site

## Temporary public HTTPS link

If you just want to test it on your phone right now, you can start a temporary Cloudflare Tunnel:

```powershell
cd C:\Users\su200\Desktop\手机课表开发
powershell -ExecutionPolicy Bypass -File .\scripts\start_public_https.ps1
```

It will print a `https://...trycloudflare.com` address.

Notes:

- this link only works while your computer is on
- this link changes every time you restart the tunnel
- for long-term use, still deploy to a real static hosting service

Upload the whole folder contents except the original source images and xls if you do not want them public.

The minimum public files are:

- `index.html`
- `schedule-data.js`
- `manifest.webmanifest`
- `sw.js`
- `icons/`

## Install on Android

1. Open the HTTPS URL in Chrome.
2. Wait a few seconds after the page fully loads.
3. If the install card appears, tap `添加到主屏幕`.
4. If it does not appear, open the browser menu and choose `安装应用` or `添加到主屏幕`.

## Install on iPhone

1. Open the HTTPS URL in Safari.
2. Tap `分享`.
3. Tap `添加到主屏幕`.

## When timetable data changes

If the Excel changes:

```powershell
cd C:\Users\su200\Desktop\手机课表开发
python scripts\build_schedule_data.py
```

Then redeploy:

- `schedule-data.js`
- `index.html` if the UI changed
- `sw.js` if offline assets changed

## Cache refresh

If the phone still shows old data:

1. Close the app from recent tasks.
2. Open it again while online.
3. If needed, clear the site data in the browser and reopen it.
