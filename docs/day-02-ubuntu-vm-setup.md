# Day 02 – Ubuntu VM Setup

## Objective

Set up an Ubuntu virtual machine in VirtualBox for cybersecurity lab practice.

## VM Configuration

| Setting | Value |
|---|---|
| Virtualization software | Oracle VirtualBox |
| Guest OS | Ubuntu 24.04.4 LTS |
| RAM | 4096 MB |
| CPU | 2 processors |
| Disk | 25 GB virtual disk |
| Network | NAT |
| Video memory | 128 MB |
| Graphics controller | VBoxSVGA |

## Installation Summary

Ubuntu was installed manually using the interactive installer.

Selected options:

- Ubuntu 24.04.4 LTS Desktop ISO
- Interactive installation
- Default application selection
- No third-party proprietary software
- Erase disk and install Ubuntu inside the VirtualBox virtual disk

The “Erase disk” option applied only to the VM’s virtual disk, not the host Windows system.

## Display Issue and Fix

During the initial setup, the VM showed a black screen after boot/login.  
The issue was fixed by changing VirtualBox display settings and using the working graphics configuration.

Final working setup:

- Video memory: 128 MB
- 3D acceleration: disabled
- Stable display configuration saved as a VirtualBox snapshot

## Installed Tools

The following tools were installed:

```bash
sudo apt install nmap net-tools curl git openssh-server -y
```

Verified tools:

```bash
nmap --version
git --version
curl --version
```

## Network Verification

The VM network interface was checked using:

```bash
ip a
```

The VM received a NAT IP address from VirtualBox.

## SSH Verification

SSH socket was enabled and verified using:

```bash
systemctl status --no-pager ssh.socket
sudo ss -tlnp | grep :22
```

SSH was listening on port 22.

## Snapshots Created

VirtualBox snapshots created:

1. Clean Ubuntu setup
2. Ubuntu with basic tools
3. Stable display working

## Screenshots

### VirtualBox VM Details

![VirtualBox VM Details](../screenshots/day-02-ubuntu-vm-setup/01-virtualbox-vm-details.png)

### Working Display Settings

![Working Display Settings](../screenshots/day-02-ubuntu-vm-setup/02-display-settings-working.png)

### Ubuntu Desktop Running

![Ubuntu Desktop Running](../screenshots/day-02-ubuntu-vm-setup/03-ubuntu-desktop-running.png)

### Ubuntu Version

![Ubuntu Version](../screenshots/day-02-ubuntu-vm-setup/04-ubuntu-version.png)

### Basic Tools Installed

![Basic Tools Installed](../screenshots/day-02-ubuntu-vm-setup/05-basic-tools-installed.png)

### Network Interface

![Network Interface](../screenshots/day-02-ubuntu-vm-setup/06-network-interface.png)

### SSH Socket Active

![SSH Socket Active](../screenshots/day-02-ubuntu-vm-setup/07-ssh-socket-active.png)

### VirtualBox Snapshots

![VirtualBox Snapshots](../screenshots/day-02-ubuntu-vm-setup/08-virtualbox-snapshots.png)