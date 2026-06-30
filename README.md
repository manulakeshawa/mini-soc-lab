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
| -------------------------- | ------------------------------------------------------- | ----------------- |
| Oracle VirtualBox          | Virtual lab environment                                 | In use            |
| Ubuntu Desktop 24.04.4 LTS | Ubuntu test machine                                     | Completed         |
| Ubuntu Server 24.04.4 LTS  | Wazuh server base OS                                    | Completed         |
| Wazuh SIEM/XDR             | Log collection, alert analysis, and security monitoring | Installed         |
| Nmap                       | Safe scan activity and network testing                  | Installed         |
| OpenSSH Server             | SSH access and failed login detection practice          | Installed         |
| Wireshark                  | Manual packet analysis                                  | Installed on host |
| Suricata IDS               | Network intrusion detection                             | Planned           |
| Windows Endpoint           | Windows event log collection                            | Planned           |

## Lab Architecture

| Machine             | IP Address              | Purpose                             | Status    |
| ------------------- | ----------------------- | ----------------------------------- | --------- |
| Wazuh Server        | 192.168.56.10           | SIEM/XDR dashboard and log analysis | Installed |
| Ubuntu Test Machine | To be assigned/verified | Test machine and future Wazuh agent | Created   |
| Windows Endpoint    | 192.168.56.30 planned   | Windows event log collection        | Planned   |

Architecture diagram will be updated as the lab environment is completed.

## Planned Detection Scenarios

| Scenario                                 | Status    |
| ---------------------------------------- | --------- |
| Wazuh server setup                       | Completed |
| Ubuntu endpoint agent enrollment         | Planned   |
| Nmap port scan detection                 | Planned   |
| Failed SSH login / brute-force detection | Planned   |
| Suspicious command execution             | Planned   |
| Suricata network alert analysis          | Planned   |
| Safe malware test detection using EICAR  | Planned   |

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

## Current Status

The lab foundation is in progress.

Completed:

* GitHub repository created
* Ubuntu test machine created
* Wazuh server VM created
* Wazuh server installed
* Wazuh dashboard accessed successfully
* Setup documentation and screenshots added

Next steps:

1. Connect the Ubuntu Test Machine to the host-only lab network.
2. Install the Wazuh agent on the Ubuntu Test Machine.
3. Confirm the Ubuntu endpoint appears in the Wazuh dashboard.
4. Generate safe test activity.
5. Document the first alert and incident report.

## Repository Structure

```text
mini-soc-lab/
├── README.md
├── setup-guide.md
├── architecture-diagram.png
├── docs/
│   ├── day-02-ubuntu-vm-setup.md
│   └── day-03-wazuh-server-setup.md
├── screenshots/
│   ├── day-02-ubuntu-vm-setup/
│   └── day-03-wazuh-server-setup/
├── detection-rules/
├── sample-alerts/
├── incident-reports/
└── lessons-learned.md
```

## Safety and Ethics

All testing in this project is performed only inside a private virtual lab environment.

No public systems, university networks, company networks, or third-party targets will be scanned or tested without permission.