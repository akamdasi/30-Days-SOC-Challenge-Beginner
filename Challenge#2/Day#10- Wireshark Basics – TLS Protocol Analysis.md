# **Day#10: Wireshark Basics – TLS Protocol Analysis**

---

## 🎯 **Objective**  
The objective of this lab is to help students analyze **TLS (Transport Layer Security)** traffic using **Wireshark**. Students will explore how TLS secures data over the network, understand handshake messages, and identify metadata like server names and certificate details.

---

## 🛠️ **Lab Setup**

### **System Requirements**
- **Operating System:** Windows 10/11 (or Linux/macOS)
- **Software:** Wireshark (latest version)

### **Files Needed**
- [Download Sample PCAP file](https://github.com/0xrajneesh/90-Days-SOC-Challenge-Beginner/raw/refs/heads/main/Protocol_Analysis_pcap.pcapng)

---

## 📘 **TLS Packet Structure and Fields**

TLS is a **cryptographic protocol** that provides secure communication over the internet. It runs over **TCP**, commonly on port **443**, and is used in HTTPS, FTPS, SMTPS, etc.

### **Key TLS Handshake Messages:**

| Message Type          | Description                                      |
|------------------------|--------------------------------------------------|
| **Client Hello**       | Client initiates secure connection, offers cipher suites |
| **Server Hello**       | Server selects cipher and provides certificate  |
| **Certificate**        | Server provides digital certificate (X.509)     |
| **Key Exchange**       | Client and server exchange keys for session     |
| **Finished**           | Secure session begins                           |

---

## 🔍 **Most Common TLS Display Filters**

Use these filters in Wireshark’s **Display Filter** bar:

| Filter                        | Description                              |
|-------------------------------|------------------------------------------|
| `tls`                        | Show all TLS traffic                     |
| `tcp.port == 443`            | TLS over HTTPS                           |
| `tls.handshake.type == 1`    | Client Hello messages                    |
| `tls.handshake.type == 2`    | Server Hello messages                    |
| `tls.record.version == 0x0303`| TLS 1.2 traffic                         |
| `tls.record.version == 0x0304`| TLS 1.3 traffic                         |

---

✅ Conclusion
- TLS secures communication using encryption, making traffic unreadable without keys.
- Wireshark can't decrypt TLS by default but can reveal:
 - Server name (SNI)
 - Certificate chain
 - TLS versions and cipher suites

- Analyzing TLS metadata helps detect:
 - Outdated TLS versions (e.g., TLS 1.0)
 - Suspicious or self-signed certificates
 - Malicious domain encryption abuse

## 📸 Submission
Submit a screenshot showing:
- Show all TLS traffic
- Show Client Hello messages
- Show TLS 1.2 traffic   

