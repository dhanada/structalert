# StructAlert — DKM Consult Limited (Hong Kong)

Landing site for **StructAlert**, DKM Consult Limited's crowdsourced building
early-warning portal: photographs of buildings and structures → AI condition
scores → failure prediction → alerts to the right people before it breaks.

- **Live (GitHub Pages):** <https://dhanada.github.io/structalert/>
- **Custom domain:** `https://structalert.consultdkm.in/` (CNAME → GitHub Pages)
- **Company:** DKM Consult Limited, Business Registration No. 149460186 (Hong Kong)

## Stack

Plain static site — no build step, no external requests:

- `index.html` — single-page landing (hero, how-it-works, why, about, contact)
- `assets/css/styles.css` — hand-written CSS on the DKM brand palette
  (Blue `#00529F`, Amber `#EB9419`, Sage `#7D8667`, Dark `#231F20`)
- `assets/js/main.js` — mobile nav, reveal-on-scroll, footer year
- `assets/img/dkm-logo.png` — DKM logo (RGB PNG, converted from the CMYK
  source in the consulting-sales repo)

## Hosting notes

- This repository is **GitHub-only**. It is deliberately *not* part of the
  Raspect GitLab (gitsrc.raspect.ai) sync; the consulting-sales repo carries a
  defensive `.gitignore` entry for this folder.
- Pages builds from `main`, root. `.nojekyll` keeps files served verbatim.
- DNS/email setup records: [`docs/domain-email-setup.md`](docs/domain-email-setup.md).

## Local preview

```sh
py -m http.server 8080     # then open http://localhost:8080
```

## Change log

Company-standard change log: [`change-log.md`](change-log.md).
