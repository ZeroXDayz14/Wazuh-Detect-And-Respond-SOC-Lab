# Detection Rules

This folder contains custom Wazuh rules used in the lab.

## Files

### `local_rules.xml`
Custom detection rules for PowerShell activity.

## Custom Rules Included

### Rule `100500`
Detects PowerShell execution activity.

**Purpose:**  
Raise visibility when `powershell.exe` is executed on the Windows endpoint.

### Rule `100501`
Detects PowerShell download behavior.

**Purpose:**  
Trigger when `Invoke-WebRequest` appears in the command line, indicating file retrieval or remote content access.

### Rule `100502`
Detects encoded PowerShell commands.

**Purpose:**  
Trigger when `-enc` appears in the command line, which is commonly associated with obfuscated execution.

## Detection Strategy

These rules build on Wazuh’s existing PowerShell-related detections and increase severity for lab scenarios that are commonly associated with malicious behavior.

## Tuning Considerations

In a production environment, these rules would need tuning to reduce false positives. Legitimate administration, scripting, and software management can also involve:
- PowerShell execution
- web requests from PowerShell
- encoded commands in rare cases

## Lab Context

These rules were created for a controlled home lab and were used to validate alert generation and analyst triage workflows.
