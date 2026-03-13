# SIP Debugging Handbook

Practical Guide for Telecom Platform Engineers

## Overview

This document describes systematic techniques for debugging issues in SIP-based communication platforms.

The guide focuses on real-world production troubleshooting scenarios including:

* SIP registration failures
* call setup errors
* RTP audio problems
* NAT traversal issues
* signaling routing errors

The troubleshooting workflow described here is applicable to VoIP platforms built on Linux infrastructure.

---

# SIP Protocol Overview

SIP (Session Initiation Protocol) is used to establish, modify, and terminate multimedia sessions.

Typical SIP operations include:

* REGISTER – user registration
* INVITE – call initiation
* ACK – call confirmation
* BYE – call termination
* OPTIONS – capability query

Example SIP request:

```
REGISTER sip:example.com SIP/2.0
Via: SIP/2.0/UDP 192.168.1.10
From: <sip:user@example.com>
To: <sip:user@example.com>
Call-ID: 123456789
CSeq: 1 REGISTER
```

Successful registration response:

```
SIP/2.0 200 OK
```

---

# SIP Troubleshooting Workflow

When debugging SIP issues follow a structured approach.

## Step 1 — Verify Network Connectivity

Confirm that the SIP server is reachable.

```
ping sip-server-ip
```

Verify SIP port availability.

```
telnet sip-server-ip 5060
```

Expected result:

```
Connected to sip-server-ip
```

---

## Step 2 — Check Service Status

Verify that SIP services are running.

```
systemctl status kamailio
systemctl status asterisk
systemctl status rtpengine
```

Look for:

* failed services
* configuration errors
* port conflicts

---

# Packet Capture Analysis

Packet capture is the most effective way to diagnose SIP issues.

## Capture SIP Traffic

```
tcpdump -i eth0 port 5060 -n
```

Example captured packet:

```
INVITE sip:1002@example.com SIP/2.0
```

Verify that responses are returned:

```
100 Trying
180 Ringing
200 OK
```

---

# SIP Call Flow Debugging

Typical call establishment sequence:

```
Caller      Proxy        PBX        Callee
  |           |           |           |
  | INVITE    |           |           |
  |---------->|           |           |
  |           | INVITE    |           |
  |           |---------->|           |
  |           |           | INVITE    |
  |           |           |---------->|
  |           |           |           |
  |           |           | 180 Ring  |
  |           |<----------|           |
  |<----------|           |           |
  |           |           |           |
  |           |           | 200 OK    |
  |<----------|<----------|           |
  | ACK       |           |           |
  |---------->|---------->|---------->|
```

Any missing response indicates where the signaling path is failing.

---

# RTP Media Debugging

If a call connects but audio is missing, the problem is usually related to RTP.

## Capture RTP Packets

```
tcpdump -i eth0 udp portrange 10000-20000
```

Verify that RTP packets are flowing in both directions.

Example RTP packet:

```
RTP version 2
Payload type: PCMU
Sequence number: 24501
```

---

# One-Way Audio Diagnosis

One-way audio typically occurs due to:

* NAT misconfiguration
* firewall blocking RTP ports
* incorrect SDP media address

Check the SDP body inside SIP messages.

Example:

```
c=IN IP4 192.168.1.50
m=audio 16384 RTP/AVP 0
```

If the IP address is private but the endpoint is external, RTP may fail.

---

# NAT Traversal Issues

Common NAT problems include:

* incorrect contact headers
* unreachable RTP ports
* private IP addresses in SDP

Solutions:

* enable media relay
* configure STUN/TURN
* use RTP proxying

---

# Log Analysis

Application logs often provide valuable debugging information.

Example log sources:

```
/var/log/syslog
/var/log/asterisk/messages
```

Search logs for SIP errors.

```
grep SIP /var/log/syslog
```

---

# Advanced Debugging Tools

Professional VoIP debugging frequently uses the following tools:

| Tool      | Purpose                |
| --------- | ---------------------- |
| tcpdump   | packet capture         |
| Wireshark | SIP and RTP analysis   |
| sngrep    | SIP call visualization |
| ngrep     | SIP text filtering     |

Example SIP capture using sngrep:

```
sngrep port 5060
```

This tool displays live SIP call flows.

---

# Best Practices

Effective troubleshooting requires:

* structured debugging workflow
* packet capture analysis
* log inspection
* configuration validation

Avoid modifying multiple variables simultaneously during debugging.

Always test one change at a time.

---

# Conclusion

SIP troubleshooting requires understanding both signaling and media flow.

Successful debugging depends on:

* analyzing SIP messages
* verifying RTP media streams
* identifying NAT and firewall issues

Engineers working with telecom platforms must combine network diagnostics with SIP protocol analysis to resolve production issues efficiently.
