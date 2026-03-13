# Installation Guide Example

This guide explains how to install the application on a Linux server.

## Step 1: Update System

```
sudo apt update
sudo apt upgrade -y
```

## Step 2: Install Dependencies

```
sudo apt install git nginx
```

## Step 3: Install Application

```
git clone https://github.com/example/application
cd application
make install
```

## Step 4: Start Service

```
systemctl start application
```

## Step 5: Verify Installation

```
systemctl status application
```
