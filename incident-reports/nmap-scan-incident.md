# Incident Report: Nmap Scan Against Ubuntu Endpoint

## Summary

A safe Nmap scan was performed inside the private lab network to simulate basic reconnaissance activity against a monitored Ubuntu endpoint.

The scan was launched from the Ubuntu-Scanner VM against the Ubuntu-Test-Machine VM. The Ubuntu-Test-Machine was already enrolled as a Wazuh agent.

## Lab Environment

| Machine             | Role                             | IP Address    |
| ------------------- | -------------------------------- | ------------- |
| Wazuh-Server        | SIEM/XDR server                  | 192.168.56.10 |
| Ubuntu-Test-Machine | Monitored endpoint / scan target | 192.168.56.20 |
| Ubuntu-Scanner      | Scanner machine                  | 192.168.56.40 |

## Activity Performed

An initial service detection scan was performed from Ubuntu-Scanner:

```bash
nmap -sV 192.168.56.20
```

The scan identified SSH running on port 22:

```text
22/tcp open ssh
```

After enabling UFW firewall logging on the target endpoint, a SYN scan was performed:

```bash
sudo nmap -sS -Pn 192.168.56.20
```

## Detection and Evidence

The Ubuntu-Test-Machine firewall logged blocked scan traffic from the scanner machine.

Important log evidence:

```text
[UFW BLOCK]
SRC=192.168.56.40
DST=192.168.56.20
DPT=22
```

The UFW logs also showed multiple destination ports being contacted, which is consistent with port scanning activity.

## Wazuh Result

Wazuh successfully showed the Ubuntu endpoint as an active monitored agent.

During this test, Wazuh displayed some endpoint events, but it did not clearly classify the activity as an Nmap scan or display the UFW firewall block logs in Threat Hunting.

This was documented as a limitation of the current lab configuration.

## Evidence Screenshots

| Screenshot | Description |
| ------------ | ----------- |
| [01-nmap-scan-command.png](../screenshots/day-05-nmap-scan-detection/01-nmap-scan-command.png) | Initial Nmap service detection scan |
| [02-target-ssh-log-after-nmap.png](../screenshots/day-05-nmap-scan-detection/02-target-ssh-log-after-nmap.png) | Target SSH/auth log showing connection activity |
| [03-wazuh-scan-related-events.png](../screenshots/day-05-nmap-scan-detection/03-wazuh-scan-related-events.png) | Wazuh endpoint events reviewed during investigation |
| [04-ufw-enabled-on-target.png](../screenshots/day-05-nmap-scan-detection/04-ufw-enabled-on-target.png) | UFW firewall logging enabled on target |
| [05-nmap-syn-scan-command.png](../screenshots/day-05-nmap-scan-detection/05-nmap-syn-scan-command.png) | SYN scan performed from Ubuntu-Scanner |
| [06-ufw-log-after-nmap-scan.png](../screenshots/day-05-nmap-scan-detection/06-ufw-log-after-nmap-scan.png) | UFW logs showing blocked packets from scanner IP |

## Analysis

Port scanning is commonly used during the reconnaissance phase of an attack. Attackers may scan a system to identify open ports, running services, and possible entry points.

In this lab, the Ubuntu-Scanner contacted multiple ports on the Ubuntu-Test-Machine. The target firewall logged blocked packets from the scanner IP address.

The scan was safely performed only inside the private VirtualBox host-only lab network.

## Severity

Medium

## Recommended Response

* Identify the source IP address.
* Confirm whether the scan was authorized.
* Review firewall logs and endpoint logs.
* Check for follow-up activity after the scan.
* Block unauthorized scanning sources if needed.
* Improve monitoring by collecting firewall or network IDS logs.

## Limitations

Wazuh did not clearly display the UFW firewall block logs or classify the activity as an Nmap scan during this test.

Future improvements:

* Configure Wazuh to collect and parse UFW firewall logs more clearly.
* Add Suricata IDS for network-based scan detection.
* Create custom Wazuh rules for firewall scan patterns.
* Add a Windows endpoint later for additional detection scenarios.

## Lessons Learned

This test showed that endpoint firewall logs can provide strong evidence of scan activity.

It also showed that a SIEM may not automatically classify every suspicious action without the correct log sources and detection rules. SOC analysts need to verify activity using multiple sources, such as endpoint logs, firewall logs, and SIEM events.