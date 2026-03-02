# VITVI R&D Workshop 2026

**Roadblocks, Methods, and Breakthroughs**

Website and registration system for the VITVI R&D Workshop — a two-day, invite-only event bringing together PhD researchers and industry R&D professionals for hands-on technical troubleshooting.

**May 6–7, 2026**

## What's in this repo

```
website/
├── index.html          # Landing page (schedule, format, example anti-pitch)
├── register.html       # Registration form with email domain whitelist
├── impressum.html      # Legal notice (German TMG)
├── datenschutz.html    # Privacy policy (German DSGVO)
└── css/
    └── style.css       # Dark minimal theme
.github/
└── workflows/
    └── pages.yml       # GitHub Pages deployment via GitHub Actions
LICENSE                  # MIT
```

## Deployment

The site is deployed automatically to GitHub Pages on every push to `main`.

**Setup (one-time):**
1. Go to **Settings > Pages**
2. Set **Source** to **GitHub Actions**
3. That's it — the workflow deploys the `website/` folder

**Live at:** [batmanvane.github.io/VITVI_RD_Workshop](https://batmanvane.github.io/VITVI_RD_Workshop/)

## Registration

The registration form uses [Formspree](https://formspree.io) as the backend. Submissions go to the organizer's email and Formspree dashboard.

**Email whitelist** — only these institutional domains can register directly:
- `@th-brandenburg.de`
- `@rolls-royce.com`
- `@friendship-systems.com`
- `@tu-berlin.de`
- `@b-tu.de`

Others see an inquiry button that opens a pre-filled email to the organizer.

## Authors

- **Robert Flassig** — organizer, TH Brandenburg
- **Claude Code** — co-author

## License

[MIT](LICENSE)
