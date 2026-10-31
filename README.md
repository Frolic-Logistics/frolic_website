# frolic_website

Frolic's public website, served by GitHub Pages at https://froliclogistics.com.

Plain HTML and one stylesheet. No build step, no JavaScript, and no requests
to other sites (the Overpass font is self-hosted under `assets/fonts/`, OFL licence).

## Pages

| URL | File |
|---|---|
| `/` | `index.html` |
| `/terms-privacy/2026-09-01/` | `terms-privacy/2026-09-01/index.html` |
| `/kyc-consent/2026-09-01/` | `kyc-consent/2026-09-01/index.html` |
| any missing path | `404.html` |

The app opens the two policy pages. The backend sends their addresses from
`TERMS_PRIVACY_URL` and `KYC_CONSENT_URL` (backend spec 004a).

## The one rule: never edit a published policy version

Users accept a specific version, and their consent record names it. If that
version's page changes, the record no longer proves what they agreed to
(DPDP Act; backend `docs/legal-risks.md`, row 8). A typo fix is still a new version.

To change policy text:

1. Copy the current version's folder to a new folder named after the new
   version, for example `terms-privacy/2026-11-15/`.
2. Edit only the copy, and point the links in `index.html` and the other pages at it.
3. Merge it, and check the new page is live.
4. Then, in the backend, change `CURRENT_POLICY_VERSION` (or `KYC_CONSENT_VERSION`)
   and the matching URL together.
5. Leave the old folder in place for good.

`2026-09-01` is a draft, published so development has a working link. The
lawyer's final text goes in a new version; the draft folder stays.

## Working on the site

Same flow as the other repos: a branch off `main`, small commits, a PR,
"Create a merge commit". Every merge to `main` is live within a few minutes.

To preview, run a local server from the repo folder, then open
http://localhost:8000:

```
python -m http.server 8000
```

Opening the files directly works for single pages, but links to folders
(like `terms-privacy/2026-09-01/`) only resolve through a server.
