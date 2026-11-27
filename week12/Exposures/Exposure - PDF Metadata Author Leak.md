---
type: exposure
risk: Low
found: exiftool discovery.pdf, 20 Nov
---

- Target: [[nmap.org]]
- Risk: Low
- Why: `discovery.pdf` shows author name and Word/Acrobat versions inside metadata (real name is not written here).
- Fix: Remove metadata before publishing files.
