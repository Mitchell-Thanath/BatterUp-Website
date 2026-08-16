# Batter Up — public website

Static site hosting the **Privacy Policy** and **Support** pages that Apple requires for App Store
submission. No build step, no dependencies, no JavaScript.

## Live URLs

| Page | URL |
| --- | --- |
| Privacy Policy | `https://mitchell-thanath.github.io/BatterUp-Website/privacy/` |
| Support | `https://mitchell-thanath.github.io/BatterUp-Website/support/` |
| Home | `https://mitchell-thanath.github.io/BatterUp-Website/` |

These paths are permanent — redeploying does not change them.

## ⚠️ Before submitting to Apple

The contact email is a **placeholder**. It appears twice and renders as a loud yellow dashed box
on the live pages so it can't be missed:

- `privacy/index.html` — section 11, Contact
- `support/index.html` — Contact us

Replace `support@[DOMAIN] — PLACEHOLDER: replace with the real contact address before launch` with a
real address, and drop the surrounding `<span class="needs-fill">…</span>` wrapper so it renders as
normal text. Consider making it a `mailto:` link.

Also confirm before launch:

- [ ] **Contact email** — real address (a `@cheneybrothers.com` support address or a dedicated Batter Up inbox).
- [ ] **Legal entity name** — the pages say "Cheney Brothers". Confirm whether Cheney wants a formal
      entity named instead (e.g. "Cheney Brothers, Inc.") and update `privacy/index.html` §1 plus the
      footers if so.
- [ ] **Effective date** — currently August 16, 2026 in `privacy/index.html`. Set it to the actual
      launch date if different.
- [ ] **Domain** — if a custom domain is used instead of github.io, see below.

## Structure

```
index.html          home / landing
privacy/index.html  Privacy Policy   →  /privacy/
support/index.html  Support          →  /support/
404.html            not-found page
styles.css          shared stylesheet
.nojekyll           serve files as-is, no Jekyll processing
```

The site collects nothing: no analytics, no ad trackers, no cookies, no forms, no third-party fonts
or CDNs. Every request stays on the origin.

## Deployment

GitHub Pages, served from the `main` branch at the repository root. Pushing to `main` redeploys
within a minute or two.

## Using a custom domain

1. Add a `CNAME` file at the repo root containing the bare domain (e.g. `batterup.example.com`).
2. Point the DNS record at GitHub Pages, then set the domain under Settings → Pages and enable
   "Enforce HTTPS".
3. Update the absolute `/BatterUp-Website/...` paths in `404.html` to `/...` — that file is the only
   one using absolute paths; all other pages use relative links and need no changes.
4. Update the URLs in App Store Connect.
