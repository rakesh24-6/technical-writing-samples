# User Manual Example

This document demonstrates the structure of a typical software user manual.

## Introduction

This manual explains how to install, configure, and use the application.

## System Requirements

Minimum requirements:

CPU: 2 cores
RAM: 4 GB
Disk: 10 GB

Supported operating systems:

Linux
macOS
Windows

## Installation

Download the application package and run the installer.

Example on Linux:

```
sudo apt install example-application
```

## Configuration

Configuration file location:

```
/etc/example/application.conf
```

Example configuration:

```
port=8080
log_level=info
```

## Using the Application

Start the service:

```
systemctl start example
```

Access the web interface:

```
http://localhost:8080
```

## Stopping the Application

```
systemctl stop example
```
