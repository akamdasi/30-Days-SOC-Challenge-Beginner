# **Day#14: Detecting Suspicious PowerShell Activity – Windows Incident Response Lab**

---

## 🎯 **Objective:**  
The objective of this lab is to simulate and investigate a **suspicious PowerShell command** on a Windows system. Students will learn how to detect PowerShell-based threats using built-in logs, analyze activity using Event Viewer, and perform basic incident response actions.

---

## 📘 **Why PowerShell Matters in Incident Response**

**PowerShell** is a powerful tool for system administration — but it’s also commonly used by attackers to download malware, move laterally, and execute hidden scripts. Proper logging and monitoring can help detect abuse.

---

## 🔁 **Incident Response Process (NIST SP 800-61 Rev. 2)**

| **Phase**                         | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **1. Preparation**               | Enable PowerShell logging and ensure security auditing is in place.            |
| **2. Detection and Analysis**    | Identify and investigate PowerShell misuse in logs.                            |
| **3. Containment, Eradication, and Recovery** | Kill malicious processes, remove scripts, and secure PowerShell usage.         |
| **4. Post-Incident Activity**    | Document findings and improve PowerShell restrictions and monitoring.          |

---

## ⚠️ **Scenario: Suspicious PowerShell Command Executed**

A user accidentally ran a PowerShell command that simulates suspicious behavior — like contacting a remote server and writing data to disk. You must detect and analyze this command through system logs.

---

## 🛠️ **Lab Setup**

### **System Requirements:**
- Windows 10/11 or Server 2019/2022
- Admin rights or access to Group Policy
- Event Viewer

### **Enable PowerShell Logging:**

1. Open `gpedit.msc`
2. Go to:  
   `Computer Configuration → Administrative Templates → Windows Components → Windows PowerShell`
3. Enable:
   - **Turn on Module Logging**
   - **Turn on Script Block Logging**

Logs will appear here:  
`Event Viewer → Applications and Services Logs → Microsoft → Windows → PowerShell → Operational`

---

## 🧪 **Step-by-Step Investigation**

### **1. Simulate Suspicious PowerShell Activity**

Open **PowerShell as Administrator** and run:

```powershell
Invoke-Expression "Write-Output 'Connecting to http://test.com' | Out-File -FilePath $env:TEMP\testlog.txt"
```

This simulates:

An obfuscated command using Invoke-Expression

Network-like behavior (Connecting to)

File write to the temp directory

### Step 2. Detect and Analyze the Activity
- Open Event Viewer
Navigate to:
`Applications and Services Logs → Microsoft → Windows → PowerShell → Operational`

- Filter by Event ID 4104 (Script Block Logging)
Look for the full command executed

Confirm:

The use of Invoke-Expression

The output path: %TEMP%\testlog.txt

The user who ran it

### Step 3. Containment and Eradication
- Remove the file:
```
Remove-Item "$env:TEMP\testlog.txt"
```
- Check for additional PowerShell script files:
```
Get-ChildItem -Path C:\Users\ -Filter *.ps1 -Recurse
```
- Kill PowerShell process if still active (via Task Manager)

## Step 4. Post-Incident Activity
- Document the incident:
 - What command was executed?
 - Which user ran it?
 - What was the intent or risk?

- Recommendations:
 - Monitor for Invoke-Expression and IEX usage
 - Restrict PowerShell with Constrained Language Mode
 - Route logs to SIEM for alerting on key PowerShell behaviors

## Lab Checklist
Task	Description
✅ Enable Logging	Ensure PowerShell operational logs are active
✅ Simulate Suspicious Command	Use Invoke-Expression and write to disk
✅ Analyze Logs	Investigate the command via Event ID 4104
✅ Remove File	Delete the generated log file
✅ Document and Recommend	Create a short report on findings

## Submission
Submit screenshots showing:
- The PowerShell Operational log with Event ID 4104
- Highlighted use of Invoke-Expression
- The test file before deletion (testlog.txt)
- The command used to remove the file
