# Week 5 — Lab: firewall and segmentation

## The host firewall
- Configured default incoming traffic to be blocked (`default deny incoming`) and explicitly allowed port 22 for SSH before enabling the firewall on `ubuntu-srv`.
- Verified that allowed SSH connections succeeded, while attempts to reach unallowed ports (such as port 8080) were successfully blocked.

## Segmentation
- Split the virtual network into two isolated segments (`labnet` and `labnet2`) using VirtualBox internal networks.
- Assigned machines addresses in different subnets (`192.168.10.10/24` and `192.168.20.20/24`), ensuring they could not reach each other directly because they were on separate segments without a connecting path.

## The gateway
- Configured `ubuntu-srv` with two network cards connected to both segments (`192.168.10.1` and `192.168.20.1`) to act as a bridge.
- Pointed the client machines to the gateway using static routes (`ip route`) and enabled IP forwarding (`net.ipv4.ip_forward=1`) on `ubuntu-srv` so it could pass traffic between the two segments.

## Controlling the crossing with ufw
- Blocked forwarded traffic by default on the gateway using `sudo ufw default deny routed`.
- Added a specific rule allowing only TCP traffic on port 22 between the subnets (`sudo ufw route allow proto tcp from 192.168.10.0/24 to 192.168.20.0/24 port 22`), proving that SSH traffic could cross the gateway while ping traffic remained blocked.

## What broke and how I fixed it
- *(Add any specific issues encountered during the lab, such as interface naming differences or gateway configuration mistakes here).*
