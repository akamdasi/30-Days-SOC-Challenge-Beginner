# 📘 Introduction to Linux Logs + Cheat Sheet

Linux logs are essential for **system monitoring, debugging, troubleshooting, and security analysis**. Understanding how to access and interpret these logs is a foundational skill for system administrators, DevOps engineers, and security analysts.

---

## 📂 Where Are Linux Logs Stored?

Most logs in Linux are stored in the `/var/log/` directory.

---

## 📄 Common Log Files

| Log File                         | Description                                      |
|----------------------------------|--------------------------------------------------|
| `/var/log/syslog` / `messages`   | General system activity logs                     |
| `/var/log/auth.log`              | Authentication logs (login, sudo, ssh)           |
| `/var/log/kern.log`              | Kernel messages                                  |
| `/var/log/dmesg`                 | Boot-time and hardware-related messages          |
| `/var/log/faillog`              | Failed login attempts                            |
| `/var/log/secure`                | Security-related logs (RHEL/CentOS)              |
| `/var/log/boot.log`              | System boot logs                                 |
| `/var/log/cron` or `cron.log`    | Cron job scheduling logs                         |
| `/var/log/httpd/`                | Apache web server logs                           |
| `/var/log/audit/`                | SELinux and AuditD logs                          |

---

## 🧠 Linux Logs Cheat Sheet

### 🔍 View Logs

```bash
cat /var/log/syslog              # Display entire log
less /var/log/auth.log           # Scroll through logs
tail -f /var/log/syslog          # Live log monitoring
journalctl                       # View systemd journal logs

### 📌 Filter Logs
```bash
grep "error" /var/log/syslog                     # Search for 'error'
journalctl -u ssh                                # Logs for SSH service
journalctl --since "1 hour ago"                  # Logs from the past hour
journalctl --since "2024-10-01" --until "2024-10-02"  # Logs between two dates
```


### 🛠️ Useful Log Management Commands
```bash
dmesg | less                        # View kernel ring buffer
logrotate -d /etc/logrotate.conf   # Test log rotation
last                               # Show login history
lastb                              # Show failed login attempts
```
###🧾 Example: Detect Failed SSH Logins
```bash
grep "Failed password" /var/log/auth.log
```
### 🔐 Why Are Logs Important?
- 🔍 Security Monitoring – Detect brute force attacks, unauthorized logins.
- 🛠️ Troubleshooting – Identify service errors and system crashes.
- 📜 Auditing – Track user activity and system changes.

