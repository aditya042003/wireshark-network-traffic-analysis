# Wireshark Network Traffic Analysis

## 1. Project Overview

This project documents a practical network traffic analysis exercise using Wireshark on Windows 11. The capture was inspected with DNS, TCP, and HTTP display filters to understand common protocols, packet fields, and connection behavior.

## 2. Objectives

- Capture and review network packets.
- Inspect DNS queries and responses.
- Examine TCP traffic and connection setup flags.
- Identify source and destination IP addresses and port numbers.
- Recognize HTTP responses and TLS traffic.
- Save the capture for repeatable analysis.

## 3. Tools and Environment

- **Operating system:** Windows 11
- **Packet analyzer:** Wireshark
- **Capture driver:** Npcap
- **Command-line utility:** `nslookup`

## 4. Practical Steps Completed

1. Installed Wireshark and Npcap.
2. Captured traffic on the Wi-Fi interface.
3. Ran `nslookup example.com`.
4. Applied the `dns` display filter.
5. Applied the `tcp` display filter.
6. Inspected SYN packets using `tcp.flags.syn == 1`.
7. Reviewed packet details, including IP addresses, TCP/UDP fields, ports, and protocol information.
8. Saved the capture as `network_traffic_analysis.pcapng`.

## 5. Observed Results

The following counts and observations are taken from the Wireshark screenshots captured during this exercise.

| Item | Observed result |
|---|---|
| Capture file | `network_traffic_analysis.pcapng` |
| Total packets in capture | 293,148 |
| DNS filter | 954 displayed packets (0.3%) |
| TCP filter | 282,958 displayed packets (96.5%) |
| HTTP filter | 696 displayed packets (0.2%) |
| DNS activity | DNS queries and responses were visible, including A/AAAA lookups and CNAME-related responses |
| TCP activity | TCP SYN, SYN/ACK, ACK, FIN/ACK, and a TCP RST/ACK packet were visible |
| Encrypted application traffic | TLS 1.2 traffic over port 443 was visible |
| HTTP activity | HTTP GET requests and `HTTP/1.1 206 Partial Content` responses were visible |

*Display percentages are rounded as shown in Wireshark. Filter counts describe packets matching each display filter in this capture; they are not mutually exclusive protocol totals.*

## 6. Interpretation

- **DNS:** The capture contains DNS requests and responses. DNS records such as A, AAAA, and CNAME help clients resolve names to addresses or aliases.
- **TCP:** The capture includes connection-establishment and connection-closure traffic. A SYN packet is used to initiate a TCP connection; SYN/ACK is a typical response during the handshake.
- **TLS:** Traffic using port 443 and identified as TLS 1.2 was visible. Encrypted application payloads generally cannot be interpreted as ordinary readable HTTP without appropriate decryption material.
- **HTTP:** The capture includes GET requests and `206 Partial Content` responses. A 206 response indicates that the server returned a requested portion of a resource.
- **TCP reset:** A RST/ACK packet was visible. A reset can occur for several legitimate reasons and, by itself, does not establish malicious activity.

## 7. Security and Privacy Notes

This is a learning exercise, not a confirmed threat-detection report. The screenshots do not establish that an attack occurred. Any suspicious-traffic conclusion would require additional context and corroborating evidence.

Packet captures can contain IP addresses, hostnames, URLs, and other sensitive information. Review and sanitize the capture before sharing it publicly. Do not upload raw captures containing private or confidential traffic to a public repository.

## 8. Project Files

- `README.md` — Project documentation
- `network_traffic_analysis.pcapng` — Local packet capture (keep private unless reviewed and sanitized)

## 9. Key Learnings

- Starting a packet capture and saving it in PCAPNG format
- Applying Wireshark display filters
- Reviewing DNS queries and responses
- Recognizing TCP SYN/SYN-ACK and connection-closure packets
- Identifying HTTP partial-content responses and TLS traffic
- Interpreting packet evidence cautiously rather than assuming a security incident

## 10. Conclusion

This exercise provided hands-on practice with packet capture, DNS and TCP filtering, packet-detail inspection, and basic protocol interpretation. It establishes a foundation for further network troubleshooting and entry-level SOC analysis.

## 11. Possible Next Steps

- Record the exact SYN-only filter count using `tcp.flags.syn == 1 && tcp.flags.ack == 0`.
- Inspect selected DNS transactions and record a few examples without exposing sensitive details.
- Add sanitized screenshots of the DNS, TCP, and HTTP filters.
- Compare related packets using **Follow → TCP Stream** only when appropriate and safe.
