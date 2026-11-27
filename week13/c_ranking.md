## 1. Count

* **Critical:** 13
* **High:** 9
* **Medium:** 39
* **Low:** 6

### Does it match Nessus?

**No.** OpenVAS and Nessus usually give different numbers for the same server.

* Two scanners use different vulnerability databases, different rules to check if a bug is real.

---

## 2. KEV check

1. **`CVE-2020-1938`** — *Apache Tomcat AJP RCE Vulnerability (Ghostcat)* (Port `8009/tcp`, Critical, CVSS 9.8)
2. **`CVE-2012-1823`** — *PHP < 5.3.13 / 5.4.x < 5.4.3 Multiple Vulnerabilities* (Port `80/tcp`, High, CVSS 7.5)

*`CVE-2011-2523` [vsftpd] and `CVE-2004-2687` [DistCC] are very old, so they are not in the CISA KEV list.*

---

## 3. Rank the top 10

| # | Finding | Port | CVSS | On KEV? | Reachable from? | Decision | When | Reason for Rank |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | **Apache Tomcat AJP RCE (Ghostcat)** (`CVE-2020-1938`) | 8009/tcp | 9.8 | **Yes** | Office network (all staff) | **Patch** | **Today** | It is on the KEV list (hackers really use it in real life) and lets someone take over the server. |
| 2 | **PHP-CGI Argument Injection RCE** (`CVE-2012-1823`) | 80/tcp | 7.5 | **Yes** | Office network (all staff) | **Patch** | **Today** | Even with a 7.5 score, it is on the KEV list and sits on the main web port (80), so it is very easy to attack. |
| 3 | **Possible Backdoor: Ingreslock** | 1524/tcp | 10.0 | No | Office network (all staff) | **Remove** | **Today** | It is not a real app—it is just a wide-open door that gives full admin rights to anyone in the office. |
| 4 | **vsftpd Compromised Source Backdoor** (`CVE-2011-2523`) | 21/tcp & 6200/tcp | 9.8 | No | Office network (all staff) | **Patch** | **Today** | Someone hid a secret backdoor in this FTP app that gives full control if you just type `:)` in the username. |
| 5 | **rlogin Passwordless Login** | 513/tcp | 10.0 | No | Office network (all staff) | **Remove** | **Today** | Anyone on the office Wi-Fi or network can log in with zero password, and nothing is hidden (no encryption). |
| 6 | **The rexec service is running** (`CVE-1999-0618`) | 512/tcp | 10.0 | No | Office network (all staff) | **Remove** | **Today** | This is a super old tool that lets people run commands on the server over the network in plain text. |
| 7 | **Distributed Ruby (dRuby/DRb) Multiple RCE** | 8787/tcp | 10.0 | No | Office network (all staff) | **Remove** | **This week** | Anyone in the office can send Ruby code to this port and run it on the server without logging in. |
| 8 | **MySQL / MariaDB Default Credentials** | 3306/tcp | 9.8 | No | Office network (all staff) | **Mitigate** | **This week** | The database still has default or empty passwords, so anyone in the office can open, read, or delete files. |
| 9 | **PostgreSQL Default Credentials** | 5432/tcp | 9.0 | No | Office network (all staff) | **Mitigate** | **This week** | Default passwords let anyone on the local network enter the database and even run commands on the PC. |
| 10 | **Operating System (OS) End of Life (EOL)** | general | 10.0 | No | Office network (indirect) | **Mitigate** | **Next window** | The OS is too old to get security fixes, so we should block risky access now and upgrade the system later when we have time. |
---

## 4. The Odd One

`vsftpd` service runs normally on **port 21/tcp**, but when someone logs in with a username ending in `:)`, it opens a secret root shell on **port 6200/tcp**. OpenVAS shows the finding twice because its test first finds the vulnerable FTP service on port 21 and then connects to the open backdoor shell on port 6200.