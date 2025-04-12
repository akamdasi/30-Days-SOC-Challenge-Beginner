# **Day#22- Phishing Analysis: Investigating a Suspicious Lookalike Email**

---

## 🎯 **Lab Objective**

The objective of this lab is to analyze a real-world phishing email sample using manual investigation techniques. Students will learn to review email headers, validate the sender's identity, check domain/IP reputation, and extract indicators of compromise (IOCs).

---

## 🛠️ **Lab Setup**

- 📨 [Download Email Sample (.eml)](https://github.com/0xrajneesh/30-Days-SOC-Challenge-Beginner/blob/main/BRADESCO%20LIVELO.eml)  
- 💻 Tools Recommended:
  - [MX Toolbox Email Header Analyzer](https://mxtoolbox.com/EmailHeaders.aspx)
  - [EML Analyzer](https://eml-analyzer.herokuapp.com/#/)
  - IP reputation check (e.g., VirusTotal, AbuseIPDB, Cisco Talos)
  - Whois lookup (e.g., whois.domaintools.com)
  - URL and Domain analysis (e.g., urlscan.io, VirusTotal)

---

## 🧪 **Lab Task: Analyze the Suspicious Email**

### 📥 Scenario:  
You received an email from **BANCO DO BRADESCO LIVELO** claiming that your card has **92,990 points expiring today**, sent from `banco.bradesco@atendimento.com.br`. The sender’s domain looks similar to Bradesco’s official domain.

Investigate and answer the following:

---

### 🔍 **Questions:**

1. **What is the full email address of the sender?**  
2. **What domain is used to send this email?** (Check Return-Path or From)
3. **What is the sender’s IP address from the header?**  
4. **Is the sender IP blacklisted?** (Check using AbuseIPDB or VirusTotal – Answer Yes/No)  
5. **What is the result of SPF authentication?** (Pass / Fail / Neutral)  
6. **What is one suspicious URL or link found in the email body?**  


---


## 📸 **Submit the Following Screenshots:**

1. Screenshot of the email header with sender, Return-Path, and IP address highlighted.  
2. Screenshot of the IP reputation lookup result (AbuseIPDB or VirusTotal).  
3. Screenshot of the suspicious link found in the email body.  
4. Screenshot of the email content or HTML preview that shows urgency, branding, or spoofing.  

## ✅ **Learning Outcome**

By the end of this lab, students should be able to:
- Trace email origin
- Validate domains and IPs
- Understand spoofing techniques
- Detect phishing attempts using header and body analysis
