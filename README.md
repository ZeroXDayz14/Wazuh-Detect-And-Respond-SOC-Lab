# 🛡️ Wazuh SOC Detection Lab – Multi Use Cases

## 📌 Project Overview

This project is a multi-use case Security Operations Center (SOC) home lab built using **Wazuh SIEM**. It demonstrates detection, analysis, and response across multiple attack scenarios, simulating real-world SOC workflows.

The lab focuses on:
- Log collection and analysis  
- Detection engineering using Wazuh rules  
- Attack simulation and validation  
- Automated and manual response actions  
- Analyst-style triage and investigation  

---

## 🏗️ Lab Architecture

![Architecture](screenshots/architecture.png)

### Environment Components:
- **Ubuntu Server** – Wazuh Manager, Indexer, Dashboard  
- **Windows 10 Endpoint** – Sysmon + Wazuh Agent  
- **Kali Linux** – Attacker machine  

---

## 🔎 Agent & Log Ingestion Verification

### Agent Connected
![Agent Active](screenshots/agent-active.png)

### Sysmon Logs Being Ingested
![Sysmon Logs](screenshots/agent-reading-sysmon.png)

---

## 🎯 Use Cases

| Use Case | Technique | Detection | Response |
|----------|----------|----------|----------|
| SSH Brute Force | Credential Access | Rule 5551 | IP Block |
| PowerShell Execution | Execution | Rule 100500 | Alert |
| PowerShell Download | Command & Control | Rule 100501 | Alert |
| Encoded PowerShell | Defense Evasion | Rule 100502 | Alert |
| Nmap Recon | Discovery | Detection Gap | None |

---

# 🔐 Use Case 1: SSH Brute Force Detection & Response

## Service Verification

![SSH Running](screenshots/ssh-service-running.png)

---

## Attack Simulation (Kali)

![Kali SSH Attempt](screenshots/kali-attack-source.png)

---

## Log Evidence (auth.log)

![Auth Log Evidence](screenshots/ssh-auth-log-evidence.png)

- Multiple failed login attempts observed  
- Source IP: **192.168.56.40**

---

## Initial Detection

![SSH Detection](screenshots/ssh-detection-details.png)

- **Rule ID:** 5760  
- Authentication failure events detected  

---

## Brute Force Detection

![Brute Force Alert](screenshots/ssh-bruteforce-alert.png)

- **Rule ID:** 5551  
- Multiple failed logins within short timeframe  

---

## Active Response Triggered

![Active Response](screenshots/active-response-triggered.png)

- Firewall-drop action executed  

---

## Firewall Evidence

![Firewall Rule](screenshots/firewall-blocked-ip.png)

- Attacker IP successfully blocked  

---

## Active Response Log (JSON)

![Active Response JSON](screenshots/active-response-json.png)

- Command executed: `firewall-drop`  
- Triggered by Rule 5551  

---

## Analyst Triage

- **Source IP:** 192.168.56.40  
- **Technique:** T1110 – Brute Force  
- **Severity:** High  
- **Verdict:** True Positive  
- **Action:** IP blocked automatically  

---

# 💻 Use Case 2: PowerShell Detection (Windows)

## Sysmon Event Evidence

### Process Creation (Event ID 1)
![Sysmon Event 1](screenshots/sysmon-local-events-ID-1.png)

---

### Network & DNS Activity (Event ID 3 & 22)
![Sysmon Events](screenshots/sysmon-local-events-ID-22-ID-3.png)

---

## Detection Query (Hunting)

![PowerShell Query](screenshots/powershell-commandline-evidence.png)

---

## Attack Simulation

![PowerShell Attack](screenshots/powershell-attack-command.png)

- Execution
- Web request
- Encoded command

---

## Custom Detection Rules

![Custom Rules](screenshots/custom-rules.png)

| Rule ID | Description |
|--------|------------|
| 100500 | PowerShell execution |
| 100501 | PowerShell download |
| 100502 | Encoded PowerShell |

---

## Detection Alerts

![Custom Alerts](screenshots/custom-detection-alerts.png)

- All attack variants successfully detected  
- Alerts generated with increased severity  

---

## Analyst Triage

- **Technique:** T1059.001 – PowerShell  
- **Technique:** T1105 – Tool Transfer  
- **Technique:** T1027 – Obfuscation  
- **Verdict:** True Positive  
- **Action:** Alert escalation  

---

# 🌐 Use Case 3: Nmap Reconnaissance

## Attack Simulation

![Nmap Scan](screenshots/reconnaissance-nmap-filtered.png)

- Target scanned from Kali Linux  

---

## Detection Gap

- No alerts generated in Wazuh  
- Demonstrates limitation of host-based SIEM  

👉 Requires:
- Network IDS (Suricata / Zeek)

---

# 📊 Wazuh Dashboard Overview

![Dashboard](screenshots/wazuh-dashboard-alerts.png)

---

## 🔍 Detection Strategy

- Linux detection via **auth.log (PAM events)**  
- Windows detection via **Sysmon telemetry**  
- Wazuh correlates logs and triggers alerts  
- Custom rules extend detection coverage  

---

## ⚡ Response Mechanisms

- **Active Response**
  - Automatic IP blocking via firewall  

- **Alert-Based Detection**
  - Requires analyst investigation  

---

## 🧬 MITRE ATT&CK Mapping

| Use Case | Technique |
|----------|----------|
| SSH Brute Force | T1110 |
| PowerShell Execution | T1059.001 |
| PowerShell Download | T1105 |
| Encoded PowerShell | T1027 |
| Nmap Recon | T1046 |

---

## 📚 Lessons Learned

- Built-in rules effectively detect brute force attacks  
- Sysmon provides strong visibility into endpoint activity  
- PowerShell detection requires tuning to reduce false positives  
- Host-based monitoring lacks visibility for network scans  
- Active response is powerful but must be controlled  

---

## 🚀 Future Improvements

- Integrate Suricata for network detection  
- Add threat intelligence enrichment  
- Expand detection use cases  
- Improve alert tuning  

---

## ⚠️ Disclaimer

This project was conducted in a controlled lab environment.  
All attacks were simulated on owned systems.

---

## 👤 Author

SOC Lab Project by **ZeroXDayz**

