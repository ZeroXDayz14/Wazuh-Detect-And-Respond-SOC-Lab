# 🔐 Use Case: Encoded PowerShell Detection

## 🎯 Objective
Detect obfuscated PowerShell commands using base64 encoding.

---

## ⚔️ Attack Simulation

Command executed:
```powershell
powershell -enc <base64_string>
```

![Encoded](../screenshots/powershell-attack-command.png)

---

## 📄 Log Source

- Sysmon Event ID 1

---

## 🔍 Detection Logic

- Base Rule: **92027**
- Custom Rule: **100502**

```xml
<rule id="100502" level="13">
  <if_sid>92027</if_sid>
  <match>-enc</match>
  <description>Custom: Encoded PowerShell detected</description>
</rule>
```

---

## 🚨 Alert Evidence

![Alerts](../screenshots/custom-detection-alerts.png)

---

## 🧠 Analyst Triage

- **Indicator:** Encoded command  
- **Technique:** T1027 – Obfuscation  
- **Severity:** High  
- **Verdict:** True Positive  

---

## 📚 Lessons Learned

- Encoded commands are a strong indicator of malicious intent  
- High-priority alerting is appropriate for this behavior  
