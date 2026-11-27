---
type: exposure
risk: Medium
found: dig TXT, 20 Nov
---

- Targets: [[vulnweb.com]], [[nmap.org]]
- Risk: Medium
- Why: Both domains use `~all` (softfail) instead of `-all` (hardfail), and nmap.org also uses `ptr`.
- Fix: Remove `ptr` and switch `~all` to `-all`.
- Plan: [[Defender plan]]
