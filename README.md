# 🛡️ Integrated SOC Lab: Detection Engineering & Threat Response Pipeline

![Architecture Diagram](Documentation/Project%20Diagram.png)

A production-like, isolated security operations lab built to demonstrate **end-to-end threat detection, automated response, and threat intelligence integration**. This project goes beyond simple tool setup to operationalize a full stack (Wazuh SIEM, TheHive/Cortex SOAR, OpenCTI TIP) against realistic adversary emulation.

## 🎯 Objectives Demonstrated
1.  **Operationalize Detection:** Build and tune detection logic (Wazuh rules) for high-fidelity alerts against critical MITRE ATT&CK techniques.
2.  **Automate Response:** Implement active response scripts for real-time threat mitigation (malware removal, IP blocking).
3.  **Integrate Security Tools:** Create a cohesive workflow from detection (Wazuh) to case management (TheHive), analysis (Cortex), and threat intelligence (OpenCTI).
4.  **Validate with Adversary Emulation:** Test detection efficacy against simulated advanced attacks in a controlled Active Directory environment.

## ⚙️ Lab Architecture
| Role | OS | Purpose |
|------|----|---------|
| **SIEM & Management** | Ubuntu Server | Wazuh Manager & Dashboard |
| **Domain Controller** | Windows Server 2022 | AD DS, DNS (Domain: `WinServ.local`) |
| **Windows Endpoint** | Windows 10 Pro | Domain-joined workstation, Sysmon, Wazuh Agent |
| **Linux Endpoint** | Ubuntu 22.04 | Linux client, Wazuh Agent, YARA |
| **Attacker** | Kali Linux | Adversary emulation & attack simulation |
| **SOAR/TIP Platform** | Docker Containers | TheHive, Cortex, OpenCTI, Redis, MinIO, RabbitMQ |

**Network:** Isolated VMware host-only subnet (`192.168.182.0/24`).

## 🔬 Core Capabilities & Integrations

### 🧠 Detection Engineering
- **Custom Detection Rules:** Developed Wazuh rules for AD attacks (DCSync, Kerberoasting, Golden Ticket), SSH brute-force, and suspicious file creation.
- **Log Source Integration:** Ingested Windows Security Events, Sysmon logs, Linux audit logs, and application logs into Wazuh.
- **False Positive Reduction:** Tuned rules based on lab activity to increase signal-to-noise ratio.

### ⚡ Automated Response
- **Active Response:** Configured Wazuh to automatically block attacker IPs (via `firewall-drop`) on SSH brute-force detection.
- **Malware Remediation:** Integrated scripts to remove malicious files identified by VirusTotal or YARA matches.
- **Threat Intelligence Enrichment:** Built a Python integration to send Nmap scan results to Google Gemini API for AI-powered service analysis and vulnerability context.

### 🧩 Toolchain Integration
- **VirusTotal:** API integration for hash reputation checks on files altered in monitored directories.
- **YARA:** On-access malware detection via Wazuh FIM events, using curated rulesets.
- **Full SOC Stack:** Deployed and linked TheHive (case management), Cortex (automated analyzers), and OpenCTI (threat intelligence) via Docker.

## 🧪 Attack Simulations & Detection Analysis
Simulated advanced attacks to validate detection coverage and practice investigative workflow.

| Attack (MITRE ID) | Tools | Detection Method | Key Investigation Steps |
|-------------------|-------|------------------|-------------------------|
| **Kerberoasting** | Mimikatz, `tgsrepcrack.py` | Wazuh Rule on Event ID 4769 (specific encryption flags) | 1. Correlate with process creation (Sysmon) 2. Identify requested SPN & user 3. Check service account privilege level |
| **DCSync** | Mimikatz (`lsadump::dcsync`) | Wazuh Rule on Event ID 4662 (directory replication rights) | 1. Immediately treat as critical. 2. Identify source host and user. 3. Verify if account is authorized for replication. |
| **Pass-the-Hash** | Mimikatz (`sekurlsa::pth`) | Wazuh alerts on NTLM authentication anomalies and lateral movement | 1. Trace pass-the-hash to destination system logons. 2. Review source host for prior compromise. |
| **SSH Brute-Force** | Hydra | Custom Wazuh correlation rule + Active Response | 1. Confirm multiple failed auth attempts from single IP. 2. Execute automatic firewall block. 3. Review blocked IP for other malicious activity. |
| **LLMNR/NBT-NS Poisoning** | Responder | Detection via anomalous NTLMv2 authentication requests | 1. Identify poisoned name resolution requests. 2. Locate misconfigured client attempting to access non-existent shares. |


## 🚀 Getting Started
1.  **Clone the repo:** `git clone https://github.com/BouraouiMalek/Wazuh-Lab.git`
2.  **Review Documentation:** The comprehensive guide details VM setup, network configuration, and step-by-step deployment.
3.  **Replicate the Lab:** Use the provided config snippets and instructions to build your own isolated environment.

## 👨‍💻 Author
**Malek Bouraoui**  
Security-Focused Engineer | Detection Builder  
This project serves as a hands-on deep dive into building and operating a modern threat detection and response stack from the ground up.

🔗 [LinkedIn](https://www.linkedin.com/in/malek-bouraoui/) • 🔗 [GitHub](https://github.com/BouraouiMalek)

---
*“This lab bridges the gap between security theory and operational practice, proving detection logic and automating response workflows in a controlled environment.”*
