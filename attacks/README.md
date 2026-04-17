# 📂 SOC Attack Use Cases

This directory contains detailed Security Operations Center (SOC) use cases developed as part of a Wazuh SIEM home lab.

Each file represents a simulated attack scenario, including:
- Attack execution
- Log analysis
- Detection logic
- Alert evidence
- Response actions (if applicable)
- Analyst triage

---

## 🎯 Purpose

These use cases demonstrate hands-on experience with:
- Threat detection using SIEM (Wazuh)
- Log analysis from Linux and Windows systems
- Detection engineering with custom rules
- Incident investigation and triage
- Understanding detection gaps and limitations

---

## 📚 Use Cases Overview

### 🔐 SSH Brute Force Detection & Response
- Detects repeated failed SSH login attempts  
- Uses Wazuh rule **5551** for correlation  
- Triggers **active response (firewall block)**  

👉 [View Full Case Study](ssh-bruteforce.md)

---

### 💻 PowerShell Execution Detection
- Detects execution of PowerShell processes  
- Based on **Sysmon Event ID 1**  
- Uses custom rule **100500**  

👉 [View Full Case Study](powershell-execution.md)

---

### 🌐 PowerShell Download Detection
- Detects file download via `Invoke-WebRequest`  
- Monitors command-line activity  
- Uses custom rule **100501**  

👉 [View Full Case Study](powershell-download.md)

---

### 🔐 Encoded PowerShell Detection
- Detects obfuscated PowerShell commands (`-enc`)  
- Indicates potential malicious activity  
- Uses custom rule **100502**  

👉 [View Full Case Study](powershell-encoded.md)

---

### 🌐 Nmap Reconnaissance
- Simulates network scanning activity  
- Demonstrates **detection gap** in host-based SIEM  

👉 [View Full Case Study](reconnaissance-nmap.md)

---

## 🔍 Detection Coverage Summary

| Use Case | Data Source | Detection Type | Response |
|----------|------------|---------------|----------|
| SSH Brute Force | Linux auth.log | Correlation Rule | Active Response |
| PowerShell Execution | Sysmon | Custom Rule | Alert |
| PowerShell Download | Sysmon | Custom Rule | Alert |
| Encoded PowerShell | Sysmon | Custom Rule | Alert |
| Nmap Recon | Network | Not Detected | None |

---

## 🧠 Lessons Learned

- SIEM detection depends heavily on log sources  
- Sysmon significantly improves endpoint visibility  
- Correlation rules are effective for identifying attack patterns  
- Custom rules allow detection of specific attacker behavior  
- Host-based SIEM has limitations for network-level attacks  

---

## ⚠️ Disclaimer

All activities were performed in a controlled lab environment for educational purposes only.  
No unauthorized systems were targeted.
