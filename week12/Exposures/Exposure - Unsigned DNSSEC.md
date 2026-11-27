---
type: exposure
risk: Low
found: whois, 20 Nov
---

- Targets: [[vulnweb.com]], [[nmap.org]]
- Risk: Low
- Why: WHOIS shows DNSSEC is unsigned on both domains, so DNS records are not signed against spoofing.
- Fix: Enable DNSSEC at DNS host (AWS / Linode) and set DS records at registrar.
