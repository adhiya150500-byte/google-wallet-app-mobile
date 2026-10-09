# Google Wallet — now a mobile app

This is your original project, upgraded so it looks and behaves like a real
mobile app on your laptop, with working camera and file upload.

## What changed

1. **Phone-frame app shell** — the whole app now renders inside a
   phone-shaped frame (notch, status bar, home indicator) whenever you open
   it on a laptop/desktop browser. On an actual phone (or once installed),
   the frame disappears and the app just fills the screen normally, like
   any native app. See `components/mobile-shell.tsx` and the
   `.phone-*` styles at the bottom of `app/globals.css`.

2. **Installable as an app (PWA)** — added `public/manifest.json`,
   `public/sw.js`, and app icons (`public/icons/`). When you visit the app
   in Chrome/Edge on your laptop you'll see an install icon in the address
   bar (or the blue "Install app" button in the bottom right) — click it and
   it opens in its own window, pinned to your taskbar/dock, exactly like a
   installed mobile app.

3. **Real camera access** — the Camera tab under **Dashboard → Upload**
   now actually opens your device camera (`getUserMedia`), shows a live
   preview, lets you snap a photo, retake it, and confirm it — see
   `components/camera-capture.tsx`. Your browser will ask for camera
   permission the first time.

4. **Real file upload with previews** — the Upload tab stores chosen
   files in memory, shows image thumbnails in a grid, and lets you remove
   any of them. See the rewritten `components/receipt-upload.tsx`.

Everything else (login, dashboard, send/receive money, rewards, bill
reminders, chat bot, offers) is untouched — same project, same layout,
same data — just wrapped as a mobile app shell.

## Run it

```bash
npm install
npm run dev
```

Then open **http://localhost:3000** in Chrome or Edge.

- On your laptop you'll see it inside a phone frame with an "Install app"
  button — click it to install as a standalone app.
- On your phone, open the same URL (make sure your phone is on the same
  Wi-Fi and use your laptop's local IP, e.g. `http://192.168.x.x:3000`) and
  "Add to Home Screen" from the browser menu.

## Notes

- Camera access requires either `localhost` or HTTPS — it will **not** work
  over a plain `http://<ip>` address from another device unless you deploy
  it (e.g. Vercel) or set up HTTPS locally. On `localhost` on your own
  laptop it works out of the box.
- To deploy so you can install it on your phone too, the easiest option is
  pushing this folder to Vercel (`vercel deploy`) — it's a standard Next.js
  app, no extra config needed.
