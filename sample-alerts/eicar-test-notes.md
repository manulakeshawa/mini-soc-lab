# EICAR Test Notes

## Purpose

The EICAR test file was used to safely test anti-malware detection behavior in the lab environment.

EICAR is a safe test string commonly used to verify whether anti-malware tools can detect a test file without using real malware.

## Lab Environment

| Machine             | Role                      | IP Address    |
| ------------------- | ------------------------- | ------------- |
| Wazuh-Server        | SIEM/XDR server           | 192.168.56.10 |
| Ubuntu-Test-Machine | Monitored Ubuntu endpoint | 192.168.56.20 |

## Tool Used

| Tool   | Purpose                             |
| ------ | ----------------------------------- |
| ClamAV | Scan and detect the EICAR test file |

## Activity Performed

ClamAV was installed on the Ubuntu-Test-Machine.

The EICAR test file was created locally for testing purposes only.

The file was scanned using:

```bash
clamscan eicar-test.txt
```

## Detection Result

ClamAV successfully detected the EICAR test file.

Detection result:

```text
Eicar-Signature FOUND
```

The scan summary showed:

```text
Infected files: 1
```

## Wazuh Result

Wazuh was reviewed for EICAR-related events.

Search terms used included:

```text
eicar
clamscan
Eicar-Signature
eicar-test.txt
```

During this test, Wazuh did not clearly display an EICAR-related malware detection event.

This was documented as a limitation of the current lab configuration.

## Evidence Screenshots

| Screenshot                                                                                                                  | Description                                       |
|:----------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------|
| [04-clamav-installed.png](../screenshots/day-07-suspicious-command-eicar/04-clamav-installed.png)                           | ClamAV installed and verified                     |
| [05-eicar-clamav-detection.png](../screenshots/day-07-suspicious-command-eicar/05-eicar-clamav-detection.png)               | ClamAV detecting the EICAR test file              |
| [06-wazuh-eicar-search-no-results.png](../screenshots/day-07-suspicious-command-eicar/06-wazuh-eicar-search-no-results.png) | Wazuh search showing no clear EICAR-related event |
| [07-eicar-test-file-removed.png](../screenshots/day-07-suspicious-command-eicar/07-eicar-test-file-removed.png)             | EICAR test file removed after testing             |

## Safety Notes

The EICAR file was used only inside the private lab environment.

The actual EICAR test file was not uploaded to GitHub.

Only screenshots and notes were added to the repository.

After testing, the file was removed from the Ubuntu-Test-Machine.

## Limitations

ClamAV detected the EICAR test file successfully, but Wazuh did not clearly show an EICAR malware detection event during this test.

Future improvements:

* Configure Wazuh to collect ClamAV scan logs.
* Add custom Wazuh rules for ClamAV detection output.
* Test Wazuh File Integrity Monitoring for suspicious file creation.
* Add dedicated malware detection documentation after improving log collection.

## Lessons Learned

This test showed that anti-malware detection and SIEM visibility are not always the same thing.

ClamAV successfully detected the EICAR test file, but Wazuh did not automatically display a clear malware alert. This shows that security tools must be configured with the correct log sources and rules to provide useful detection visibility.