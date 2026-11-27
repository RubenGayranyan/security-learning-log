# Part D — Verification & Remediation Ticket

## 1. Verification with Nmap

* **Does what you see support the finding?**  
  **Yes.** The `nmap -sV -p 21 192.168.56.40` scan shows that port `21/tcp` is open and running **`vsftpd 2.3.4`**. This is the version that was hacked in 2011 to include a secret backdoor (`CVE-2011-2523`).

* **What is its QoD in the report, and what does that number tell you?**  
  The **QoD** (Quality of Detection) in the OpenVAS report is **99%**. This number tells us that the scanner is almost 100% sure the bug is real—it did not just guess from a version banner, it actually tested the backdoor safely and confirmed it works.

---

## 2. Remediation

### **Host + port**
* **Host:** `192.168.56.40` (Metasploitable server on the office network)
* **Port:** `21/tcp` (and `6200/tcp` when the backdoor opens)

### **Finding + CVE**
* **Finding:** vsftpd Compromised Source Packages Backdoor Vulnerability
* **CVE:** `CVE-2011-2523` (CVSS 9.8 — Critical)

### **Priority + why**
* **Priority:** **Critical — Fix Today**
* **Why:** Anyone in the office network can reach port 21 and enter to the hidden backdoor just by typing `:)` at the end of a username. This opens a root shell on port 6200 and gives the attacker full admin control of the whole server without a password.

### **Fix + how to check**
* **Fix:** Remove the infected `vsftpd 2.3.4` package and install a clean, updated version from the official repository, or it's better to switch to SFTP over SSH and turn off FTP completely.
* **How to check:** 
  1. Run `nmap -sV -p 21,6200 192.168.56.40` to make sure `vsftpd 2.3.4` is gone (showing a safe version or closed port) and port `6200` is closed.
  2. Re-run the **OpenVAS** scan against `192.168.56.40` to confirm that `CVE-2011-2523` no longer appears in the report.