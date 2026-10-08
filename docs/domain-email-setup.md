# Domain & email setup — consultdkm.in

`consultdkm.in` is registered at GoDaddy (nameservers ns39/ns40.domaincontrol.com).
The apex serves the DKM India marketing site from AWS — **apex A records are
untouched**. All DNS edits below were made through the GoDaddy API
(Personal Access Token, deleted after use).

## Status (2026-10-08)

| Item | State |
|---|---|
| CNAME `structalert` → `dhanada.github.io` | ✅ live — site at https://structalert.consultdkm.in (Let's Encrypt, HTTPS enforced) |
| MX `mx.zoho.com` (10) / `mx2.zoho.com` (20) | ✅ live — resolving |
| SPF `v=spf1 include:zoho.com ~all` | ✅ live — resolving |
| Zoho domain-verification TXT | ⏳ value comes from the Zoho console during signup — add on receipt |
| DKIM `zmail._domainkey` TXT | ⏳ value comes from the Zoho console after verification — add on receipt |
| Zoho mailboxes `dhanada@` + `hello@` | ⏳ create in Zoho Mail admin (free plan, 5 users) |

## Remaining Zoho Mail steps

1. Sign up at <https://www.zoho.com/mail/> (free plan) → Mail Admin →
   **Domains → Add Domain** → `consultdkm.in` → TXT verification.
2. Paste the verification TXT (host + value) to the agent; it is added via
   the GoDaddy API. Then click **Verify** in Zoho.
3. Zoho shows the DKIM record (`zmail._domainkey`); paste it to the agent —
   it is added the same way.
4. Create users `dhanada@consultdkm.in` (Claude Startups application) and
   `hello@consultdkm.in` (public site contact).

## Notes

- A DMARC record already exists on the domain: `v=DMARC1; p=reject; adkim=r;
  aspf=r`. SPF passes via the Zoho include; **add DKIM before sending any
  real mail** so DMARC never rejects it.
- The GoDaddy PAT used for these edits should be deleted at
  developer.godaddy.com once setup is complete.

## Verify

```sh
nslookup structalert.consultdkm.in     # → 185.199.108–111.x (GitHub Pages)
curl -sI https://structalert.consultdkm.in/   # → 200
nslookup -type=MX consultdkm.in        # → mx.zoho.com / mx2.zoho.com
nslookup -type=TXT consultdkm.in       # → "v=spf1 include:zoho.com ~all"
```
