# VITVI R&D Workshop 2026

**Roadblocks, Methods, and Breakthroughs**

Website and registration system for the VITVI R&D Workshop — a two-day, invite-only event bringing together PhD researchers and industry R&D professionals for hands-on technical troubleshooting.

**May 6–7, 2026 · Klosterhotel Lehnin, Brandenburg**

## What's in this repo

```
website/
├── index.html          # Landing page (schedule, format, examples)
├── register.html       # Registration form with domain whitelist
├── legal.html          # Legal notice (German TMG)
├── privacy.html        # Privacy policy (GDPR)
├── config.example.js   # Template for form endpoint config
└── css/
    └── style.css       # Dark minimal theme
docs/
└── google-sheets-setup.md  # Backend setup guide
emails/
└── call-for-participation.md  # Email template
.github/
└── workflows/
    └── pages.yml       # GitHub Pages deployment via GitHub Actions
LICENSE                  # MIT
```

## Deployment

The site is deployed automatically to GitHub Pages on every push to `main`.

**Setup (one-time):**
1. Go to **Settings > Pages** → set **Source** to **GitHub Actions**
2. Go to **Settings > Secrets and variables > Actions** → add a repository secret:
   - Name: `FORM_ENDPOINT`
   - Value: your Google Apps Script web app URL
3. The deploy workflow injects the endpoint into `config.js` at build time

For local development, copy `website/config.example.js` to `website/config.js` and add your endpoint URL.

## Registration Backend

Registration data is collected via a **Google Apps Script** web app that writes directly to a **Google Sheet**. No third-party form services required.

See [`docs/google-sheets-setup.md`](docs/google-sheets-setup.md) for full setup instructions.

**Security layers:**
- Client-side email domain whitelist (5 institutional domains)
- Honeypot field (invisible to humans, catches bots)
- Minimum time check (rejects submissions under 3 seconds)
- Math captcha (simple addition question)
- Server-side domain whitelist (in Apps Script)
- Server-side honeypot and captcha validation
- Rate limiting (max 3 submissions per email per hour)

**Email whitelist** — only these institutional domains can register:
- `@th-brandenburg.de`
- `@rolls-royce.com`
- `@friendship-systems.com`
- `@tu-berlin.de`
- `@b-tu.de`

Others see an inquiry button that opens a pre-filled email to the organizer.

## Forking this for your own workshop

1. Fork the repo
2. Edit content in `index.html`, `register.html`, `legal.html`, `privacy.html`
3. Set up a Google Sheet + Apps Script backend (see `docs/google-sheets-setup.md`)
4. Add your `FORM_ENDPOINT` as a GitHub secret
5. Update the email domain whitelist in both `register.html` and your Apps Script
6. Enable GitHub Pages with Actions as source

## Author

- **Robert Flassig** — organizer, TH Brandenburg

## License

[MIT](LICENSE)
