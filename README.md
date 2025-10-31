# 🧠 Wazuh SOC Lab — Threat Detection & Response Project

![Wazuh SOC Lab Diagram](Documentation/Project%20Diagram.png)

## 📌 Overview
This project is a **fully isolated SOC (Security Operations Center) lab** built from scratch to simulate real-world cyberattacks and detect them using **Wazuh SIEM**.

It includes **Active Directory**, multiple endpoints, and an attacker machine to test detection and automated response for various attack scenarios.

---

## ⚙️ Lab Environment

| Component | Description |
|------------|-------------|
| **Windows Server 2022** | Domain Controller (AD DS, DNS) |
| **Windows 10** | Workstation joined to domain |
| **Ubuntu Server** | Wazuh SIEM & Manager |
| **Ubuntu Desktop** | Linux endpoint with agent |
| **Kali Linux** | Attacker machine |
| **Network** | Isolated VMnet1 subnet (192.168.182.0/24) |

---

## 🔍 Main Features
- **Active Directory attack simulations**  
  DCSync, Golden Ticket, Kerberoasting, Pass-the-Hash, SMB Relay  
- **Brute-force detection and automatic IP blocking**
- **VirusTotal integration** for malware verification  
- **YARA integration** for local malware detection  
- **AI-powered alert enrichment** using Gemini + Nmap  
- **Custom Wazuh rules, decoders, and active responses**

---

## 🧪 Attack Simulations
- **DCSync (Mimikatz)**
- **Kerberoasting**
- **Golden Ticket**
- **Pass-the-Hash**
- **NTDS Extraction**
- **SSH Brute-Force**
- **LLMNR & SMB Relay**

Each attack was detected and correlated in **Wazuh Dashboard** with custom rules and active responses.

---

## 🧰 Integrations & Automation
- **VirusTotal API** → Hash analysis and threat verification  
- **YARA Rules** → File integrity monitoring and malware detection  
- **Active Response Scripts** → Automatic threat removal and firewall drops  
- **Gemini AI Integration** → Enrich alerts with vulnerability context  
- **Nmap Automation** → Periodic network scanning via Wazuh agent

---

## 🧠 Goals
- Build a realistic SOC environment from scratch  
- Understand blue-team detection and incident response techniques  
- Automate malware detection and response  
- Combine security monitoring with AI-based analysis  

---

## 👨‍💻 Author
**Malek Bouraoui**  
Software Engineer | Aspiring SOC Analyst  
📍 Tunisia  
🔗 [LinkedIn](https://www.linkedin.com/in/malek-bouraoui/)  
🔗 [GitHub](https://github.com/BouraouiMalek)

---

⭐ Learning by doing — turning theory into practice.
