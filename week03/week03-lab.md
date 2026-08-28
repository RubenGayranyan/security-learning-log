# Week 3 Lab: Windows fundamentals

## What I did
* Enumerated system users, groups, and running services using PowerShell commands like `Get-LocalUser` and `Get-Process`.
* Executed a mini-attack by creating a fake service account (`backup_svc`) and elevating it to the Administrators group.
* Used Windows Event Viewer to hunt for my own attack tracks and failed logon attempts.
* Navigated the Windows Registry safely to create and delete a temporary string value (`LabTest`).
* Wrote a custom PowerShell script (`hunt.ps1`) to list Administrators and count failed logon events.

## The attack I ran on myself, and how I found it
* I created a sneaky account named `backup_svc`, which I found in Event Viewer caught by Event ID 4720 (account created).
* I gave the account admin rights for persistence, which triggered Event ID 4732 (added to a privileged group).
* I locked my screen and entered the wrong password multiple times to generate failed logons, which I tracked down using Event ID 4625.
* I investigated successful logons (Event ID 4624) and verified the Logon Type was 2, indicating an interactive keyboard login.

## How I built my script
* I reused `Get-LocalGroupMember` from the enumeration exercise to list the admins.
* I searched the web using queries like "PowerShell get event 4625" and "PowerShell count results" to assemble the log-hunting portion of the script. 
* I had to ensure my PowerShell execution policy allowed the script to run by using `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`.

## The Linux <-> Windows link that stuck
* The comparison between Linux cron backdoors and Windows Registry Run keys made sense, as both are persistence mechanisms attackers use so malware launches at boot. 
* I also noticed how seamlessly PowerShell commands map to Linux terminal commands, like `Get-Process` mirroring `ps aux` and `Get-Service` acting like `systemctl`.
