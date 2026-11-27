---
type: summary
found: whois, dig, nslookup, crt.sh, theHarvester, Google, Shodan, 20 Nov
---

# Names & IPs Summary - [[nmap.org]]

## Confirmed domains and subdomains
- [[nmap.org]] -> [[50.116.1.184]]
- [[svn.nmap.org]] -> [[50.116.1.184]]
- [[issues.nmap.org]] -> [[50.116.1.184]]
- [[scanme.nmap.org]] -> [[45.33.32.156]]
- [[chat.nmap.org]] -> [[45.33.32.156]]

## Shared IPs
- [[50.116.1.184]] has [[nmap.org]], [[svn.nmap.org]], [[issues.nmap.org]] and many other domains (sectools, seclists, npcap, insecure.com). Also used for wildcard `*.nmap.org`.
- [[45.33.32.156]] has [[scanme.nmap.org]] and [[chat.nmap.org]].

## Wildcard check
- `dig +short this-does-not-exist-123.nmap.org` returned [[50.116.1.184]].
- Because of wildcard DNS, we cant trust only dig or theHarvester for names on 50.116.1.184. We need another proof like crt.sh. Other names are in [[unconfirmed names]].
