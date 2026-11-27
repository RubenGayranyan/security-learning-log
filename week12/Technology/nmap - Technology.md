---
type: technology
found: whois, dig NS, nslookup MX, internetdb.shodan.io, exiftool, 20 Nov
---

# Technology Summary - [[nmap.org]]

- DNS provider: Linode (`ns1..5.linode.com`)
- Mail provider: Google
- Hosting: Linode / Akamai ([[50.116.1.184]], [[45.33.32.156]])
- Web servers and software (from InternetDB):
  - [[50.116.1.184]]: Apache 2.4.6, OpenSSH 7.4, Postfix, CentOS (ports 22, 25, 80, 443)
  - [[45.33.32.156]]: Apache 2.4.7, OpenSSH 6.6.1p1, NTP 3, Ubuntu Linux (ports 22, 80, 123, 9929)
- PDF creation software (`exiftool discovery.pdf`):
  - Creator: Microsoft Word 10.0
  - Producer: Acrobat Distiller 4.0 for Windows
  - Create Date: 2002-11-13 20:57:17
  - Author field is also filled (name not included here, see [[Exposure - PDF Metadata Author Leak]])
