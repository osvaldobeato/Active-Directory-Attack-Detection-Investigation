# SOC Active Directory: Attack Detection & Investigation

## Project Overview

This project demonstrates the design and implementation of an Active Directory home lab used to simulate enterprise authentication attacks and investigate the resulting Windows security events.

The environment consists of a Windows Server 2022 Domain Controller, a Windows 10 domain-joined workstation, Kali Linux, and Splunk Enterprise. Sysmon and Windows Event Logs were collected and analyzed to provide visibility into authentication activity, endpoint behavior, and attack telemetry.

Attack simulations included Active Directory user management, remote administration, brute-force authentication attempts, and Atomic Red Team testing. Splunk was used to investigate Windows Security events, validate detections, identify monitoring gaps, and demonstrate detection engineering techniques.

This project demonstrates the ability to build an enterprise Windows environment, generate realistic attack telemetry, investigate malicious activity using SIEM data, and document findings through a structured SOC investigation workflow.

---

## Lab Architecture

<img width="791" height="780" alt="Screenshot 2026-07-18 103809" src="https://github.com/user-attachments/assets/fd62f265-4bee-4b09-8993-ac5ae2976c44" />


---

## Skills Demonstrated

- Active Directory Administration
- Windows Server 2022 Configuration
- Domain Controller Deployment
- Windows Domain Management
- Splunk Log Analysis
- Windows Event Log Analysis
- Sysmon Endpoint Monitoring
- Authentication Attack Detection
- Brute-Force Attack Simulation
- Atomic Red Team Testing
- Incident Investigation
- Detection Engineering
- Threat Hunting
- Security Event Correlation
- MITRE ATT&CK Framework

  ---

## Tools Used

| Tool | Purpose |
|------|---------|
| Windows Server 2022 | Active Directory Domain Controller |
| Windows 10 | Domain-joined endpoint used for attack simulation |
| Kali Linux | Attack platform for brute-force authentication testing |
| Splunk Enterprise | Centralized log collection, search, and investigation |
| Sysmon | Endpoint telemetry and process monitoring |
| Splunk Universal Forwarder | Forwarded Windows logs to Splunk |
| Hydra | Brute-force authentication testing |
| Atomic Red Team | Simulated adversary techniques for detection validation |
| VirtualBox | Hosted the Active Directory lab environment |
