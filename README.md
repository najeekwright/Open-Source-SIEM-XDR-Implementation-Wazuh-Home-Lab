# Open-Source SIEM & XDR Implementation: Wazuh Home Lab

## 1. Project Objective
I initiated this project to build a production-grade Security Operations Center (SOC) environment. The goal was to deploy **Wazuh** as a centralized SIEM/XDR platform to monitor cross-platform endpoints, analyze telemetry against the MITRE ATT&CK framework, and perform automated vulnerability assessments.

---

## 2. Infrastructure & System Engineering (Ubuntu Backend)
Unlike basic cloud-managed tools, I engineered the underlying infrastructure using a **Linux-first approach**. This involved configuring a virtualized network and a hardened server environment.

* **Manager OS:** Ubuntu Server 22.04 LTS (Headless).
* **System Configuration:** Optimized the Linux kernel settings for high-volume log ingestion (4 vCPUs, 8GB RAM).
* **Network Architecture:** Established a private virtual network in VMware to allow secure communication between the Ubuntu Manager and the monitored endpoints.
* **CLI Administration:** Performed all server-side tasks via the Bash terminal, including script execution, service management, and troubleshooting.

(Ubuntu Terminal Setup)

<img width="1403" height="761" alt="Ubuntu Initial" src="https://github.com/user-attachments/assets/fcd15b0d-0fdb-463d-9ea8-96c5fa16058c" />

*Figure 1: Using the Ubuntu terminal to execute the Wazuh installation and verify service status.*

---

## 3. Phase 1: SIEM Manager & Dashboard Deployment
The Wazuh Manager was deployed as a full-stack security engine.
* **Automation:** Utilized the Wazuh installation assistant to deploy the Indexer, Server, and Dashboard in a single automated workflow.
* **Security:** Configured SSL/TLS certificates for secure web access via Port 443 and established administrative role-based access.

(Wazuh Dashboard) 

<img width="2026" height="798" alt="Wazuh Dashboard" src="https://github.com/user-attachments/assets/1b5cf646-0918-432b-9e24-db5078aed936" />

*Figure 2: The centralized Wazuh dashboard indicating the manager is online and ready for telemetry.*

---

## 4. Phase 2: Cross-Platform Agent Deployment
I deployed telemetry agents across different operating systems to simulate a diverse corporate environment.
* **Linux Agent:** Enrolled a secondary Ubuntu Desktop instance using the Wazuh agent API.
* **Windows Agent:** Deployed the Wazuh MSI package via PowerShell on a Windows 10 endpoint.
* **Heartbeat Verification:** Confirmed that both agents were reporting real-time system data back to the manager node.

(Active Agents) 

<img width="1975" height="640" alt="Windows Linux Client Online" src="https://github.com/user-attachments/assets/1e541f03-a690-4867-a7a6-e54fc7933ab0" />


*Figure 3: Multi-OS visibility showing both Linux and Windows agents in an "Active" state.*

---

## 5. Phase 3: Threat Detection & MITRE Mapping
With the foundation built, I moved into active security monitoring:
* **FIM (File Integrity Monitoring):** Configured real-time monitoring of sensitive Windows Registry keys and Linux system files.
* **MITRE ATT&CK Correlation:** Validated that administrative escalations (e.g., `sudo` usage) were correctly mapped to Tactic **TA0004 (Privilege Escalation)**.
* **EDR Testing:** Generated "noise" through software installations to observe how the SIEM captures and categorizes system changes.



---

## 6. Phase 4: Vulnerability & Compliance Auditing
The final phase involved using the SIEM as an auditing tool to improve the overall security posture.
* **CVE Identification:** Scanned endpoints for known vulnerabilities, identifying critical patches missing on the Windows host.
* **CIS Hardening:** Used the SCA (Security Configuration Assessment) module to audit the system against CIS Benchmarks, revealing configuration gaps.

## 7. Final Observations & SIEM Conclusion
This project successfully demonstrated the deployment of a full-scale, open-source SIEM/XDR solution. By moving the lab from a cloud-managed service to a self-hosted Ubuntu environment, I gained a deeper understanding of the "plumbing" behind security operations.


### Key Technical Takeaways:
* **The Power of Visibility**: Within minutes of installing the agents, I was able to see the "hidden" background processes of my Windows and Linux machines. Seeing a simple software install generate dozens of File Integrity Monitoring (FIM) alerts highlighted how much telemetry is available for analysis.
* **Linux as a Backbone**: Configuring the Wazuh manager on **Ubuntu Server** solidified my Linux administration skills. Managing services via the CLI and troubleshooting connectivity between VMs proved that a SOC Analyst must also be a capable Systems Administrator.
* **Proactive vs. Reactive**: While my previous projects focused on logging "attacks," this Wazuh lab focused on **Vulnerability Management**. Identifying CVEs and CIS compliance gaps *before* an attack occurs is the most critical lesson I learned for real-world defense.
* **Automated Correlation**: The ability of the manager to automatically map a simple `sudo` command to the **MITRE ATT&CK Framework** showed me how modern SIEMs reduce the "cognitive load" on analysts by providing instant context to raw logs.

---
**[End of Project Documentation]**
