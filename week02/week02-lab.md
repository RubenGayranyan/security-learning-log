# Week 2 — Lab: Linux fundamentals

## What I did
- Configured network IP addresses for the `ubuntu-lab` and `ubuntu-srv` machines.
- Modified file permissions using `chmod` to understand read, write, and execute rights.
- Performed a defender's audit by hunting for SUID files and world-writable files across the system.
- Audited system events by filtering for `sudo` commands and failed logins in `/var/log/auth.log`.
- Scheduled an automated cron job to write timestamps to a `heartbeat.log` file every minute.
- Generated an `ed25519` SSH key pair and transferred the public key to the server using `ssh-copy-id`.

## The command that made something click
- **The command:** `find / -perm -4000 -type f 2>/dev/null`
- **What clicked:** This demonstrated how defenders can quickly list every SUID program on the system. It made me realize that by knowing the normal baseline of legitimate SUID binaries, an abnormal, malicious entry will immediately jump out during an audit.

## What broke and how I fixed it
- **What broke:** Access to my test file was completely revoked after running `chmod 000 report.txt`, resulting in a "Permission denied" error even for my own user.
- **How I fixed it:** I ran `chmod 600 report.txt` to restore owner read and write permissions, reinforcing the rule that the file owner always keeps the power to fix their own files.

## The hardening I performed
- **Action:** Disabled SSH password login on `ubuntu-srv` by setting `PasswordAuthentication no` in the `/etc/ssh/sshd_config` file and restarting the SSH service.
- **Why it matters:** It removes the ability to authenticate with a password, meaning brute-force attacks can no longer succeed. Authentication is now proven by the cryptographic key alone.
