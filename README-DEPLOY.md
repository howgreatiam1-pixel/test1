# WealthOS: deploy as a PWA

This folder is a complete static website. It needs HTTPS (the app uses Web Crypto and the service worker requires it).

## Files
- index.html: the app
- manifest.webmanifest: install metadata (name, icons, colors)
- sw.js: offline support (caches the app shell)
- icons/: home-screen icons (192, 512, 180 px)
- privacy.html: privacy policy (replace the contact placeholder first)
- _headers: security headers and cache rules (Netlify and Cloudflare Pages)
- .nojekyll: stops GitHub Pages from skipping files

## Before going live
1. Edit privacy.html and replace REPLACE_WITH_YOUR_EMAIL.
2. Test locally with `python3 -m http.server 8000` and open http://localhost:8000 (localhost counts as secure).
3. Bump the cache name in sw.js (for example wealthos-v2) whenever you change index.html, so users get the new version.

## Option A: Netlify (easiest, free)
1. Go to app.netlify.com/drop and drag the wealthos-pwa folder onto the page.
2. Netlify gives you an https://<name>.netlify.app address with HTTPS.
3. Optional: Site settings > Domain management to add your own domain.

## Option B: Cloudflare Pages (free, fast)
1. Create a project, choose "Upload assets", and upload the folder.
2. Your site is served over HTTPS at <name>.pages.dev.

## Option C: GitHub Pages (free)
1. Create a repository, upload the folder contents, and commit.
2. Settings > Pages > deploy from the main branch, root folder.
3. Your site is at https://<user>.github.io/<repo>/.
   Note: GitHub Pages does not apply _headers; the security headers are then missing (the app still works).

## Verify it is ready
- Open the site in Chrome, then DevTools > Lighthouse > Progressive Web App. Fix anything it flags.
- Android Chrome: menu > Install app. iPhone Safari: Share > Add to Home Screen.
- Turn on airplane mode and reload: the app should still open.

## Notes
- Each device stores its own encrypted data. Use Encrypted backup to move data between devices.
- The app stores data in the browser only; there is no server database, so nothing is shared automatically.
