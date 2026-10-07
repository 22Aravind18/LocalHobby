LUMO - installable PWA (money, journal, habits)

FILES
  index.html            the whole app (HTML + CSS + JS in one file)
  manifest.webmanifest  install info (name, colours, icons, shortcuts)
  sw.js                 service worker (offline, update prompt)
  icons/                192, 512, maskable 512, apple-touch icon
  twa/                  files for the hosted-PWA Android method (Bubblewrap / PWABuilder)

RUN / INSTALL (web)
  1. Upload this whole folder to any HTTPS host (Netlify Drop, GitHub Pages, Vercel, Cloudflare Pages).
     Local test:  python3 -m http.server 8000  then open http://localhost:8000
  2. Open the link on your phone. Chrome: menu > Install app. Safari: Share > Add to Home Screen.
  Opening index.html directly from a file works as a normal page, without install or offline.

ANDROID, METHOD A: hosted PWA as an APK/AAB (Trusted Web Activity)
  Needs the folder above live on HTTPS first.
  Option 1, PWABuilder: go to pwabuilder.com, enter your URL, choose Android, download the package.
  Option 2, Bubblewrap CLI:
     npm i -g @bubblewrap/cli
     edit twa/twa-manifest.json (host + URLs), then:  bubblewrap init --manifest=https://YOUR-DOMAIN/manifest.webmanifest
     bubblewrap build
  Then publish /.well-known/assetlinks.json on your domain using twa/assetlinks.json.template
  with your signing key SHA-256 (this removes the browser address bar).

ANDROID, METHOD B: HTML bundled inside the app (no hosting needed)
  Use the separate lumo-android.zip (Android Studio project, same index.html inside assets).

CHANGES IN THIS VERSION
  - Professional light/dark interface (Settings > Appearance > Theme)
  - OTP / SMS removed. Accounts use email + password only
  - Journal consistency system replaces the flame streak: current and longest streak,
    30-day rate, weekly target, next-milestone progress, 16-week activity map
  - XP, levels and emoji removed; milestones are listed under Profile

YOUR DATA
  Stored on the device (localStorage). Use Profile > Backup & data > Export backup to keep a copy.
  Existing accounts and data from the previous version keep working.
