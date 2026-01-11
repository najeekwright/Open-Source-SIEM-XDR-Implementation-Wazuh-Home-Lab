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

![Ubuntu Terminal Setup](./img/ubuntu_cli.png)
*Figure 1: Using the Ubuntu terminal to execute the Wazuh installation and verify service status.*

---

## 3. Phase 1: SIEM Manager & Dashboard Deployment
The Wazuh Manager was deployed as a full-stack security engine.
* **Automation:** Utilized the Wazuh installation assistant to deploy the Indexer, Server, and Dashboard in a single automated workflow.
* **Security:** Configured SSL/TLS certificates for secure web access via Port 443 and established administrative role-based access.

![Wazuh Dashboard](./img/wazuh_dashboard.png)
*Figure 2: The centralized Wazuh dashboard indicating the manager is online and ready for telemetry.*

---

## 4. Phase 2: Cross-Platform Agent Deployment
I deployed telemetry agents across different operating systems to simulate a diverse corporate environment.
* **Linux Agent:** Enrolled a secondary Ubuntu Desktop instance using the Wazuh agent API.
* **Windows Agent:** Deployed the Wazuh MSI package via PowerShell on a Windows 10 endpoint.
* **Heartbeat Verification:** Confirmed that both agents were reporting real-time system data back to the manager node.

![Active Agents](./img/active_agents.png)
*Figure 3: Multi-OS visibility showing both Linux and Windows agents in an "Active" state.*

---

## 5. Phase 3: Threat Detection & MITRE Mapping
With the foundation built, I moved into active security monitoring:
* **FIM (File Integrity Monitoring):** Configured real-time monitoring of sensitive Windows Registry keys and Linux system files.
* **MITRE ATT&CK Correlation:** Validated that administrative escalations (e.g., `sudo` usage) were correctly mapped to Tactic **TA0004 (Privilege Escalation)**.
* **EDR Testing:** Generated "noise" through software installations to observe how the SIEM captures and categorizes system changes.

![Threat Hunting](./img/threat_hunting.png)
*Figure 4: Detailed event analysis showing logs correlated with specific MITRE ATT&CK techniques.*

---

## 6. Phase 4: Vulnerability & Compliance Auditing
The final phase involved using the SIEM as an auditing tool to improve the overall security posture.
* **CVE Identification:** Scanned endpoints for known vulnerabilities, identifying critical patches missing on the Windows host.
* **CIS Hardening:** Used the SCA (Security Configuration Assessment) module to audit the system against CIS Benchmarks, revealing configuration gaps.

![Vulnerability Report](./img/vulnerability_scan.png)
*Figure 5: Vulnerability dashboard highlighting high-severity security gaps and CVEs.*
