---
type: exposure
risk: High
found: crt.sh, Firefox, 20 Nov
---

- Target: [[vulnweb.com]] ([[testphp.vulnweb.com]], [[testasp.vulnweb.com]], [[testaspnet.vulnweb.com]], [[testhtml5.vulnweb.com]])
- Risk: High
- Why: No SSL certificates in crt.sh and all pages open on plain HTTP, so logins and user data are not encrypted.
- Fix: Install SSL/TLS certificates and force HTTPS redirect.
- Plan: [[Defender plan]]
