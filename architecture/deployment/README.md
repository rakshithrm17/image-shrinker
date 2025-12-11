# Deployment & Hosting — Image Shrinker

## Deployment Goals
- Zero-cost or minimal-cost hosting for MVP
- Fast CDN delivery for static assets (including WASM)
- Simple CI for building & publishing
- Privacy-safe analytics (optional)

## Hosting Options (Free)
1. **Vercel** — easy deploy from GitHub, automatic builds, edgestatic CDN.
2. **Netlify** — static hosting + CDN, build hooks.
3. **GitHub Pages** — simplest, free; may need manual steps for SPA routing.
Choose any; Vercel recommended for easiest WASM + caching support.

## Build & CI
- Use Vite build: `npm run build` → outputs static `dist/` folder.
- CI flow (GitHub Actions recommended):
  - On push to `main`: run `npm ci`, `npm run build`, optionally run tests.
  - Deploy to Vercel/Netlify using their GitHub integration or via deploy action.

## Serving WASM
- Ensure WASM files are served with correct `Content-Type: application/wasm`.
- Ensure `Cache-Control` headers allow CDN caching (long TTL for WASM).
- Lazy-load codecs via dynamic import to reduce initial bundle.

## PWA Considerations (Phase 4)
- Add `manifest.json` and service worker.
- Cache essential assets and WASM modules for offline use.
- Use Workbox or Vite PWA plugin to manage caching strategies.

## Security & Privacy
- Enforce HTTPS for all hosting.
- No server endpoints for image uploads (MVP).
- If adding backend later: require explicit opt-in for cloud upload and explicit data retention policy.
- For analytics: use privacy-first options (Plausible, Simple analytics) AND anonymize IPs.

## Monitoring & Error Reporting
- Client-side error logging (Sentry or a lightweight alternative) — do NOT send image or PII. Log only stack traces and user agent.
- Basic uptime monitoring via external tools (optional).

## Domain & HTTPS
- Start with free Vercel/Netlify subdomain.
- Add custom domain when ready (buy domain and configure DNS).
- HTTPS provided by hosting (Let's Encrypt).

## Rollback & Releases
- Keep `main` branch deployable.
- Use preview branches for testing big features.
- Tag releases and produce changelog in `docs/` or `CHANGELOG.md`.

## Deployment Checklist
- [ ] Build passes locally: `npm run build`
- [ ] WASM modules present in `dist/` and have correct headers
- [ ] Service worker (if PWA) configured
- [ ] CI configured to run build on push
- [ ] Deployment target connected (Vercel/Netlify)
- [ ] Analytics configured (optional) and privacy checkbox in UI

## Developer tasks (deployment)
- Create GitHub Action: build + test on push.
- Connect repo to Vercel (recommended) and configure environment.
- Setup caching headers for WASM and static assets.
- Test cross-browser builds and WASM load on low-end devices.
