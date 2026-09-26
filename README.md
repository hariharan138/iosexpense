# iOS Expense Tracker (PWA)

Standalone PWA frontend for the expense tracker, copied from the
`frontend/` folder of [Money-Tracker](https://github.com/hariharan138/Money-Tracker).
It's a small Vite static site that talks to the Expense API over HTTP — no
backend code lives in this repo.

## Setup

```bash
npm install
cp .env.example .env.local   # set PRIMARY_API_URL to your API deployment
npm run dev
```

## Build

```bash
npm run build      # outputs dist/
npm run preview
```

`PRIMARY_API_URL` is baked into the build at build time, not read at runtime.

## Install it as an app (PWA)

The dashboard is a progressive web app: installable, launches without browser
chrome, and starts with no network.

- **iPhone:** open the site in Safari, then Share → **Add to Home Screen**.
- **Android / desktop Chrome:** use **Install app** in the address bar or menu.

`public/manifest.webmanifest` declares the name, colors, orientation, and
icons. `public/sw.js` precaches the app shell (filled in at build time by the
`pwa-precache` Vite plugin in `vite.config.js`), so a launch with no network
still renders.

## Android app (Capacitor)

`android/` is a generated Capacitor project wrapping this same HTML/CSS/JS in
a WebView shell:

```bash
npm run build
npx cap sync android
cd android && ./gradlew assembleDebug   # -> app/build/outputs/apk/debug/app-debug.apk
```

Requires JDK 21+. The API origin serving this app (`https://localhost` inside
the WebView) must be added to `CORS_ORIGINS` on the API deployment.

Launcher icons/splash screens are generated from `resources/icon.png` with
`npx capacitor-assets generate --android`.
