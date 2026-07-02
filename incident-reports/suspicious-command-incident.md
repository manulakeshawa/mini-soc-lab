# Incident Report: Suspicious Command Activity

## Summary

Harmless suspicious command activity was performed inside the private lab environment to simulate basic post-login enumeration behavior.

The commands were executed on the Ubuntu-Test-Machine, which was already enrolled as a Wazuh agent.

This scenario was used to observe how Wazuh records privileged command execution and access attempts involving sensitive Linux files.

## Lab Environment

| Machine             | Role                      | IP Address    |
| ------------------- | ------------------------- | ------------- |
| Wazuh-Server        | SIEM/XDR server           | 192.168.56.10 |
| Ubuntu-Test-Machine | Monitored Ubuntu endpoint | 192.168.56.20 |

## Activity Performed

The following commands were executed on the Ubuntu-Test-Machine:

```bash
whoami
hostname
ip a | head -n 12
cat /etc/passwd | head -n 5
sudo ls -l /etc/shadow
sudo head -n 5 /etc/shadow > /dev/null
```

The `/etc/shadow` file contents were not displayed in the final project screenshot or uploaded to GitHub.

## Detection and Evidence

Wazuh recorded the privileged command activity from the monitored Ubuntu endpoint.

Important Wazuh event details included:

```text
data.command: /usr/bin/head -n 5 /etc/shadow
data.dstuser: root
data.srcuser: manula
decoder.name: sudo
agent.name: ubuntu-test-machine
agent.ip: 192.168.56.20
```

This confirmed that Wazuh captured the sudo command used to access a sensitive Linux file.

## Evidence Screenshots

| Screenshot                                                                                                                        | Description                                             |
|:----------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------|
| [01-suspicious-commands-terminal.png](../screenshots/day-07-suspicious-command-eicar/01-suspicious-commands-terminal.png)         | Harmless enumeration and sensitive file access commands |
| [02-wazuh-shadow-command-events.png](../screenshots/day-07-suspicious-command-eicar/02-wazuh-shadow-command-events.png)           | Wazuh events related to `/etc/shadow` activity          |
| [03-wazuh-suspicious-command-details.png](../screenshots/day-07-suspicious-command-eicar/03-wazuh-suspicious-command-details.png) | Wazuh event details showing the executed sudo command   |

## Analysis

Commands such as `whoami`, `hostname`, `ip a`, and `cat /etc/passwd` are normal administrative commands. However, they can also appear during post-login enumeration after an attacker gains access to a system.

Accessing `/etc/shadow` is more sensitive because it contains password hash information on Linux systems. In this lab, the command was executed only for safe monitoring practice, and the actual file contents were not uploaded to GitHub.

Wazuh successfully recorded the privileged command execution through sudo logs.

## Severity

Low to Medium

## Recommended Response

* Identify the user account that executed the command.
* Confirm whether the activity was authorized.
* Review recent login activity for the same user.
* Check whether sensitive files were accessed.
* Monitor for privilege escalation attempts.
* Restrict unnecessary sudo access where possible.
* Continue monitoring for follow-up suspicious commands.

## Lessons Learned

This test showed that Wazuh can record sudo command activity on a monitored Linux endpoint.

It also showed why command context matters. Some commands may be normal for administrators, but they can become suspicious when combined with unauthorized login activity, sensitive file access, or unusual timing.