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

| Scenario                                 | Status    |
|------------------------------------------|-----------|
| Wazuh server setup                       | Completed |
| Ubuntu endpoint agent enrollment         | Completed |
| Nmap port scan detection                 | Completed |
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

## Current Status

The lab foundation and first detection scenario are in progress.

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
* First incident report written
* Setup documentation and screenshots added

Next steps:

1. Generate manual failed SSH login attempts inside the lab network.
2. Check `/var/log/auth.log` on the Ubuntu Test Machine.
3. Check Wazuh dashboard for failed SSH login events.
4. Capture evidence screenshots.
5. Write the failed SSH login incident report.

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
│   └── day-05-nmap-scan-detection/
├── detection-rules/
├── sample-alerts/
├── incident-reports/
│   └── nmap-scan-incident.md
└── lessons-learned.md
```

## Safety and Ethics

All testing in this project is performed only inside a private virtual lab environment.

No public systems, university networks, company networks, or third-party targets will be scanned or tested without permission.