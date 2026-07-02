# Mini SOC Lab: Threat Detection and Incident Response

## Overview

This project is a beginner-friendly SOC home lab designed to practice security monitoring, log analysis, threat detection, and incident response using open-source tools.

The lab focuses on collecting logs from Linux/Windows endpoints, detecting suspicious activity, analyzing alerts, and documenting findings through incident reports.

## Objectives

* Build a small SOC-style lab environment.
* Collect logs from endpoints.
* Detect suspicious activity such as port scans and failed login attempts.
* Analyze alerts using a SIEM/XDR platform.
* Document findings through incident reports.
* Improve practical cybersecurity skills for internship preparation.

## Tools Used / Planned

| Tool                       | Purpose                                                 | Status            |
|----------------------------|---------------------------------------------------------|-------------------|
| Oracle VirtualBox          | Virtual lab environment                                 | In use            |
| Ubuntu Desktop 24.04.4 LTS | Ubuntu test machine                                     | Completed         |
| Ubuntu Scanner VM          | Dedicated scanner machine for safe Nmap testing         | Completed         |
| Ubuntu Server 24.04.4 LTS  | Wazuh server base OS                                    | Completed         |
| Wazuh SIEM/XDR             | Log collection, alert analysis, and security monitoring | Installed         |
| Nmap                       | Safe scan activity and network testing                  | Installed         |
| OpenSSH Server             | SSH access and failed login detection practice          | Installed         |
| Wireshark                  | Manual packet analysis                                  | Installed on host |
| Suricata IDS               | Network intrusion detection                             | Planned           |
| Windows Endpoint           | Windows event log collection                            | Planned           |

## Lab Architecture

| Machine             | IP Address            | Purpose                                    | Status         |
|---------------------|-----------------------|--------------------------------------------|----------------|
| Wazuh Server        | 192.168.56.10         | SIEM/XDR dashboard and log analysis        | Installed      |
| Ubuntu Test Machine | 192.168.56.20         | Monitored Ubuntu endpoint and scan target  | Agent enrolled |
| Ubuntu Scanner      | 192.168.56.40         | Dedicated scanner machine for Nmap testing | Created        |
| Windows Endpoint    | 192.168.56.30 planned | Windows event log collection               | Planned        |

Architecture diagram will be updated as the lab environment is completed.

## Planned Detection Scenarios

| Scenario                                  | Status                 |
|-------------------------------------------|------------------------|
| Wazuh server setup                        | Completed              |
| Ubuntu endpoint agent enrollment          | Completed              |
| Nmap port scan detection                  | Completed              |
| Failed SSH login / brute-force detection  | Completed              |
| Suspicious command execution              | Completed              |
| Safe malware test detection using EICAR   | Completed / Documented |
| Suricata network alert analysis           | Planned                |

## Lab Progress

### Day 02 – Ubuntu VM Setup

Completed Ubuntu test machine setup using Oracle VirtualBox.

Configured and verified:

* Ubuntu 24.04.4 LTS VM
* 4096 MB RAM and 2 processors
* NAT networking
* Basic cybersecurity tools: `nmap`, `git`, `curl`, `net-tools`
* OpenSSH server socket listening on port 22
* VirtualBox snapshots for recovery

Documentation: [Day 02 – Ubuntu VM Setup](docs/day-02-ubuntu-vm-setup.md)

### Day 03 – Wazuh Server Setup

Completed Wazuh server installation using Ubuntu Server 24.04.4 LTS.

Configured and verified:

* Wazuh Server VM in Oracle VirtualBox
* 8192 MB RAM and 4 processors
* 50 GB virtual disk
* NAT networking for internet access
* Host-only IP address: `192.168.56.10`
* Wazuh installation completed successfully
* Wazuh services verified:

  * `wazuh-manager.service`
  * `wazuh-indexer.service`
  * `wazuh-dashboard.service`
  * `filebeat.service`
* Wazuh dashboard accessed from the Windows host browser
* Admin password saved privately and not uploaded to GitHub
* VirtualBox snapshot created after successful Wazuh installation

Documentation: [Day 03 – Wazuh Server Setup](docs/day-03-wazuh-server-setup.md)

### Day 04 – Ubuntu Agent Enrollment

Completed Ubuntu Test Machine enrollment as a Wazuh agent.

Configured and verified:

- Host-only network configured on Ubuntu Test Machine
- Ubuntu Test Machine assigned static IP address: `192.168.56.20`
- Wazuh Server reachable at `192.168.56.10`
- Wazuh agent installed on Ubuntu Test Machine
- Wazuh agent service verified as `active (running)`
- Ubuntu endpoint appeared in Wazuh dashboard as an active agent
- Agent details verified:
  - Agent name: `ubuntu-test-machine`
  - Agent ID: `001`
  - IP address: `192.168.56.20`
  - Operating system: Ubuntu 24.04.4 LTS
  - Wazuh agent version: 4.14.5

Documentation: [Day 04 – Ubuntu Agent Enrollment](docs/day-04-ubuntu-agent-enrollment.md)

### Day 05 – Nmap Scan Detection

Completed a safe Nmap scan detection scenario inside the private lab network.

Configured and verified:

- Ubuntu Scanner VM created as a dedicated scanner machine
- Ubuntu Scanner assigned host-only IP address: `192.168.56.40`
- Ubuntu Scanner successfully reached:
  - Wazuh Server: `192.168.56.10`
  - Ubuntu Test Machine: `192.168.56.20`
- Nmap service detection scan performed against Ubuntu Test Machine
- UFW firewall enabled on Ubuntu Test Machine
- UFW logging enabled on Ubuntu Test Machine
- SYN scan performed from Ubuntu Scanner to Ubuntu Test Machine
- UFW logs confirmed blocked scan packets from `192.168.56.40`
- Wazuh dashboard was reviewed for scan-related events
- Limitation documented: Wazuh did not clearly classify the activity as an Nmap scan during this test

Incident report: [Nmap Scan Incident Report](incident-reports/nmap-scan-incident.md)

### Day 06 – Failed SSH Login Detection

Completed a failed SSH login detection scenario inside the private lab network.

Configured and verified:

- SSH access allowed from Ubuntu Scanner to Ubuntu Test Machine
- SSH service verified as running on Ubuntu Test Machine
- Manual failed SSH login attempts generated from Ubuntu Scanner
- Invalid username used: `wronguser`
- Source IP address: `192.168.56.40`
- Target IP address: `192.168.56.20`
- Ubuntu authentication logs confirmed failed SSH attempts
- Wazuh dashboard displayed SSH-related failed login events
- Wazuh detected:
  - `sshd: Attempt to login using a non-existent user`
  - `syslog: User missed the password more than one time`
- Wazuh events confirmed the invalid username and source IP address

Incident report: [Failed SSH Login Incident Report](incident-reports/failed-ssh-login-incident.md)

### Day 07 – Suspicious Command Activity and EICAR Test

Completed suspicious command activity testing and a safe EICAR anti-malware test inside the private lab environment.

Configured and verified:

- Harmless enumeration commands executed on Ubuntu Test Machine
- Sensitive file access attempt performed safely using `/etc/shadow`
- `/etc/shadow` contents were not uploaded to GitHub
- Wazuh recorded sudo command activity
- Wazuh event details showed:
  - Source user: `manula`
  - Destination user: `root`
  - Command: `/usr/bin/head -n 5 /etc/shadow`
  - Agent: `ubuntu-test-machine`
- ClamAV installed on Ubuntu Test Machine
- EICAR test file created locally for safe anti-malware testing
- ClamAV detected the EICAR test file as `Eicar-Signature FOUND`
- Wazuh was reviewed for EICAR-related events
- Limitation documented: Wazuh did not clearly show an EICAR malware detection event during this test
- EICAR test file removed after testing
- Actual EICAR test file was not uploaded to GitHub

Incident report: [Suspicious Command Incident Report](incident-reports/suspicious-command-incident.md)

Notes: [EICAR Test Notes](sample-alerts/eicar-test-notes.md)

## Current Status

The lab foundation and first two detection scenarios are completed.

Completed:

* GitHub repository created
* Ubuntu test machine created
* Wazuh server VM created
* Wazuh server installed
* Wazuh dashboard accessed successfully
* Ubuntu test machine connected to host-only lab network
* Ubuntu test machine enrolled as a Wazuh agent
* Ubuntu scanner VM created
* Safe Nmap scan performed inside the lab network
* UFW firewall logs collected as scan evidence
* Failed SSH login attempts generated manually
* Ubuntu authentication logs reviewed
* Wazuh failed SSH login events reviewed
* Suspicious command activity generated and reviewed
* Wazuh sudo command events reviewed
* EICAR safe malware test performed with ClamAV
* Three incident reports written
* EICAR test notes documented
* Setup documentation and screenshots added

Next steps:

1. Add Suricata IDS for network-based detection.
2. Generate safe network traffic inside the lab.
3. Review Suricata logs.
4. Capture Wireshark evidence.
5. Write the network scan / Suricata incident report.

## Incident Reports

- [Nmap Scan Incident Report](incident-reports/nmap-scan-incident.md)
- [Failed SSH Login Incident Report](incident-reports/failed-ssh-login-incident.md)
- [Suspicious Command Incident Report](incident-reports/suspicious-command-incident.md)

## Sample Alert Notes

- [EICAR Test Notes](sample-alerts/eicar-test-notes.md)

## Repository Structure

```text
mini-soc-lab/
├── README.md
├── setup-guide.md
├── architecture-diagram.png
├── docs/
│   ├── day-02-ubuntu-vm-setup.md
│   ├── day-03-wazuh-server-setup.md
│   └── day-04-ubuntu-agent-enrollment.md
├── screenshots/
│   ├── day-02-ubuntu-vm-setup/
│   ├── day-03-wazuh-server-setup/
│   ├── day-04-ubuntu-agent-enrollment/
│   ├── day-05-nmap-scan-detection/
│   ├── day-06-failed-ssh-login-detection/
│   └── day-07-suspicious-command-eicar/
├── detection-rules/
├── sample-alerts/
│   └── eicar-test-notes.md
├── incident-reports/
│   ├── nmap-scan-incident.md
│   ├── failed-ssh-login-incident.md
│   └── suspicious-command-incident.md
└── lessons-learned.md
```

## Safety and Ethics

All testing in this project is performed only inside a private virtual lab environment.

No public systems, university networks, company networks, or third-party targets will be scanned or tested without permission.