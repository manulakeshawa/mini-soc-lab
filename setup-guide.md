# Mini SOC Lab Setup Guide

## Lab Goal

The goal of this lab is to simulate a small SOC environment where endpoint and network logs are collected, analyzed, and used for threat detection and incident response practice.

This lab is being built step by step for cybersecurity internship preparation.

## Planned Lab Components

| Component           | Purpose                                                     | Status                    |
|---------------------|-------------------------------------------------------------|---------------------------|
| Ubuntu Test Machine | Generate test activity and practice Linux/security commands | Completed                 |
| Ubuntu Scanner      | Run safe Nmap scans inside the private lab network          | Completed                 |
| Wazuh Server        | SIEM/XDR dashboard and alert analysis                       | Completed                 |
| Windows Endpoint    | Collect Windows event logs                                  | Planned                   |
| Suricata IDS        | Network intrusion detection                                 | Planned                   |
| Wireshark           | Manual packet analysis                                      | Installed on host machine |
| Nmap                | Generate safe scan activity for detection practice          | Installed                 |
| OpenSSH Server      | Practice SSH access and failed login detection              | Installed                 |

## Current Completed Setup

### Ubuntu Test Machine

The first Ubuntu test machine has been created successfully in Oracle VirtualBox.

Completed work:

* Ubuntu 24.04.4 LTS installed
* VM configured with 4096 MB RAM and 2 processors
* NAT networking verified
* Basic tools installed: `nmap`, `net-tools`, `curl`, `git`, `openssh-server`
* SSH socket verified on port 22
* VirtualBox snapshots created for recovery
* Setup screenshots documented

Detailed documentation:

* [Day 02 – Ubuntu VM Setup](docs/day-02-ubuntu-vm-setup.md)

### Wazuh Server

The Wazuh server VM has been created and installed successfully using Ubuntu Server 24.04.4 LTS.

Completed work:

* Wazuh Server VM created in Oracle VirtualBox
* VM configured with 8192 MB RAM and 4 processors
* 50 GB virtual disk allocated
* NAT network configured for internet access
* Host-only network configured with IP address `192.168.56.10`
* Wazuh server installed successfully
* Wazuh services verified as running:

  * `wazuh-manager.service`
  * `wazuh-indexer.service`
  * `wazuh-dashboard.service`
  * `filebeat.service`
* Wazuh dashboard accessed from the Windows host browser
* Admin password saved privately and not uploaded to GitHub
* VirtualBox snapshot created after successful Wazuh installation

Detailed documentation:

* [Day 03 – Wazuh Server Setup](docs/day-03-wazuh-server-setup.md)

### Ubuntu Agent Enrollment

The Ubuntu Test Machine has been connected to the host-only lab network and enrolled as a Wazuh agent.

Completed work:

* Host-only network configured on Ubuntu Test Machine
* Static IP address assigned: `192.168.56.20`
* Connectivity to Wazuh Server verified
* Wazuh agent installed
* Wazuh agent service verified as running
* Ubuntu endpoint appeared as active in the Wazuh dashboard

Detailed documentation:

* [Day 04 – Ubuntu Agent Enrollment](docs/day-04-ubuntu-agent-enrollment.md)

### Ubuntu Scanner

A separate Ubuntu Scanner VM was created to run safe Nmap scans inside the private lab network.

Completed work:

* Ubuntu Scanner VM created in Oracle VirtualBox
* Basic tools installed, including `nmap`
* Host-only adapter configured
* Static IP address assigned: `192.168.56.40`
* Connectivity verified to Wazuh Server at `192.168.56.10`
* Connectivity verified to Ubuntu Test Machine at `192.168.56.20`

Purpose:

The Ubuntu Scanner is used to generate safe scan activity against lab endpoints only.

### Failed SSH Login Detection

Manual failed SSH login attempts were generated from Ubuntu Scanner against the Ubuntu Test Machine.

Completed work:

* SSH service verified as running on Ubuntu Test Machine
* UFW rule added to allow SSH from Ubuntu Scanner
* Failed SSH attempts generated manually using the username `wronguser`
* Authentication logs reviewed on Ubuntu Test Machine
* Wazuh dashboard reviewed for failed SSH login events
* Wazuh showed SSH-related alerts for non-existent user login attempts
* Source IP confirmed as `192.168.56.40`
* Failed SSH login incident report written

Detailed documentation:

* [Failed SSH Login Incident Report](incident-reports/failed-ssh-login-incident.md)

### Suspicious Command Activity and EICAR Test

Suspicious command activity was generated on the Ubuntu Test Machine to simulate basic post-login enumeration behavior.

Completed work:

* Harmless enumeration commands executed on Ubuntu Test Machine
* Sensitive file access attempt performed using `/etc/shadow`
* `/etc/shadow` contents were not uploaded to GitHub
* Wazuh dashboard reviewed for sudo command activity
* Wazuh event details confirmed the executed command
* Suspicious command incident report written

EICAR safe malware testing was also performed using ClamAV.

Completed work:

* ClamAV installed on Ubuntu Test Machine
* EICAR test file created locally for safe anti-malware testing
* ClamAV detected the EICAR test file as `Eicar-Signature FOUND`
* Wazuh reviewed for EICAR-related events
* Limitation documented: Wazuh did not clearly show an EICAR malware detection event during this test
* EICAR test file removed after testing
* Actual EICAR test file was not uploaded to GitHub

Detailed documentation:

* [Suspicious Command Incident Report](incident-reports/suspicious-command-incident.md)
* [EICAR Test Notes](sample-alerts/eicar-test-notes.md)

## Planned Network Design

The lab uses NAT networking for internet access and a host-only network for internal lab communication.

Planned IP address structure:

| Machine             | Planned IP Address   | Role                             |
|---------------------|----------------------|----------------------------------|
| Wazuh Server        | 192.168.56.10        | SIEM/XDR server                  |
| Ubuntu Test Machine | 192.168.56.20        | Monitored endpoint / scan target |
| Ubuntu Scanner      | 192.168.56.40        | Scanner / Nmap machine           |
| Windows Endpoint    | 192.168.56.30        | Endpoint/victim machine          |

The Wazuh Server currently uses the host-only IP address:

```text
192.168.56.10
```

The Ubuntu Test Machine is connected to the host-only lab network with the IP address 192.168.56.20 and has been enrolled as an active Wazuh agent.

## Detection Scenarios

The lab is being used to test and document these detection scenarios:

| Scenario                                         | Status                 |
|--------------------------------------------------|------------------------|
| Nmap port scan detection                         | Completed              |
| Failed SSH login / brute-force attempt detection | Completed              |
| Suspicious command execution                     | Completed              |
| Safe malware test detection using EICAR          | Completed / Documented |
| Suricata network alert                           | Planned                |

## Setup Status

* [x] GitHub repository created
* [x] Ubuntu test machine created
* [x] Ubuntu test machine updated
* [x] Basic tools installed on Ubuntu test machine
* [x] SSH socket enabled and verified
* [x] VirtualBox snapshots created
* [x] Wazuh server VM created
* [x] Host-only network configured for Wazuh server
* [x] Wazuh server installed
* [x] Wazuh services verified
* [x] Wazuh dashboard accessed successfully
* [x] Ubuntu test machine connected to host-only network
* [x] Wazuh agent installed on Ubuntu test machine
* [x] Ubuntu test machine active in Wazuh dashboard
* [x] Ubuntu scanner VM created
* [x] Ubuntu scanner connected to host-only network
* [x] Nmap scan performed inside lab network
* [x] UFW firewall logs captured as scan evidence
* [x] Nmap scan incident report written
* [x] Failed SSH login detection completed
* [x] Failed SSH login incident report written
* [x] Suspicious command detection completed
* [x] Suspicious command incident report written
* [x] EICAR safe malware test completed
* [x] EICAR test notes written
* [ ] Suricata installed
* [ ] Windows endpoint created

## Setup Progress Logs

* [Day 02 – Ubuntu VM Setup](docs/day-02-ubuntu-vm-setup.md)
* [Day 03 – Wazuh Server Setup](docs/day-03-wazuh-server-setup.md)
* [Day 04 – Ubuntu Agent Enrollment](docs/day-04-ubuntu-agent-enrollment.md)
* [Nmap Scan Incident Report](incident-reports/nmap-scan-incident.md)
* [Failed SSH Login Incident Report](incident-reports/failed-ssh-login-incident.md)
* [Suspicious Command Incident Report](incident-reports/suspicious-command-incident.md)
* [EICAR Test Notes](sample-alerts/eicar-test-notes.md)

## Next Steps

1. Install Suricata IDS for network-based detection.
2. Generate safe network traffic inside the lab.
3. Review Suricata logs.
4. Capture Wireshark evidence.
5. Write the network scan / Suricata incident report.