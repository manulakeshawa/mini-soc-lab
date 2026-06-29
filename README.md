# Mini SOC Lab: Threat Detection and Incident Response

## Overview
This project is a beginner SOC home lab designed to practice security monitoring, log analysis, threat detection, and incident response using open-source tools.

The lab focuses on collecting logs from Linux/Windows endpoints, detecting suspicious activity, analyzing alerts, and writing simple incident reports.

## Objectives
- Build a small SOC-style lab environment.
- Collect logs from endpoints.
- Detect suspicious activity such as port scans and failed login attempts.
- Analyze alerts using a SIEM.
- Document findings through incident reports.
- Improve practical cybersecurity skills for internship preparation.

## Tools Planned
- Wazuh SIEM/XDR
- Ubuntu Linux
- Windows endpoint
- Suricata IDS
- Wireshark
- Nmap
- GitHub documentation

## Planned Detection Scenarios
1. Nmap port scan detection
2. Failed login / brute-force attempt detection
3. Suspicious command execution
4. Basic network traffic analysis
5. Safe malware test file detection using EICAR

## Lab Architecture
Architecture diagram will be added after the lab environment is finalized.

## Status
Project setup in progress.

## Lab Progress

### Day 02 – Ubuntu VM Setup

Completed Ubuntu VM setup using Oracle VirtualBox.

Configured and verified:

- Ubuntu 24.04.4 LTS VM
- 4096 MB RAM and 2 processors
- NAT networking
- Basic cybersecurity tools: nmap, git, curl, net-tools
- OpenSSH server socket listening on port 22
- VirtualBox snapshots for recovery

Documentation: [Day 02 – Ubuntu VM Setup](docs/day-02-ubuntu-vm-setup.md)