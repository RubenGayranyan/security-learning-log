---
type: exposure
risk: Medium
found: dig TXT _dmarc, 20 Nov
---

- Targets: [[vulnweb.com]], [[nmap.org]]
- Risk: Medium
- Why: Both domains dont have a `_dmarc` TXT record, so mail servers dont know what to do with spoofed emails.
- Fix: Add `_dmarc` TXT record with..
- Plan: [[Defender plan]]
