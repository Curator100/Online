# Online Tuition Hub

A WhatsApp-style chat webapp connecting guardians and tutors, backed by Supabase. Installable as an app on phones (PWA).

## Files

- `index.html` — the app itself
- `manifest.json` — makes the app installable ("Add to Home Screen")
- `service-worker.js` — enables offline loading and the install prompt
- `icon-192.png`, `icon-512.png` — app icons
- `netlify.toml` — Netlify build/redirect config

## 1. Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

## 2. Connect to Netlify

1. Go to [app.netlify.com](https://app.netlify.com) → **Add new site** → **Import an existing project**.
2. Choose GitHub and select this repository.
3. Build settings: leave the build command **empty** and set the publish directory to `.` (root) — `netlify.toml` already has this configured, so Netlify should pick it up automatically.
4. Click **Deploy site**. Netlify will give you a URL like `https://your-site-name.netlify.app`.
5. Optional: in **Site settings → Domain management**, set a custom subdomain or connect your own domain.

## 3. Install it as an app

Once live on Netlify (PWAs require HTTPS, which Netlify provides automatically):

- **Android (Chrome):** open the site → tap the **⋮** menu → **Add to Home screen** / **Install app**.
- **iPhone (Safari):** open the site → tap the **Share** icon → **Add to Home Screen**.

It'll then open full-screen like a native app, with its own icon, and keeps working (mostly) if the connection drops briefly.

## Notes

- The Supabase URL and anon key are in `index.html` (client-side, safe to expose — access is controlled by your Supabase RLS policies, not by hiding this key).
- Login credentials are saved in the browser's `localStorage` so users stay logged in between visits; logging out clears them.
- If you rename the repo or deploy under a subpath (not the domain root), update the absolute paths (`/manifest.json`, `/icon-192.png`, `/service-worker.js`) in `index.html` and `manifest.json` to match.
