# Week 4 Lab: networking in action

## What I captured and saw
* Captured live network packets on the `enp0s3` interface using Wireshark.
* Expanded individual ICMP packets to inspect the encapsulation layers: Ethernet II for Link layer MAC addresses, Internet Protocol for Network layer IP addresses, and ICMP for the ping data.
* Applied display filters such as `icmp`, `arp`, `ip.addr == 192.168.56.11`, and `tcp.port == 22` to isolate specific protocols and conversations out of the network noise.

## The cleartext password moment
* Applied the `telnet` filter and used the "Follow TCP Stream" function to view the entire login conversation.
* Observed the credentials `labuser` and `Cleartext123` sitting completely visible in plain, readable text.
* Telnet is dangerous because it sends data with no protection, allowing anyone capturing the network traffic to read it.
* SSH is safe because the traffic appears as scrambled, unreadable bytes in the TCP stream, demonstrating encryption protecting the login.

## DNS and ARP
* Used `nslookup` and `dig` to watch domain names resolve into IPs, viewing `A` records for IPv4, `AAAA` records for IPv6, and `MX` records for mail servers.
* Captured live DNS query and response packets in Wireshark to see the lookup happen in milliseconds.
* Ran `ip neigh` and `arp -a` to view the ARP table, mapping IP addresses to the physical MAC addresses of devices the machine had talked to on the local network.
* Captured a live ARP exchange, viewing the broadcast request ("Who has 192.168.56.11?") and the targeted reply with the MAC address.

## The investigation (lab4_investigation.pcap)
* **Recon:** The attacker rapidly mapped the local network using a sweep of ARP requests to discover live targets.
* **Port scan:** The attacker then launched a fast TCP SYN scan against 192.168.1.7 to identify open ports and services (135, 139, 445, 3389, and 5357).
* **ARP spoofing:** By sending fake ARP replies, the attacker claimed the gateway's IP address (192.168.1.1) to position themselves as a Man-in-the-Middle and intercept traffic.
* **Stolen credentials:** From their MITM position, the attacker captured an unencrypted Telnet session and read the `admin` username and password (`Sup3rSecret!`) in plain text.
* **Post-exploitation (what they ran after login):** Immediately after logging in, the attacker read the `/etc/shadow` file to extract the password hashes for all system users.
* **The story in my own words:** The attacker started by sweeping the network with ARP requests to find active hosts, then executed a port scan on their chosen target to see what services were running. Next, they deployed an ARP spoofing attack to impersonate the network gateway, effectively placing themselves in the middle of the victim's communications. This allowed them to intercept a highly insecure Telnet session and steal an admin password in plain text. Finally, using those stolen credentials to log into the machine, the attacker extracted the system's entire password hash list, escalating the breach to a full system compromise.

## What broke and how I fixed it
* *If Wireshark showed no packets or interfaces:* I ran it with capture rights using `sudo wireshark`.
* *If the ping to the server failed:* I realized the IPs reset on reboot and restored them using `sudo ip addr add 192.168.56.x/24 dev enp0s3`, ensuring I included the `/24` subnet.
* *If the ARP table was empty:* I pinged a neighbor device first, since the machine's table only remembers devices it has recently communicated with.
