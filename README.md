# Network Forensics Investigation: NetSupport RAT Infection

Analysis of a real malware infection from network traffic alone, using Wireshark. The full write-up is in **[NetSupport_RAT_Incident_Report.pdf](NetSupport_RAT_Incident_Report.pdf)**.

## Summary

A Windows client on a small Active Directory network was infected with **NetSupport Manager RAT**, a remote access trojan. Starting from a single alerted IP address, I identified the infected computer and its user, confirmed the malware family, and documented its command-and-control (C2) activity.

| Finding | Value |
| --- | --- |
| Infected host IP | 10.2.28.88 |
| MAC address | 00:19:d1:b2:4d:ad |
| Hostname | DESKTOP-TEYQ2NR |
| User account | brolf (Becka Rolf) |
| C2 server | 45.131.214.85 (TCP 443) |
| First C2 contact | 2026-02-28 19:55:51 UTC |

## Key findings

- **Malware confirmed by name:** C2 requests carried the HTTP User-Agent `NetSupport Manager/1.3`.
- **Unencrypted HTTP on port 443:** traffic to a port normally used for HTTPS, a common way to blend in.
- **Regular beaconing:** the host checked in with the attacker about every 60 seconds.
- **User identified through Windows protocols:** username from Kerberos, full name from SAMR traffic to the domain controller.

## Skills demonstrated

- Packet analysis with Wireshark display filters
- Host and user identification from DHCP/NBNS/Browser, Kerberos, and SAMR traffic
- Indicator of compromise (IOC) extraction and timeline reconstruction
- Evidence integrity with SHA-256 hashing
- Incident report writing

## Evidence

- **Source:** [Malware-Traffic-Analysis.net, 2026-02-28 exercise "Easy As 123"](https://www.malware-traffic-analysis.net/2026/02/28/index.html)
- **SHA-256 (pcap):** `3dc470f5490ec15b4024c513e87c67e0b17caeae2a2ce3d83541be24ef407e61`
- **Tools:** Wireshark, shasum (macOS)

The packet capture itself is not included in this repository because it contains live malware traffic. It can be downloaded from the source above.
