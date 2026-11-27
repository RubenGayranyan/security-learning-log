---
type: summary
found: dig, crt.sh, internetdb.shodan.io, whois, 20 Nov
---

# Exposures Summary - [[vulnweb.com]]

Sorted by risk:

1. **HIGH - [[Exposure - No HTTPS on vulnweb.com]]**
   - Why: Sites run only on HTTP with no SSL certificates, so passwords and traffic can be sniffed.
   - Fix: Add SSL certificates and redirect all HTTP traffic to HTTPS.
2. **MEDIUM - [[Exposure - Exposed Ports and Software Versions]]**
   - Why: InternetDB shows old EOL software versions (PHP 7.1.26, Apache 2.4.25, IIS 8.5) which attackers can target.
   - Fix: Update software, close unneeded ports, and hide version banners.
3. **MEDIUM - [[Exposure - Missing DMARC Policy]]**
   - Why: No `_dmarc` TXT record, so anyone can spoof emails from `vulnweb.com`.
   - Fix: Add DMARC record (`v=DMARC1; p=quarantine;` then `p=reject;`).
4. **MEDIUM - [[Exposure - Weak SPF Softfail]]**
   - Why: SPF uses `~all` (softfail), so fake emails are not strictly blocked.
   - Fix: Change `~all` to `-all` (hardfail).
5. **LOW - [[Exposure - Unsigned DNSSEC]]**
   - Why: DNSSEC is unsigned in WHOIS, so DNS replies are not protected against spoofing.
   - Fix: Turn on DNSSEC in AWS Route 53 and add DS record at Gandi.
