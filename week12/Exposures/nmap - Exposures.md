---
type: summary
found: dig, whois, exiftool, internetdb.shodan.io, 20 Nov
---

# Exposures Summary - [[nmap.org]]

Sorted by risk:

1. **MEDIUM - [[Exposure - Missing DMARC Policy]]**
   - Why: No `_dmarc.nmap.org` record, so attackers can spoof emails from this domain.
   - Fix: Add a DMARC TXT record (`p=quarantine` or `p=reject`).
2. **MEDIUM - [[Exposure - Weak SPF Softfail]]**
   - Why: SPF ends with `~all` (softfail) and uses old `ptr` option.
   - Fix: Remove `ptr` and change `~all` to `-all`.
3. **MEDIUM - [[Exposure - Exposed Ports and Software Versions]]**
   - Why: InternetDB shows open ports and old versions like Apache 2.4.6 / 2.4.7 and OpenSSH 6.6.1p1 on [[50.116.1.184]] and [[45.33.32.156]].
   - Fix: Update server software, hide version banners, and limit open ports on main server.
4. **LOW - [[Exposure - PDF Metadata Author Leak]]**
   - Why: `discovery.pdf` leaks author name and software info in metadata.
   - Fix: Clean metadata with `exiftool -all=` before uploading PDFs.
5. **LOW - [[Exposure - Unsigned DNSSEC]]**
   - Why: DNSSEC is unsigned in WHOIS.
   - Fix: Turn on DNSSEC at Linode and add DS records at Dynadot.
