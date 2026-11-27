---
type: domain
found: whois, dig, nslookup, crt.sh, theHarvester, Google, 20 Nov
---

# [[nmap.org]]

## WHOIS
- Registrar: Dynadot Inc
- Creation Date: 1999-01-18T05:00:00Z
- Expiry Date: 2032-01-18T05:00:00Z
- Name Servers: `ns1.linode.com`, `ns2.linode.com`, `ns3.linode.com`, `ns4.linode.com`, `ns5.linode.com`
- Registrant: REDACTED FOR PRIVACY
- DNSSEC: Unsigned

## DNS Records
- IP: [[50.116.1.184]]
- DNS host: Linode - see [[nmap - Technology]]
- Mail provider: Google - see [[nmap - People]]
- SPF: `v=spf1 a mx ptr ip4:50.116.1.184 ip6:2600:3c01::f03c:91ff:fe98:ff4e ip6:2600:3c01:e000:3e6::6d4e:7061 include:_spf.google.com ~all` (allows listed IPs, A/MX/PTR and Google; `~all` is softfail) - see [[Exposure - Weak SPF Softfail]]
- DMARC: none - see [[Exposure - Missing DMARC Policy]]

## Certificate logs (crt.sh)
- Found public SSL certificates (also shared with `insecure.com`).
- Names confirmed in crt.sh: [[nmap.org]], [[svn.nmap.org]], [[issues.nmap.org]], [[scanme.nmap.org]].

## Confirmed subdomains
- [[scanme.nmap.org]] -> [[45.33.32.156]]
- [[chat.nmap.org]] -> [[45.33.32.156]]
- [[svn.nmap.org]] -> [[50.116.1.184]]
- [[issues.nmap.org]] -> [[50.116.1.184]]

## Wildcard DNS check
- `dig +short this-does-not-exist-123.nmap.org` returned [[50.116.1.184]].
- This means `nmap.org` has Wildcard DNS (`*.nmap.org`). So dig and theHarvester alone do not prove that a subdomain on `50.116.1.184` is real. Unconfirmed ones are in [[unconfirmed names]].

## Google Dorks (Web tab / udm=14)
- `site:nmap.org filetype:pdf` -> found public PDFs like `https://nmap.org/docs/discovery.pdf`
- `site:nmap.org intitle:"index of"` -> `http://scanme.nmap.org/images/` is open directory
