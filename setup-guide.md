# Mini SOC Lab Setup Guide

## Lab Goal

The goal of this lab is to simulate a small SOC environment where endpoint and network logs are collected, analyzed, and used for threat detection and incident response practice.

This lab is being built step by step for cybersecurity internship preparation.

## Planned Lab Components

| Component | Purpose | Status |
|---|---|---|
| Ubuntu Test Machine | Generate test activity and practice Linux/security commands | Completed |
| Wazuh Server | SIEM/XDR dashboard and alert analysis | Planned |
| Windows Endpoint | Collect Windows event logs | Planned |
| Suricata IDS | Network intrusion detection | Planned |
| Wireshark | Manual packet analysis | Installed on host machine |
| Nmap | Generate safe scan activity for detection practice | Installed |
| OpenSSH Server | Practice SSH access and failed login detection | Installed |

## Current Completed Setup

The first Ubuntu test machine has been created successfully in Oracle VirtualBox.

Completed work:

- Ubuntu 24.04.4 LTS installed
- VM configured with 4096 MB RAM and 2 processors
- NAT networking verified
- Basic tools installed: `nmap`, `net-tools`, `curl`, `git`, `openssh-server`
- SSH socket verified on port 22
- VirtualBox snapshots created for recovery
- Setup screenshots documented

Detailed documentation:

- [Day 02 – Ubuntu VM Setup](docs/day-02-ubuntu-vm-setup.md)

## Planned Network Design

The current Ubuntu test machine uses NAT networking for internet access.

For the full SOC lab, a host-only lab network will be added later so that lab traffic stays inside the virtual environment.

Planned IP address structure:

| Machine | Planned IP Address | Role |
|---|---|---|
| Wazuh Server | 192.168.56.10 | SIEM/XDR server |
| Ubuntu Test Machine | 192.168.56.20 | Test/attacker machine |
| Windows Endpoint | 192.168.56.30 | Endpoint/victim machine |

## Planned Detection Scenarios

The lab will later be used to test and document these detection scenarios:

1. Nmap port scan detection
2. Failed SSH login / brute-force attempt detection
3. Suspicious command execution
4. Suricata network alert
5. Safe malware test file detection using EICAR

## Setup Status

- [x] GitHub repository created
- [x] Ubuntu test machine created
- [x] Ubuntu test machine updated
- [x] Basic tools installed on Ubuntu test machine
- [x] SSH socket enabled and verified
- [x] VirtualBox snapshots created
- [ ] Host-only network configured
- [ ] Wazuh server installed
- [ ] Windows endpoint created
- [ ] Suricata installed
- [ ] Wazuh agent installed
- [ ] First alert generated
- [ ] First incident report written

## Setup Progress Logs

- [Day 02 – Ubuntu VM Setup](docs/day-02-ubuntu-vm-setup.md)

## Next Steps

1. Decide whether the laptop can handle a local Wazuh server VM.
2. Configure host-only networking for lab communication.
3. Create the Wazuh server VM or choose a lighter alternative.
4. Connect the Ubuntu test machine to the SOC lab network.
5. Generate the first test activity and document the first alert.