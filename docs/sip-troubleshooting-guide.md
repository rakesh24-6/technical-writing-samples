# SIP Troubleshooting Guide

This document describes common issues encountered in SIP-based communication systems and provides troubleshooting techniques.

## Common Issues

Typical SIP problems include:

* registration failures
* one-way audio
* call setup failures
* RTP media issues

## Registration Failure

Verify SIP server connectivity.

```bash
telnet sip-server-ip 5060
```

Check SIP logs on the server.

Example command:

```bash
journalctl -u sip-server
```

## Packet Capture

Capture SIP packets using tcpdump.

```bash
tcpdump -i eth0 port 5060 -n
```

Example SIP message:

```
REGISTER sip:example.com SIP/2.0
```

Verify that the server responds with:

```
200 OK
```

## RTP Media Issues

If calls connect but audio is missing, verify RTP traffic.

Capture RTP packets:

```bash
tcpdump -i eth0 udp portrange 10000-20000
```

Ensure RTP ports are open in the firewall.

## NAT Issues

Many VoIP problems occur due to NAT misconfiguration.

Solutions include:

* enabling STUN
* configuring media relay
* adjusting NAT settings on the SIP server
