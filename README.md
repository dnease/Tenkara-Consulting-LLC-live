# Tenkara Consulting website

Static website for Tenkara Consulting, LLC (tenkaraconsulting.org). Plain HTML, CSS and a small amount of JavaScript. There is no server, database, admin login or plugin system.

**This repository is public. Never commit passwords, API keys, tokens, `.env` files, or anything private.**

## What is here

| Path | What it is |
| --- | --- |
| `index.html` | Home page (hero, services, leadership, about, contact summary) |
| `contact/index.html` | Contact form and map |
| `publications/index.html` | Selected publications (names of the two principals in bold) |
| `contact/thank-you/index.html` | Page shown after a message is sent |
| `404.html` | "Page not found" page |
| `static/css/styles.css` | All styling and brand colors (identical to the previous site) |
| `static/js/main.js` | Smooth scrolling, header effect, card animation (identical to the previous site) |
| `static/images/favicon.svg` | Site icon |
| `.nojekyll` | Tells GitHub Pages to publish the files as they are |

Links between pages are relative, so the site works at a temporary address and on the real domain.

## Before this site goes live (checklist)

- [x] **Connect the contact form (Web3Forms).** Create an access key at web3forms.com for the address that should receive messages, the key is now set in `contact/index.html`. The access key is public by design (it only routes messages to the inbox). Never put any secret key in this repo.
- [x] Spam traps are in place: hidden `fax_number` field and Web3Forms' `botcheck` checkbox (both silently discard the message), plus an hCaptcha widget loaded from the Web3Forms script.
- [ ] In the Web3Forms dashboard, make hCaptcha the preferred captcha / block-spam option, and check whether the free plan can limit submissions to the site's own domain. Send test messages after enabling.
- [ ] Send a real test message and confirm it arrives at the right inbox, and that the thank-you page appears.
- [ ] Review the content flagged below.

## Content to review

- The home page lists `info@tenkaraconsulting.org`. The previous site listed `info@tenkaraconsulting.com`; it was corrected to `.org`. The contact page still lists `don@tenkaraconsulting.org`.
- Dr. Nease's biography now reads "Professor Emeritus" (the previous site said "Professor").
- The footer year was updated to 2026. Update it each January.

## Publishing with GitHub Pages

1. In the repository, open **Settings → Pages**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`.
2. The site appears at a temporary `github.io` address. Test everything there first.
3. When ready for the real domain, add a file named `CNAME` containing `tenkaraconsulting.org`, set the custom domain in the Pages settings, and turn on **Enforce HTTPS**.
4. At the domain registrar, change **only** the website's `A` record (and add a `www` record) to the addresses in GitHub's current Pages documentation. **Do not change the MX, SPF, DKIM or DMARC records**: they run the email for the domain.
5. To undo, change the `A` record back to its previous value.

## Making changes

Edit the HTML files, preview them, and submit changes as a pull request so they can be reviewed before they go live. Pushing to `main` publishes the site.

To preview locally: `python3 -m http.server 8000` in this folder, then open http://localhost:8000.

## Security notes

- Turn on two-factor authentication for GitHub, the domain registrar, the form service and the email account.
- The map uses Leaflet loaded from a CDN, pinned to version 1.9.4 with integrity hashes. If the version is ever changed, the hashes must be updated too, or the map will not load.
- GitHub Pages cannot set custom security headers. Do not add anything to this site that needs them.
- If a secret is ever committed by mistake, revoke and replace it immediately. Deleting the file is not enough, because it stays in the history.
- The contact form tells visitors not to send patient or other sensitive health information. Keep that notice.
