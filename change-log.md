# StructAlert — Change Log

Company-wide change-log audit standard (see
`~/.claude/company/change-log-audit.md`).

StructAlert: crowdsourced building condition intelligence by DKM Consult
Limited (Hong Kong). This repository is **GitHub-only** and deliberately not
part of the Raspect GitLab sync.

**Linked to:**
`https://github.com/dhanada/structalert` (this repo); the launch is also
logged in the consulting-sales repo
(`Accounts/DKM_DKM-India-Projects/DKM.C.202610_consult/change-log.md`).

## Children

*(none — leaf repository)*

## Entries

### 2026-10-08 — Custom domain + email DNS live (structalert.consultdkm.in, Zoho MX/SPF)

- **What:**  https://structalert.consultdkm.in/ live: GoDaddy CNAME
  `structalert` → `dhanada.github.io` added via GoDaddy API (PAT), custom
  domain set on GitHub Pages (CNAME file committed by GitHub in `2ab4348`),
  Let's Encrypt cert issued, HTTPS enforced (http → 301 https;
  dhanada.github.io → 301 custom domain). Zoho Mail DNS pre-staged on
  `consultdkm.in`: MX `mx.zoho.com` (10) + `mx2.zoho.com` (20), SPF
  `v=spf1 include:zoho.com ~all` — resolving. Remaining Zoho steps tracked
  in `docs/domain-email-setup.md` (verification TXT + DKIM values from the
  Zoho console; mailboxes `dhanada@`/`hello@`). Existing DMARC p=reject
  noted — DKIM must be added before real mail.
- **When:**  2026-10-08
- **Where:** GoDaddy DNS (API); GitHub Pages config; `CNAME`,
  `docs/domain-email-setup.md`, `change-log.md` (this entry)
- **How:**   GoDaddy API PUTs (CNAME/MX/TXT) with the user-issued PAT;
  `gh api` PUT pages (cname + https_enforced — `-F` for the boolean);
  verified via nslookup + curl (200 on custom domain, cert CN/issuer/dates,
  301 http→https, MX/SPF answers; Windows DNS cache flush needed once for
  the pre-propagation NXDOMAIN). `Ref` is the pre-amend commit hash, kept
  resolvable via local tag `structalert-ref-domain`.
- **Why:**   Claude Startups application needs the live site + working
  company email on the same domain; Dhanada issued the GoDaddy PAT so the
  agent could automate the records.
- **Who:**   AIOS (agent), on instruction from Dhanada
- **Ref:**   8cfbe03

### 2026-10-08 — StructAlert landing site v1.0 (GitHub Pages)

- **What:**  Single-page StructAlert landing site for DKM Consult Limited
  (Hong Kong, BR No. 149460186): crowdsourced building images → AI condition
  score → failure prediction → smart alerts. Static site, no build step, no
  external requests — `index.html` + `assets/css/styles.css` +
  `assets/js/main.js` + DKM logo (converted from CMYK to RGB PNG). Sections:
  hero with demo condition report, stats, how-it-works (4 steps), why-now,
  about (entity facts), early-access contact (`hello@consultdkm.in`). Brand
  palette from the DKM logo: Blue `#00529F`, Amber `#EB9419`, Sage `#7D8667`,
  Dark `#231F20`. Hosting: GitHub Pages on `main`, custom domain
  `structalert.consultdkm.in` (CNAME; DNS record added by Dhanada at
  GoDaddy); apex `consultdkm.in` stays on the AWS-hosted DKM India site.
  Setup records: `docs/domain-email-setup.md` (CNAME, Zoho MX/SPF/DKIM).
- **When:**  2026-10-08
- **Where:** `index.html`, `assets/css/styles.css`, `assets/js/main.js`,
  `assets/img/dkm-logo.png`, `docs/domain-email-setup.md`, `README.md`,
  `change-log.md` (this entry)
- **How:**   Hand-written HTML/CSS/JS (DKM palette), logo converted
  PowerShell/System.Drawing (CMYK JPEG → 256 px RGB PNG), committed and
  pushed to `https://github.com/dhanada/structalert` (public; GitHub-only —
  not synced to the Raspect GitLab). `Ref` is the pre-amend commit hash of
  the site commit, kept resolvable via local tag `structalert-ref-launch`.
- **Why:**   Claude Startups application for DKM Consult Limited (HK) needs a
  live website + company email on the same domain; StructAlert is the
  product pitch. Dhanada chose the product name StructAlert, the
  `consultdkm.in` domain (already owned), Zoho Mail free for email, and a
  fresh GitHub repo.
- **Who:**   AIOS (agent), on instruction from Dhanada
- **Ref:**   0c3af16
- **Impact:** Blocks on Dhanada: GoDaddy CNAME `structalert` →
  `dhanada.github.io`, Zoho Mail domain setup + `dhanada@`/`hello@`
  mailboxes, then the Claude Startups application.
