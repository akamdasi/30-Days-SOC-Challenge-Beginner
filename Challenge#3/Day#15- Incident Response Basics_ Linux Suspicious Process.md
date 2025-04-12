# **Day#15: Incident Response Basics: Linux Suspicious Process**

---

## 🎯 **Objective:**  
To investigate and respond to a **suspicious background process** running on a Linux machine, simulating malware or a stealthy backdoor. Students will learn how to identify abnormal processes, trace binaries, and take action.

---

## 📘 **Why It Matters**

Attackers often run malicious binaries in the background and try to hide their process names or use legit-sounding names like `kworker`, `updater`, or `syslogd`. Detecting these is crucial in real-world IR.

---

## 🔁 **Incident Response Process (NIST SP 800-61 Rev. 2)**

| **Phase**                         | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **1. Preparation**               | Baseline your system’s normal running processes and enable process auditing.     |
| **2. Detection and Analysis**    | Use tools like `ps`, `lsof`, and `netstat` to identify suspicious processes.     |
| **3. Containment, Eradication, and Recovery** | Kill the process, investigate its binary, and delete or quarantine it.          |
| **4. Post-Incident Activity**    | Document behavior, clean up remnants, and build detection rules.                 |

---

## ⚠️ **Scenario: Unknown Process 'kupdate' Found Running in Background**

During routine checks, you spot a process named `kupdate` running — but it’s not part of your system’s normal activity.

---

## 🛠️ **Lab Setup**

### **System Requirements:**
- Any Linux system (Ubuntu/Kali recommended)
- sudo/root access

### **Simulate the Suspicious Process:**

1. Create a fake malicious script:
```bash
echo -e '#!/bin/bash\nwhile true; do sleep 60; done' > /usr/local/bin/kupdate
chmod +x /usr/local/bin/kupdate
```
2. Run it in the background:

```
nohup /usr/local/bin/kupdate &
```

## 🧪 Step-by-Step Investigation

### Step 1. Detect Unknown Background Process
```
ps aux | grep kupdate
```
Or use:

```
top
```
### Step 2. Identify Executable and Open Files
```
which kupdate
ls -l /usr/local/bin/kupdate
lsof -p <PID>
```
### Step 3. Check If Process Is Making Network Connections
```
netstat -plant | grep <PID>
```
It shouldn't have any unless it's suspicious

### Step 4. Containment and Eradication
- Kill the process:
```
kill <PID>
```
Or:

```
pkill kupdate
```
- Remove the binary:
```
rm -f /usr/local/bin/kupdate
```
### Step 5. Post-Incident Activity
- Document:
 - What process was found?
 - Was it scheduled or persistent?
 - What path did it use?

- Recommendations:
 - Monitor for unknown processes using auditd or psad
 - Use allowlists for running binaries
 - Run weekly system baselines

## Lab Checklist
Task	Description
✅ Simulate Hidden Process	Create and run a background binary named kupdate
✅ Detect via ps/top	Use commands to find abnormal processes
✅ Investigate	Use lsof, netstat, and which
✅ Kill & Remove	Terminate the process and delete the binary
✅ Document	Write findings and recommend improvements

## 📸 Submission
Submit screenshots showing:
- Output of ps aux | grep kupdate
- Binary path and file details
- kill or pkill output
- File deletion of /usr/local/bin/kupdate
