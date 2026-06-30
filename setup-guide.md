# Mini SOC Lab Setup Guide

## Lab Goal

The goal of this lab is to simulate a small SOC environment where endpoint and network logs are collected, analyzed, and used for threat detection and incident response practice.

This lab is being built step by step for cybersecurity internship preparation.

## Planned Lab Components

| Component           | Purpose                                                     | Status                    |
| ------------------- | ----------------------------------------------------------- | ------------------------- |
| Ubuntu Test Machine | Generate test activity and practice Linux/security commands | Completed                 |
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

## Planned Network Design

The lab uses NAT networking for internet access and a host-only network for internal lab communication.

Planned IP address structure:

| Machine             | Planned IP Address | Role                    |
| ------------------- | ------------------ | ----------------------- |
| Wazuh Server        | 192.168.56.10      | SIEM/XDR server         |
| Ubuntu Test Machine | 192.168.56.20      | Test/attacker machine   |
| Windows Endpoint    | 192.168.56.30      | Endpoint/victim machine |

The Wazuh Server currently uses the host-only IP address:

```text
192.168.56.10
```

The Ubuntu Test Machine still needs to be connected to the host-only lab network before it can be enrolled as a Wazuh agent.

## Planned Detection Scenarios

The lab will later be used to test and document these detection scenarios:

1. Nmap port scan detection
2. Failed SSH login / brute-force attempt detection
3. Suspicious command execution
4. Suricata network alert
5. Safe malware test detection using EICAR

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
* [ ] Ubuntu test machine connected to host-only network
* [ ] Wazuh agent installed on Ubuntu test machine
* [ ] Windows endpoint created
* [ ] Suricata installed
* [ ] First alert generated
* [ ] First incident report written

## Setup Progress Logs

* [Day 02 – Ubuntu VM Setup](docs/day-02-ubuntu-vm-setup.md)
* [Day 03 – Wazuh Server Setup](docs/day-03-wazuh-server-setup.md)

## Next Steps

1. Connect the Ubuntu Test Machine to the host-only lab network.
2. Assign or verify the Ubuntu Test Machine lab IP address.
3. Install the Wazuh agent on the Ubuntu Test Machine.
4. Confirm that the Ubuntu Test Machine appears as an active agent in the Wazuh dashboard.
5. Generate the first safe test activity and document the first alert.