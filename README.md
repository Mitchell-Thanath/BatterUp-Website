# Batter Up — public website

Static site hosting the **Privacy Policy** and **Support** pages that Apple requires for App Store
submission. No build step, no dependencies, no JavaScript.

## Pages

| Page | Path |
| --- | --- |
| Privacy Policy | `/privacy` |
| Support | `/support` |
| Home | `/` |

Once deployed, the App Store Connect URLs are `https://<your-domain>/privacy` and
`https://<your-domain>/support`. These paths are permanent — redeploying does not change them.

## Deploying to Vercel

There is no build step; this is a plain static site.

**Option A — dashboard:** Import the GitHub repo at [vercel.com/new](https://vercel.com/new).
Framework Preset: **Other**. Leave build command and output directory empty. Deploy.

**Option B — CLI:**

```sh
npm i -g vercel
vercel        # preview deploy
vercel --prod # production deploy
```

Pushing to `main` redeploys automatically once the repo is linked.

`vercel.json` sets `cleanUrls` and `trailingSlash: false`, so the canonical URLs have no trailing
slash (`/privacy`, not `/privacy/`). Vercel serves `404.html` for unknown paths.

## Structure

```
index.html          home / landing
privacy/index.html  Privacy Policy   →  /privacy
support/index.html  Support          →  /support
404.html            not-found page
styles.css          shared stylesheet
vercel.json         clean URLs + security headers
```

All links are root-relative (`/privacy`), so the site must be served from a domain root — which is
what Vercel does by default.

## Privacy posture of the site itself

The site collects nothing: no analytics, no ad trackers, no cookies, no forms, no third-party fonts
or CDNs. Type uses the system font stack and the only asset request is same-origin `styles.css`.
This is deliberate — it keeps the policy short and true. **Don't add analytics** without updating
`/privacy` to match.

## Editing the policy

- **Contact email** — `mitchellthanath@gmail.com`, in `privacy/index.html` §11 and
  `support/index.html`. Change both if it moves to a dedicated inbox.
- **Dates** — "Effective date" and "Last updated" are at the top of `privacy/index.html`. Bump
  "Last updated" whenever the policy text changes.
- The policy names **Supabase**, **Expo**, and **Apple** as the only third parties. If the app adds
  another service provider (analytics, crash reporting, a maps SDK that phones home), section 5 must
  be updated before that ships.

## Note on custom domains

Add the domain under the Vercel project's Settings → Domains and point DNS at Vercel. No code
changes are needed — nothing in the site hardcodes a hostname.
