# Linux Server Hardening Guide

This document describes recommended security practices for securing Linux servers deployed in production environments.

The procedures are applicable to most modern Linux distributions including Ubuntu Server.

## Security Objectives

The goal of server hardening is to reduce the attack surface by:

* disabling unnecessary services
* enforcing authentication policies
* restricting network access
* monitoring system activity

## System Updates

Ensure the system is regularly updated.

```bash
sudo apt update
sudo apt upgrade -y
```

## SSH Hardening

Edit the SSH configuration file.

```
/etc/ssh/sshd_config
```

Recommended settings:

```
PermitRootLogin no
PasswordAuthentication no
MaxAuthTries 3
```

Restart the SSH service.

```bash
sudo systemctl restart ssh
```

## Firewall Configuration

Enable the firewall.

```bash
sudo ufw enable
```

Allow SSH access.

```bash
sudo ufw allow 22
```

Check firewall status.

```bash
sudo ufw status
```

## Intrusion Prevention

Install fail2ban to block repeated login attempts.

```bash
sudo apt install fail2ban
```

Enable service.

```bash
sudo systemctl enable fail2ban
```

## Monitoring

Monitor system logs regularly.

```bash
journalctl -xe
```

Log analysis helps detect unauthorized activity.
