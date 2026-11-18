---
type: troubleshooting
created: 2026-11-18
status: resolved
tags:
  - troubleshooting
  - web
  - hosting
  - spa
---

# Onboarding links 404 in production

## Problem
Links sent in onboarding emails (application-status, confirm-and-pay) and the
Stripe Checkout post-payment redirect failed when opened directly:

- `https://ximembersclub.com/request-access/status?token=...` — 404
- `https://ximembersclub.com/request-access/confirm-pay?token=...` — 403, then 404
  (including on what looked like an XHR to the same path)
- `https://www.ximembersclub.com/` (root, with `www`) loaded the app fine

## Root Cause
Two separate issues, both in hosting configuration rather than the app code:

1. **No SPA fallback rule on production hosting (Hostinger/Apache).** The web
   app is a client-side single-page app (React Navigation handles routing in
   the browser). Webpack's dev server has `historyApiFallback: true` built in,
   but that doesn't carry over to static hosting — a direct request for a path
   like `/request-access/confirm-pay` isn't a real file on disk, so Apache
   returned 404 instead of serving `index.html` and letting the app's router
   take over.
2. **www vs apex domain handling was inconsistent** — the root loaded under
   `www.ximembersclub.com`, but a deep path on the apex domain
   (`ximembersclub.com`) returned 403 before 404, suggesting no canonical
   redirect existed between the two.

Earlier in the same day, the web-facing links (status, confirm-and-pay, Stripe
redirect) had also been changed from being derived from the request's
`Origin` header (which resolved to `localhost` during local dev, and so
"worked" only by accident) to a hardcoded `https://ximembersclub.com` origin.
That change was correct — `ximembersclub.com` is the right production domain —
but it exposed this pre-existing hosting gap, since local dev never exercised
a real static-file server.

## Solution
Added `web/.htaccess` with:
- A redirect from `www.ximembersclub.com` to the apex domain.
- An Apache rewrite rule to serve `index.html` for any request that isn't an
  existing file or directory (the standard SPA fallback pattern).

Added `web/copy-htaccess.js` and wired it into `build:web`
(`package.json`) so `.htaccess` is copied into `dist/` on every production
build, since webpack's `output.clean: true` would otherwise wipe a manually
placed copy on each rebuild.

## Verification
Rebuild `dist/` (including the hidden `.htaccess` file), upload to Hostinger,
then load the confirm-pay/status links directly to confirm they resolve
instead of 404/403.

## Resolution Status
Code fix committed and pushed. Still needs the rebuilt `dist/` uploaded to
Hostinger to take effect in production.

## References
- None
