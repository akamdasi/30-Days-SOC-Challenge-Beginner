# **Day#4: Log Analysis Basics – Network-Based Attack Detection Using UFW**

---

## 🎯 **Objective**  
The objective of this lab is to simulate a **network-based port scan attack** and demonstrate how to detect it using **ufw.log** logs on a Linux system. Students will learn how to launch the HTTP scan prob from Kali Linux(attacker) machine and detect these scan ataempt on Victim machine using UFW.

---

## **▶️Video Tutorial**

[![▶️Watch the video](https://img.youtube.com/vi/8A0vkpDPmxM/maxresdefault.jpg)](https://youtu.be/8A0vkpDPmxM)
---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Attacker Machine:**: Kali Linux
- **Target Machine**: Ubuntu Linux

### **Tools Needed**
- `nmap` (on attacker machine)
- `ufw` or `iptables` (on target machine)

### **Log Files**
- `/var/log/ufw.log` on Ubuntu Server– Captures system and network-related messages

---

## 🧠 **What is a Network Port Scan?**

A **port scan** is a technique used by attackers to probe a system for open ports and active services. Tools like `nmap` are commonly used to map a system’s network surface.

### **Why It’s Dangerous**
- Port scans are often a **precursor to exploitation**
- They help attackers identify vulnerable services like open SSH, FTP, or outdated web servers

---

### What is Nmap?
- Nmap (Network Mapper) is an open-source network scanning tool.
- Used to discover hosts and services on a network.
- Helps in identifying open ports, running services, and OS detection.
- Commonly used for network inventory and vulnerability scanning.

---

### Nmap Popular Scan Types
- SYN Scan (-sS): Fast and stealthy port scan.
- TCP Connect Scan (-sT): Full TCP connection, less stealthy.
- UDP Scan (-sU): Scans UDP ports for services.
- Ping Scan (-sn): Checks which hosts are up, no port scan.

### 🔐 What is UFW?
- UFW stands for Uncomplicated Firewall, a frontend for iptables.
- Simplifies firewall management for Linux users.
- Used to allow, deny, and manage traffic rules easily.
- Logs are stored in `/var/log/ufw.log`.
- Rule file `/etc/ufw/before.rules`
- To check ufw status `ufw status`
- To check the rule number `ufw status numbered`

###🧾 UFW Rule Syntax
- Basic allow rule: ufw allow <port>
- Deny a port: ufw deny <port>
- Allow by service: ufw allow <service> (e.g., ufw allow ssh)
- Allow by IP: ufw allow from <IP>
- Allow specific port from IP: ufw allow from <IP> to any port <port>
- Delete rule: ufw delete allow <port>



## 🧪 **Lab Task: Explore and Analyze Linux Syslog for Network Scans**

---

### ⚔️ **Step 1: Attack Simulation – Perform a Port Scan**

> ⚠️ *Only scan systems you own or are authorized to test.*

**On the Attacker Machine:**
```bash
nmap -p80 TARGET-IP
```


### 🔍 Step 2: Detection and Analysis – Analyze Syslog

1. Installing UFW firewall
   ```
   sudo apt install ufw
   sudo ufw enable
   sudo ufw logging on
   sudo ufw logging high
   ```
2. Create a Firewall rule to drop HTTP traffic from Attack machine
   ```
   sudo ufw deny from 69.62.84.69 to any port 80 proto tcp
   ```
3. Reload the firewall rules to take effect
   ```
   sudo ufw reload
   ```
4. Detect the HTTP Scanning traffic
   ```
   sudo tail -f /var/log/ufw.log | grep "Attcker IP"
   ```


## ✅ Conclusion
- ufw.log, combined with firewall logs, is powerful for detecting early-stage reconnaissance
- Port scanning is often the first indicator of an attacker mapping your system
- Detecting and blocking IPs performing scans is a crucial step in proactive defense

## 📸 Submission
Submit a screenshot of a syslog entry showing blocked network traffic due to a port scan. Include:
- Source IP of scan
- Targeted port
- Timestamp


