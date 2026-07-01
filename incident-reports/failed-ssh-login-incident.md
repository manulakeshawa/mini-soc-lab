# Incident Report: Failed SSH Login Attempts

## Summary

Manual failed SSH login attempts were generated inside the private lab network to simulate unauthorized login activity.

The login attempts were made from the Ubuntu-Scanner VM against the Ubuntu-Test-Machine VM. The Ubuntu-Test-Machine was already enrolled as a Wazuh agent.

## Lab Environment

| Machine             | Role                            | IP Address    |
| ------------------- | ------------------------------- | ------------- |
| Wazuh-Server        | SIEM/XDR server                 | 192.168.56.10 |
| Ubuntu-Test-Machine | Monitored endpoint / SSH target | 192.168.56.20 |
| Ubuntu-Scanner      | Source machine                  | 192.168.56.40 |

## Activity Performed

A manual SSH login attempt was made from Ubuntu-Scanner using a non-existent username:

```bash
ssh wronguser@192.168.56.20
```

Incorrect passwords were entered multiple times.

No brute-force tools were used. The activity was performed manually inside the private lab network.

## Detection and Evidence

The Ubuntu-Test-Machine authentication log recorded the failed SSH activity.

Important log evidence included:

```text
Invalid user wronguser from 192.168.56.40
Failed password for invalid user wronguser from 192.168.56.40
Connection closed by invalid user wronguser from 192.168.56.40
```

Wazuh also displayed SSH-related security events for the monitored Ubuntu endpoint.

Wazuh evidence included:

* `sshd: Attempt to login using a non-existent user`
* `syslog: User missed the password more than one time`
* Source IP: `192.168.56.40`
* Username: `wronguser`

## Evidence Screenshots

| Screenshot                                                                                                                  | Description                                           |
|:----------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------|
| [01-ufw-allow-ssh-from-scanner.png](../screenshots/day-06-failed-ssh-login-detection/01-ufw-allow-ssh-from-scanner.png)     | UFW rule allowing SSH from Ubuntu-Scanner             |
| [02-ssh-service-running.png](../screenshots/day-06-failed-ssh-login-detection/02-ssh-service-running.png)                   | SSH service running on Ubuntu-Test-Machine            |
| [03-failed-ssh-attempts-terminal.png](../screenshots/day-06-failed-ssh-login-detection/03-failed-ssh-attempts-terminal.png) | Failed SSH attempts from Ubuntu-Scanner               |
| [04-auth-log-failed-ssh.png](../screenshots/day-06-failed-ssh-login-detection/04-auth-log-failed-ssh.png)                   | Target authentication log showing failed SSH attempts |
| [05-wazuh-failed-ssh-events.png](../screenshots/day-06-failed-ssh-login-detection/05-wazuh-failed-ssh-events.png)           | Wazuh SSH-related failed login events                 |
| [06-wazuh-failed-ssh-source-ip.png](../screenshots/day-06-failed-ssh-login-detection/06-wazuh-failed-ssh-source-ip.png)     | Wazuh events filtered by scanner IP                   |
| [07-wazuh-failed-ssh-wronguser.png](../screenshots/day-06-failed-ssh-login-detection/07-wazuh-failed-ssh-wronguser.png)     | Wazuh events filtered by invalid username             |

## Analysis

Failed SSH login attempts may indicate unauthorized access attempts, password guessing, or reconnaissance against a remote access service.

In this lab, the activity was confirmed from multiple sources:

* The source terminal showed failed SSH login attempts.
* The target authentication log recorded the invalid username and failed passwords.
* Wazuh displayed SSH-related alerts for the monitored endpoint.

This demonstrates how endpoint logs and SIEM alerts can help SOC analysts investigate suspicious authentication activity.

## Severity

Medium

## Recommended Response

* Identify the source IP address.
* Confirm whether the login attempts were authorized.
* Review authentication logs for repeated failures.
* Disable password-based SSH login where possible.
* Use strong passwords or SSH keys.
* Restrict SSH access using firewall rules.
* Monitor for repeated attempts from the same source.

## Lessons Learned

Authentication logs are important for detecting unauthorized access attempts.

Compared to the Nmap scan test, Wazuh provided clearer detection for failed SSH login activity. This shows that SIEM visibility depends on the type of activity, available logs, and detection rules.