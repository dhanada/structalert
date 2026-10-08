# Domain & email setup — consultdkm.in

`consultdkm.in` is registered at GoDaddy (nameservers ns39/ns40.domaincontrol.com).
The apex currently serves the DKM India marketing site from AWS — **leave the
apex A records untouched**. Only the records below are added.

## 1. Website subdomain → GitHub Pages

| Type | Host | Points to | TTL |
|---|---|---|---|
| CNAME | `structalert` | `dhanada.github.io` | 600 (1 Hour in GoDaddy UI) |

GoDaddy: **DNS → All records → Add** → Type `CNAME`, Host `structalert`,
Points to `dhanada.github.io`, TTL `1 Hour`.

## 2. Zoho Mail on consultdkm.in

After signing up at <https://www.zoho.com/mail/> (free plan) and adding the
domain in the Zoho Mail admin console, Zoho shows you a verification TXT.
Add it, then add these records:

**MX** (host `@`, no proxying possible on GoDaddy — plain DNS):

| Priority | Points to |
|---|---|
| 10 | `mx.zoho.com` |
| 20 | `mx2.zoho.com` |

**SPF** — TXT, host `@`, value:

```
v=spf1 include:zoho.com ~all
```

**DKIM** — Zoho admin shows a `zmail._domainkey` TXT (host + value); copy it
verbatim from the Zoho console.

**Note:** GoDaddy's own "email" defaults (e.g. their free forwarding MX) must
be removed if present, otherwise MX lookup picks the wrong host.

## 3. Mailboxes

Create in Zoho Mail admin (free plan allows 5 users):

- `dhanada@consultdkm.in` — used for the Claude Startups application
- `hello@consultdkm.in` — public contact address on the site

## 4. Verify

```sh
nslookup -type=MX consultdkm.in        # → mx.zoho.com / mx2.zoho.com
nslookup structalert.consultdkm.in     # → 185.199.108–111.x (GitHub Pages)
curl -sI https://structalert.consultdkm.in/   # → 200 (cert auto-issued by GitHub)
```
