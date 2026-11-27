---
type: defender-plan
found: analysis of vulnweb.com, 20 Nov
---

# Defender Plan - [[vulnweb.com]]

Top 3 fixes for [[vulnweb.com]] by priority:

1. **Turn on HTTPS for all domains and subdomains (High)**
   - Fixes: [[Exposure - No HTTPS on vulnweb.com]]
   - Add SSL certificates (for example Let's Encrypt or AWS) for main domain and all subdomains, and redirect http to https.

2. **Update old software and close unused ports (Medium)**
   - Fixes: [[Exposure - Exposed Ports and Software Versions]]
   - Update EOL software like PHP 7.1, Apache 2.4.25 and IIS 8.5, and hide version numbers in server headers.

3. **Add DMARC and make SPF stricter (Medium)**
   - Fixes: [[Exposure - Missing DMARC Policy]] and [[Exposure - Weak SPF Softfail]]
   - Create `_dmarc` TXT record with `p=quarantine` or `p=reject`, and change SPF from `~all` to `-all` so fake emails get blocked.
