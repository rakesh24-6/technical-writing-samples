# Troubleshooting Guide

This guide describes common issues and their solutions.

## Service Does Not Start

Check service status:

```
systemctl status application
```

Review logs:

```
journalctl -u application
```

## Network Connection Issues

Verify open ports:

```
ss -lntup
```

Check firewall rules:

```
ufw status
```

## Configuration Errors

Validate configuration file:

```
application --check-config
```
