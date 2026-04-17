# 🔐 Use Case: SSH Brute Force Detection & Response

## 🎯 Objective
Detect and respond to repeated SSH login failures indicating a brute-force attack.

---

## ⚔️ Attack Simulation

- Attacker machine: Kali Linux (192.168.56.40)
- Target: Ubuntu Wazuh Manager

Command used:
```bash
ssh root@192.168.56.10
```

Multiple failed login attempts were generated.

---

## 📄 Log Source

- File: `/var/log/auth.log`
- Service: SSH (sshd)

![Auth Log](../screenshots/ssh-auth-log-evidence.png)

---

## 🔍 Detection Logic

- Initial Rule: **5760** (SSH authentication failure)
- Correlation Rule: **5551** (multiple failed logins)

![Detection](../screenshots/ssh-detection-details.png)

---

## 🚨 Alert Evidence

![Brute Force Alert](../screenshots/ssh-bruteforce-alert.png)

- Rule triggered after multiple failures in short timeframe

---

## ⚡ Response Action

- Active response triggered: `firewall-drop`

![Active Response](../screenshots/active-response-triggered.png)

---

## 🔒 Containment Evidence

![Firewall Rule](../screenshots/firewall-blocked-ip.png)

- Attacker IP successfully blocked

---

## 🧠 Analyst Triage

- **Source IP:** 192.168.56.40  
- **Target User:** root  
- **Technique:** T1110 – Brute Force  
- **Severity:** High  
- **Verdict:** True Positive  

---

## 📚 Lessons Learned

- Built-in Wazuh rules effectively detect brute-force attacks  
- Active response provides immediate containment  
- Requires tuning in production to avoid false positives  
