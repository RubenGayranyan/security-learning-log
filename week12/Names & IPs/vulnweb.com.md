---
type: domain
found: whois, dig, nslookup, crt.sh, theHarvester, Google, 20 Nov
---

# [[vulnweb.com]]

## WHOIS
- Registrar: Gandi SAS
- Creation Date: 2010-06-14T07:50:29Z
- Expiry Date: 2027-06-14T07:50:29Z
- Name Servers: `NS-136.AWSDNS-17.COM`, `NS-557.AWSDNS-05.NET`, `NS-1588.AWSDNS-06.CO.UK`, `NS-1450.AWSDNS-53.ORG`
- Registrant: REDACTED FOR PRIVACY (Org: Invicti Security Limited, MT)
- DNSSEC: Unsigned

## DNS Records
- IP: [[44.228.249.3]]
- DNS host: AWS Route 53 (`awsdns`) - see [[vulnweb - Technology]]
- Mail provider: Google (`aspmx.l.google.com`) - see [[vulnweb - People]]
- SPF: `v=spf1 ~all` (no mail servers allowed, `~all` is softfail) - see [[Exposure - Weak SPF Softfail]]
- DMARC: none (empty result) - see [[Exposure - Missing DMARC Policy]]

## Certificate logs (crt.sh)
- No certificates found for `%.vulnweb.com`.
- Reason: sites work only on `http://`, they dont use HTTPS. See [[Exposure - No HTTPS on vulnweb.com]].

## Confirmed subdomains
- [[rest.vulnweb.com]] -> [[18.215.71.186]]
- [[testasp.vulnweb.com]] -> [[44.238.29.244]]
- [[testaspnet.vulnweb.com]] -> [[44.238.29.244]]
- [[testhtml5.vulnweb.com]] -> [[44.228.249.3]]
- [[testphp.vulnweb.com]] -> [[44.228.249.3]]

## Check every name
- `dig +short this-does-not-exist-123.vulnweb.com` returned empty (no wildcard DNS).
- Passive tools gave a lot of old/deleted names, I checked them with dig and moved dead ones to [[unconfirmed names]].

## Google Dorks (Web tab / udm=14)
- `site:vulnweb.com -www` -> showed active test subdomains (testphp, testasp, testhtml5, etc.)
- `site:vulnweb.com inurl:login` -> showed login pages on test sites (all on http)
