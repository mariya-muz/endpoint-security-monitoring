# Task 1: Implement Endpoint Security & Monitoring

## Objective

Protect [**Internee.pk](http://internee.pk/)’s** devices and servers from malware and unauthorized access by deploying endpoint detection, monitoring, and automated alerting mechanisms.

---

## Environment Setup

- **Server:** Ubuntu VM (VirtualBox) running Wazuh server and dashboard
- **Agents:**
    - Ubuntu VM agent for server-side monitoring
    - Windows 11 endpoint agent with Sysmon integration for detailed event logging

<img width="1200" height="600" alt="1 wazuh-installed" src="https://github.com/user-attachments/assets/0e7760df-2481-4980-816b-f2efb3b7006a" />
<img width="1200" height="600" alt="2 wazuh-login" src="https://github.com/user-attachments/assets/90a059eb-95c9-40c3-bd58-6ba3577b03ab" />
<img width="1200" height="600" alt="3 wazuh-dashboard" src="https://github.com/user-attachments/assets/ed6d06d8-46fd-40c1-8ecd-b27b4e954490" />


---

## Task Deliverables

- **Deploy EDR tools (Wazuh):** Installed and configured Wazuh server, indexer, manager, and dashboard.
- **Monitor file integrity and user activity:** Enabled File Integrity Monitoring (FIM) to track changes in critical files (e.g., `/etc/hosts`).
- **Automate alerts for suspicious behavior:** Configured Wazuh rules to trigger alerts for anomalies such as suspicious PowerShell executions, dropped executables, and unauthorized discovery activities.
- **Sysmon integration:** Collected detailed Windows event logs (process creation, file writes, registry changes) for enhanced visibility.
- **MalwareBazaar threat intelligence:** Integrated public dataset feeds to detect known malware hashes in Sysmon logs.

---

## Data Sources

- **Sysmon logs:** Real-time monitoring of Windows endpoint activity.
- **MalwareBazaar feeds:** External threat intelligence for malware detection.

---

## Key Results

### 1. **Security Events Dashboard**

- Captured **1,771 events** between April 8–15, 2026.
- Alerts included:
    - Windows logon successes
    - Suspicious PowerShell activity creating executables
    - Executable dropped in malware-prone directories
    - Account discovery commands (`net.exe`)

<img width="1200" height="800" alt="9 malware-bazaar-logged" src="https://github.com/user-attachments/assets/b5c00568-b945-49a3-8b39-747e5218edcf" />
<img width="1200" height="800" alt="7 sysmon-dashboard" src="https://github.com/user-attachments/assets/85fda0e0-6c1c-4b08-a25d-32f22567920b" />


### 2. **File Integrity Monitoring (FIM)**

- `/etc/hosts` file modifications detected multiple times.
- Integrity checksum changes logged with severity Level 7.
- Dashboard visualizations showed modification spikes over the monitored period.

<img width="1200" height="600" alt="4 terminal-filechange" src="https://github.com/user-attachments/assets/94c63b13-b0ec-49a1-b77f-eb07b3ba17b1" />
<img width="1200" height="600" alt="5 fim-dashboard" src="https://github.com/user-attachments/assets/4f2e1468-6b8c-4918-b1e6-3e50ce396ec2" />
<img width="1200" height="600" alt="6 fim-events" src="https://github.com/user-attachments/assets/1777a6e2-7351-4e35-8731-6864269788bc" />


### 3. **Sysmon Integration**

- Discovery activities (MITRE ATT&CK Technique T1087).
- PowerShell execution spawning discovery commands (T1059.001).
- Suspicious binaries launched from unusual directories.

<img width="1200" height="800" alt="7 sysmon-dashboard" src="https://github.com/user-attachments/assets/2501b07d-6868-40a2-b2b8-f7b240597a95" />
<img width="1200" height="800" alt="8 sysmon-events" src="https://github.com/user-attachments/assets/c8e88136-19d6-402a-816c-3ac7bb2496c2" />


### 4. MalwareBazaar Integration

- API used
- data extracted (`sha256_hash`)
- stored in CDB list
- matched against Sysmon `hashes` field
- rule ID 100300 triggers alert

<img width="1200" height="800" alt="9 malware-bazaar-logged" src="https://github.com/user-attachments/assets/a1054fef-6e33-4a11-bd64-9e62b04afb7b" />


### 5. **Alert Automation**

- Configured rules to escalate alerts with severity levels (e.g., Level 12+ for malware detections).
- Example: Detection of **MalwareBazaar SHA256 hashes** in Sysmon logs triggered Level 12 alerts.

### Rule Logic:

- Rule 92031 = Sysmon process detection
- Rule 100300 = MalwareBazaar correlation layer
- Matching occurs on SHA256 inside event hash string

---

## Compliance Mapping

- Alerts mapped to **PCI DSS requirements** (e.g., 2.2, 4.1, 10.6.1).
- Demonstrated alignment with regulatory standards for monitoring and access control.

---

## Conclusion

The deployment successfully established a **comprehensive endpoint detection and response system** for [Internee.pk](http://internee.pk/).

- Wazuh server and agents are operational.
- Sysmon logs provide granular visibility into Windows endpoint behavior.
- FIM detects unauthorized file modifications.
- MalwareBazaar integration enhances detection of known threats.
- Automated alerts ensure proactive response to suspicious activity.

This setup strengthens [Internee.pk](http://internee.pk/)’s cybersecurity posture by combining **real-time monitoring, automated detection, and compliance reporting**.
