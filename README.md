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

---

## Investigation Walkthrough

This section documents the complete deployment of the Active Directory environment, attack simulation, and investigation process performed throughout the project.


### Phase 1 – Building the Active Directory Environment

The Active Directory environment was built to simulate a small enterprise Windows domain. Windows Server 2022 was promoted to a Domain Controller, Windows 10 was joined to the domain, and Splunk was configured to collect endpoint telemetry from the environment.

The following screenshots document the initial deployment and validation of the lab infrastructure.

<img width="1920" height="1080" alt="1  VirtualBox environment containing all required virtual machines; Windows Server 2022, Windows 10, Ubuntu Server (Splunk), and Kali Linux" src="https://github.com/user-attachments/assets/76391775-6cd0-4628-98fe-75a7da8d7efa" />
VirtualBox environment containing all required virtual machines; Windows Server 2022, Windows 10, Ubuntu Server (Splunk), and Kali Linux

&nbsp;

<img width="1920" height="1080" alt="2  Splunk Universal Forwader installed on the Windows Server, with inputs conf configured in the local directory to collect Windows Event Logs and Sysmon telemetry for fowarding to the Splunk server" src="https://github.com/user-attachments/assets/eaa75d6a-2ff9-4185-8ad0-2c04ee85f3c4" />
Splunk Universal Forwader installed on the Windows Server, with inputs.conf configured in the local directory to collect Windows Event Logs and Sysmon telemetry for fowarding to the Splunk server

&nbsp;

<img width="1920" height="1080" alt="PICTURE 3" src="https://github.com/user-attachments/assets/2aa77adc-ca4e-438b-b6a8-a7d665e123c5" />
Splunk Enterprise successfully receiving endpoint telemetry from both the Windows Server (Domain Controller) and Windows 10 workstation through the Splunk Universal Forwarder. The custom endpoint index confirms successful log ingestion, validating communication between the Windows endpoints and the Ubuntu Splunk server. The Windows 10 workstation was configured using the same Universal Forwarder and inputs.conf configuration as the Windows Server.

&nbsp;

<img width="1920" height="1080" alt="PICTURE 4" src="https://github.com/user-attachments/assets/54938121-1064-4cce-bf33-32707796850d" />
Active Directory Domain Services (AD DS) successfully installed on the Windows Server. The server is ready to be promoted to a Domain Controller, enabling centralized authentication, domain management, and Group Policy administration.

&nbsp;

<img width="1920" height="1080" alt="PICTURE 5" src="https://github.com/user-attachments/assets/1dfb9f36-7056-4cc2-9762-bf12ec2ed516" />
Active Directory Domain Services successfully configured with the osvaldo.local domain. Organizational Units (OUs) for the IT and HR departments were created, along with user accounts for each department, demonstrating centralized identity and user management within the domain.

&nbsp;

<img width="1920" height="1080" alt="6  Windows 10 workstation successfully joined to the OSVALDO LOCAL Active Directory domain using Domain Administrator credentials, confirming secure communication and integration with the Domain Controller" src="https://github.com/user-attachments/assets/52ea23f1-5784-4b06-a4e0-9a57dcd481dd" />
Windows 10 workstation successfully joined to the OSVALDO.LOCAL Active Directory domain using Domain Administrator credentials, confirming secure communication and integration with the Domain Controller.

&nbsp;

### Phase 2 - Domain Administration 

<img width="1920" height="1080" alt="PICTURE 7" src="https://github.com/user-attachments/assets/292ec0f9-503a-4b01-bd48-6f27853cf563" />
Successfully authenticated to the Windows 10 workstation using the domain user account Jenny Smith, confirming that Active Directory user authentication and domain login are functioning correctly across the enterprise environment.

&nbsp;

<img width="1920" height="1080" alt="PICTURE 8 " src="https://github.com/user-attachments/assets/9b6526b5-8eaa-4b8d-a1de-b4807d4cf7e6" />
Prepared the Kali attack workspace by creating a dedicated ad-project directory to organize attack resources. Downloaded the Crowbar brute-force tool, transferred and trimmed the rockyou.txt wordlist to a focused set of 20 entries, and created a custom passwords.txt file containing the credentials for the two Active Directory user accounts created during the lab. This setup establishes the environment for the upcoming password attack simulation.

&nbsp;

<img width="1920" height="1080" alt="PICTURE 9" src="https://github.com/user-attachments/assets/d4942bdc-affc-4757-bef2-58793b1cb84c" />
Enabled Remote Desktop RDP access and configured the two domain users IT and HR as authorized Remote Desktop Users, allowing both accounts to remotely log in to the Windows workstation for administration and testing within the Active Directory lab.

&nbsp;

### Phase 3 - Attack Simulation 

<img width="1920" height="1080" alt="Used Hydra to perform an RDP password attack against the domain-joined Windows endpoint  The attack successfully identified valid credentials and generated Windows Security Event Logs for investigation in Splunk" src="https://github.com/user-attachments/assets/1131ce42-ed24-4030-8d99-d2b94746a485" />
Used Hydra to perform an RDP password attack against the domain-joined Windows endpoint. The attack successfully identified valid credentials and generated Windows Security Event Logs for investigation in Splunk.

&nbsp;

<img width="1920" height="1080" alt="PICTURE 11" src="https://github.com/user-attachments/assets/793ad797-9958-4a88-acdb-9cf5a17c083d" />
Hydra brute-force attack successfully captured in Splunk. The search results show 20 failed logon attempts (Event ID 4625) followed by 1 successful logon (Event ID 4624), confirming that the attack telemetry was successfully ingested and indexed for analysis.

&nbsp;

<img width="1920" height="1080" alt="PICTURE 11 PART 2" src="https://github.com/user-attachments/assets/35ee25de-ff26-4a9e-9d9a-9678454c1a0a" />
Splunk event details confirm the successful logon originated from the Kali attack VM. The event identifies the tsmith account and the Kali workstation as the source of the authentication attempt, validating the origin of the simulated Hydra brute-force attack.

&nbsp;

### Phase 4 - Detection & Investigation

<img width="1920" height="1080" alt="PICTURE 12" src="https://github.com/user-attachments/assets/732a47b1-3dd2-4c51-bc3f-1bbc7b76d216" />
Executed Atomic Red Team test T1136.001 (Create Local Account) to simulate a MITRE ATT&CK Persistence technique. The test created a local user account on the Windows 10 target, generating security telemetry that was analyzed in Splunk to validate detection coverage and identify potential monitoring gaps.

&nbsp;

<img width="1920" height="1080" alt="PICTURE 13" src="https://github.com/user-attachments/assets/bbab2181-0a76-47c9-bbee-1c914d18da5b" />
Splunk successfully detected the Atomic Red Team T1136.001 (Create Local Account) simulation by capturing the creation of the NewLocalUser account. This validates that the current detection pipeline is ingesting and identifying persistence-related activity. Simulated attacks like this can be used to evaluate detection coverage, identify monitoring blind spots, and improve detection engineering by creating or refining rules for techniques that are not currently detected.


---

## Indicators of Compromise (IOCs)

The following indicators were identified during the attack simulation and investigation:

- Multiple failed Windows authentication attempts generated during brute-force testing.
- Successful authentication following valid credential discovery.
- Windows Security Event IDs associated with authentication activity.
- Sysmon process creation events related to attack execution.
- Source IP address of the attacking Kali Linux system.
- User accounts targeted during the brute-force attack.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ATT&CK ID |
|-----------|-----------|-----------|
| Credential Access | Brute Force | T1110 |
| Defense Evasion/Presistence | Valid Accounts | T1078 |
| Lateral Movement | Remote Services (RDP) | T1021.001 |
| Discovery | Account Discovery | T1087 |

---

## Lab Challenges & Troubleshooting

### Challenge 1

<img width="1920" height="1080" alt="Used Hydra to perform an RDP password attack against the domain-joined Windows endpoint  The attack successfully identified valid credentials and generated Windows Security Event Logs for investigation in Splunk" src="https://github.com/user-attachments/assets/62fa8764-6ac3-4103-ab3d-a106b0f20261" />
Troubleshooting: The original lab walkthrough used Crowbar for the RDP attack. During testing, Crowbar's RDP module was incompatible with my Kali environment and did not successfully authenticate despite valid credentials. After validating RDP connectivity and credentials, I adapted the lab by using Hydra with a single-threaded configuration (-t 1 -W 3), which successfully completed the attack and generated the required Windows security events.

&nbsp;

### Challenge 2

<img width="1920" height="1080" alt="PICTURE 11" src="https://github.com/user-attachments/assets/0090410c-9e81-4a48-a57f-41f9535f481e" />
During the lab, authentication events were not appearing in Splunk. Investigation revealed that the Windows 10 endpoint and Splunk server had different system times. After synchronizing the VM clocks and restarting Splunk and the Universal Forwarder, the authentication events were indexed correctly.


---

## Key Findings

- Successfully deployed an enterprise-style Active Directory environment for security testing.
- Verified Windows Security Events and Sysmon telemetry were forwarded to Splunk.
- Successfully simulated brute-force authentication activity against the domain environment.
- Investigated authentication events using Splunk searches and event correlation.
- Validated detection visibility while identifying opportunities to improve monitoring coverage.

---

## Lessons Learned

- Active Directory provides a realistic enterprise environment for SOC investigations and detection engineering.
- Accurate log collection is essential for identifying authentication attacks and reconstructing attacker activity.
- Attack simulation is valuable for validating detections and identifying monitoring gaps.
- Troubleshooting infrastructure and security tooling is a normal part of defensive security operations and strengthens investigative skills.
