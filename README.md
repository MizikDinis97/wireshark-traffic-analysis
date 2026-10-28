# Wireshark lab analyzing ICMP traffic, DNS resolution, TCP handshakes, and HTTP requests, with packet captures and documented findings.


# Wireshark Traffic Analysis Lab

## Overview

In this lab, I captured and analyzed traffic generated on my Windows
computer using Wireshark. I examined ICMP requests and replies,
DNS queries and responses, and a TCP connection carrying HTTP traffic.

## Tools

- Wireshark
- Windows Command Prompt
- ping, nslookup, and curl

## 1. ICMP Analysis

### Command

```text
ping -4 -n 4 1.1.1.1
```

### Display Filter

```text
icmp && ip.addr == 1.1.1.1
```

### Findings

- Captured four Echo Requests and four Echo Replies.
- Identified ICMP Type 8 as Echo Request and Type 0 as Echo Reply.
- Matched requests and replies using identifiers and sequence numbers.
- Inspected the 32-byte ICMP payload.
- Observed a round-trip time of approximately 41.855 ms for one pair.

Capture: [icmp-filtered.pcapng](icmp-filtered.pcapng)

## 2. DNS Analysis

### Command

```text
nslookup example.com 1.1.1.1
```

### Display Filter

```text
dns.qry.name == "example.com"
```

### Findings

- Examined A queries for IPv4 and AAAA queries for IPv6.
- Matched a query and response using transaction ID 0x0006.
- The A response returned 172.66.147.243 and 104.20.23.154.
- The response indicated No error and contained two answer records.
- Observed a response time of approximately 74.303 ms for the A query.

Capture: [dns-filtered.pcapng](dns-filtered.pcapng)

## 3. TCP and HTTP Analysis

### Command

```text
curl.exe --http1.1 -I http://example.com
```

### Findings

- Identified the TCP three-way handshake in packets 1, 2, and 3:
  SYN → SYN-ACK → ACK.
- The client used source port 62540 and connected to server port 80.
- Inspected TCP flags and relative sequence and acknowledgment numbers.
- Packet 4 contained the HTTP HEAD request.
- Packet 6 contained the HTTP 200 OK response.
- Packets 7–9 showed connection termination using FIN and ACK flags.

Capture: [tcp-http-analysis.pcapng](tcp-http-analysis.pcapng)

## How to View

Download a .pcapng file and open it in Wireshark.
The uploaded captures contain only the packets selected for this lab.

Packet numbers refer to the exported captures. Earlier screenshots
may show the original packet numbers before export.

## Skills Practised

- Capturing and filtering network traffic
- Analyzing ICMP and DNS exchanges
- Identifying TCP connection establishment and termination
- Reading TCP flags, ports, sequence numbers, and acknowledgments
- Inspecting HTTP requests and responses
- Documenting findings from packet captures
