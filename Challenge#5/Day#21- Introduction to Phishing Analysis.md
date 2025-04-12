# **Day#21- Phishing Analysis: Investigating a Suspicious Email**

---

## 🎯 **Lab Objective**

Learn how to analyze a phishing email by examining headers, body, URLs, and attachments. Understand different phishing types and techniques, and how to use open-source tools to investigate and extract Indicators of Compromise (IOCs).

---

## 📘 **What is Phishing Analysis?**

**Phishing Analysis** is the investigation of suspicious emails to determine if they’re crafted to trick users into revealing sensitive information or executing malware. This involves analyzing metadata, links, files, and content for signs of deception or malicious behavior.

---

## 🧨 **Types of Phishing Attacks**

| **Type**           | **Description**                                                        |
|--------------------|------------------------------------------------------------------------|
| **Email Phishing** | Generic emails pretending to be from trusted brands (e.g., Microsoft)  |
| **Spear Phishing** | Targeted phishing emails crafted for a specific person or department   |
| **Whaling**        | Spear phishing aimed at executives (CEO/CFO fraud)                     |
| **Smishing**       | Phishing via SMS messages with malicious links                         |
| **Vishing**        | Voice phishing calls pretending to be from IT/helpdesk                 |
| **Clone Phishing** | Re-sending a legitimate email with a malicious link or file replaced   |
| **Business Email Compromise (BEC)** | Impersonating senior staff to trick finance/HR teams into transferring money or data |

---

## 🎯 **Phishing Techniques with Examples**

| **Technique**                  | **Example**                                                                 |
|-------------------------------|------------------------------------------------------------------------------|
| **Display Name Spoofing**     | `From: Microsoft Support <helpdesk@micros0ft.com>`                          |
| **Lookalike Domains**         | `accounts@secure-paypai.com` instead of `paypal.com`                        |
| **URL Redirection**           | `http://bit.ly/securelogin` → redirects to phishing site                    |
| **HTML Form in Email**        | Fake login form embedded directly in the email body                         |
| **Macro-Based Document**      | "Open to enable content" launches PowerShell when macro is enabled          |
| **QR Code Phishing (Quishing)** | QR image in email leads to credential harvesting website                   |
| **Attachment-Only Phishing**  | `.zip` or `.docx` file with a malicious payload but no email text           |

---

## 🛠️ **Common Tools Used in Phishing Analysis**

| Tool              | Purpose                                     |
|-------------------|---------------------------------------------|
| **Email Header Analyzer** | Decode sender metadata and trace origin        |
| **VirusTotal**     | Scan email links and attachments for malware |
| **Hybrid Analysis / Any.Run** | Sandbox for dynamic file and URL behavior |
| **OLETools**       | Analyze Office macros in `.doc/.xls` files  |
| **CyberChef**      | Decode base64, hex, and obfuscated strings  |
| **Base64 Decoder** | Decode encoded payloads in email or script  |
| **Whois/IP Lookup**| Check sender domain and IP reputation       |

---

## 🧪 **Phishing Analysis Process**

| **Step** | **Action**                                                                 |
|---------|------------------------------------------------------------------------------|
| **1. Collect Email Sample** | Export the email as `.eml` or `.msg` format.                     |
| **2. Analyze Email Headers** | Review sender IP, Return-Path, SPF/DKIM/DMARC status.             |
| **3. Examine Body Content** | Check tone, language, branding, and urgency.                      |
| **4. Hover Over URLs** | Reveal if the actual link mismatches the display text.           |
| **5. Scan URLs and Files** | Use VirusTotal or a sandbox to examine behavior.               |
| **6. Decode Obfuscated Data** | Use CyberChef to decode base64, hex, or encoded scripts.         |
| **7. Extract Indicators** | Note malicious domains, IPs, file hashes, and sender addresses. |
| **8. Respond and Report** | Block in firewall/EDR, raise ticket, and alert users.             |

---

## 📎 **Suspicious Email Attachment Indicators**

| **Indicator**                         | **Example**                                  |
|--------------------------------------|----------------------------------------------|
| Executables disguised as documents   | `Invoice.pdf.exe`, `Resume.doc.scr`          |
| Encrypted ZIP files                  | Password-protected zip with `.exe` or `.js`  |
| Macro-enabled Office files           | `.docm`, `.xlsm` launching PowerShell scripts|
| Base64 or hex-encoded payloads       | Hidden in HTML or script content             |
| Unexpected themes (invoice, CV, notice)| Frequently used to grab user attention       |

---



##🧪 **Task: Investigating a Lookalike Domain Email**

### **Scenario:**
Your security team received a suspicious email claiming to be from PayPal. The sender address is:  
`noreply@secure-paypai.com`

Now, please answer below question

Question 1: What is the reputation of the domain?


### Submission
- Share the snapshot showing the reputation of teh domain
