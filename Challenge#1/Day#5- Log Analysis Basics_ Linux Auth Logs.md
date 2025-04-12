# **Day#5: Log Analysis Basics – Linux Auth Log**

---

## 🎯 **Objective**  
The objective of this lab is to simulate an **SSH brute force attack** and demonstrate how to detect it using **Linux authentication logs**. Students will learn how to identify multiple failed login attempts and analyze patterns to uncover brute force activity.

---

## **▶️Video Tutorial**

[![▶️Watch the video](https://img.youtube.com/vi/6I0s-nh8j6k/maxresdefault.jpg)](https://youtu.be/6I0s-nh8j6k)
---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Attacker Machine:** Kali Linux (or any Linux with `hydra`)
- **Target Machine:** Ubuntu Linux Server

### **Tools Needed**
- `hydra` (on attacker machine)
- `openssh-server` (on target machine)
- `rsyslog` (default logging service)

### **Log Files**
- `/var/log/auth.log` – Authentication logs (Ubuntu/Debian)
- `/var/log/secure` – (CentOS/RHEL)

---

## 📘 **Preparation**

Linux systems log every authentication event, including successful and failed SSH login attempts. Brute force attacks can be identified by analyzing patterns such as:
- Rapid failed logins from a single IP
- Attempts with multiple usernames
- Login successes after a string of failures

---

## 🧠 **What is an SSH Brute Force Attack?**

A **brute force attack** attempts to guess a user’s SSH password by trying many combinations quickly using automated tools like Hydra.

### **Why It’s Dangerous**
- Successful brute force = full shell access  
- Attackers can pivot, install malware, or exfiltrate data  
- It often goes unnoticed without proper log monitoring

---

## 🛡️ **Attack Patterns Detectable via Auth Logs**
- Multiple failed password attempts from one IP
- Repeated login attempts to root/admin accounts
- Success after multiple failures (brute force success)
- Logins from unknown or foreign IPs

---

## What is Hydra?
- Hydra is a fast, open-source password-cracking tool used for brute force attacks on logins.
- It supports 50+ protocols like SSH, FTP, HTTP, SMB, and more.
- Common use: penetration testing and checking for weak passwords in network services.
- Syntax: `hydra -L users.txt -P passlist.txt <target_ip> <protocol>`
- Use `-l/-p` for single username/password or `-L/-P` for files.
- Add `-vV` for verbose output and `-t 4` to set number of threads.

## 🧪 **Lab Task: Explore and Analyze Auth Logs for SSH Brute Force**

---

### ⚔️ **Step 1: Attack Simulation – Brute Force SSH using Hydra**

> ⚠️ *Only perform on authorized systems you own or control.*

**On the Attacker Machine:**
```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://TARGET-IP
```
This will attempt multiple password guesses for user root on the SSH port.

Ensure SSH is enabled on the target:
```
sudo systemctl status ssh
```
### 🔍 Step 2: Detection and Analysis – Analyze Auth Logs
Check for failed login attempts:
```
sudo grep "Failed password" /var/log/auth.log
```
Find usernames tried:

```
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-5)}' | sort | uniq -c | sort -nr
```
Watch live log activity:

```
sudo tail -f /var/log/auth.log
```

### 🔍 What to Look For
- 20+ failed attempts from the same IP in under 5 mins
- Attempts on sensitive users (root, admin)
- Sudden success after multiple failures

## ✅ Conclusion
- Auth logs are vital for detecting brute force login attempts
- Multiple failures from a single IP is a strong signal of attack
- Combine log analysis with tools like fail2ban to block repeat offenders automatically

## 📸 Submission
Submit a screenshot showing:
- failed login entries from the same IP
- Username attempted
