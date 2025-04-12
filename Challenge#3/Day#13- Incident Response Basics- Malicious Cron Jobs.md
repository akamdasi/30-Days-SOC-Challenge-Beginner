# **Day#13: Detecting and Removing Malicious Cron Jobs – Linux Incident Response Lab**

---

## 🎯 **Objective:**  
The objective of this lab is to investigate and respond to a **malicious cron job** used by an attacker to maintain persistence on a Linux system. Students will simulate the attack, detect the malicious scheduled task, analyze the script, and remove the threat — applying the full incident response lifecycle.

---

## 📘 **What is a Cron Job?**

A **cron job** is a scheduled task that runs automatically at defined intervals on Unix/Linux systems. Attackers often use cron to **re-execute payloads**, reconnect to command-and-control servers, or maintain access to a compromised system.

---

## 🔁 **Incident Response Process (NIST SP 800-61 Rev. 2)**

| **Phase**                         | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **1. Preparation**               | Ensure system logging is active and users are trained to detect unusual cron behavior. |
| **2. Detection and Analysis**    | Identify unauthorized cron entries and investigate associated scripts or IP addresses. |
| **3. Containment, Eradication, and Recovery** | Stop the malicious cron activity, remove the script, and restore system configuration. |
| **4. Post-Incident Activity**    | Document the incident, and set alerts for future cron job changes.              |

---

## ⚠️ **Scenario: A Malicious Cron Job is Running Every Minute**

An attacker has added a cron job that silently runs a malicious script from `/tmp` every minute. Your job is to detect it, understand its behavior, and remove it safely.

---

## 🛠️ **Lab Setup**

### **System Requirements:**
- Ubuntu 20.04/22.04 or Kali Linux
- Terminal with sudo access

## **Simulate the Incident:**

1. Create a fake "malicious" script:
```bash
echo -e '#!/bin/bash\necho "Ping from attacker server" >> /tmp/.cron.log' > /tmp/malicious.sh
chmod +x /tmp/malicious.sh
```
2. Add a cron job for the current user:
```
(crontab -l; echo "* * * * * /tmp/malicious.sh") | crontab -
```

## 🧪 Step-by-Step Investigation

### Step 1. Preparation
- Make sure cron is installed and running:
```
sudo systemctl status cron
```
- Enable logging (cron logs are usually in /var/log/syslog or /var/log/cron).

### Step 2. Detection and Analysis
- Check for suspicious cron entries:
```
crontab -l
```
- Search cron directories for unauthorized jobs:
```
grep -r "/tmp/" /etc/cron* /var/spool/cron/crontabs
```
- Review logs to confirm execution:
```
cat /tmp/.cron.log
```
- Analyze the script:
```
cat /tmp/malicious.sh
```
### Step 3. Containment, Eradication, and Recovery
- Remove the malicious cron job:
```
crontab -l | grep -v "malicious.sh" | crontab -
```
- Delete the script and its output:
```
rm -f /tmp/malicious.sh /tmp/.cron.log
```
- Restart the cron service:
```
sudo systemctl restart cron
```
### Step 4. Post-Incident Activity
- Document the following:
 - When the cron job was added
 - What the script was doing
 - Any signs of lateral movement or download activity

- Recommendations:
 - Restrict cron job access to authorized users only
 - Enable cron integrity checks
 - Set up alerts for new cron entries (using auditd or inotify)

## Lab Checklist

✅ Simulate Cron Job	Create a malicious script and schedule it via cron
✅ Investigate	Detect the cron job and examine the script behavior
✅ Respond	Remove the script and the cron entry
✅ Document	Record all findings and suggest prevention steps

## 📸 Submission
Submit screenshots showing:
- crontab -l output with the malicious job
- Contents of the cron script /tmp/malicious.sh
- Logs confirming the script execution
- Cleaned cron job list and deletion confirmation


