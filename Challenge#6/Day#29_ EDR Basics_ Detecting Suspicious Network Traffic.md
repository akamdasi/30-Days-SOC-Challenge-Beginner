# Day#29: EDR Basics - Detecting Suspicious Network Traffic using Suricata

---

## 🎯 Objective

To understand how an Endpoint Detection and Response (EDR) solution can detect suspicious network traffic using Suricata IDS and visualize alerts on Wazuh.

---

## 📚 What is Suspicious Network Traffic?

Suspicious network traffic refers to abnormal or unexpected activities on a network that may indicate malicious intent or an ongoing attack.

### 🔍 Examples:
- A machine scanning multiple ports on the network (e.g., Nmap Scan).
- Traffic to known malicious IPs (Command & Control).
- FTP uploads on non-standard ports.
- HTTP connections to rare domains or IPs.

---

## 🔐 How are IDSs Helpful?

Intrusion Detection Systems (IDS) provide the following benefits:

- Monitor and inspect network traffic in real time.
- Trigger alerts when known attack patterns are detected.
- Help detect reconnaissance, malware communication, and lateral movement.
- Provide visibility to SOC teams for early-stage attacks.

---

## ⚙️ How Does IDS Work?

1. **Packet Capture**: Captures and inspects each packet.
2. **Rule Matching**: Matches traffic patterns against rule sets.
3. **Alerting**: Triggers alerts when rules are matched.
4. **Integration**: Sends logs/alerts to SIEM platforms like Wazuh.

---

## 🐍 What is Suricata?

Suricata is an open-source, high-performance network IDS, IPS, and network monitoring engine.

### Features:
- Deep packet inspection
- Multi-threaded architecture
- Protocol identification (HTTP, TLS, DNS, etc.)
- JSON log output for easy integration
- Community rules for threat detection

---

## 🖥️ Lab Setup

| Component            | Description                                  |
|---------------------|----------------------------------------------|
| **Wazuh Server**     | Ubuntu Server with Wazuh Manager & Dashboard |
| **Wazuh Agent**      | Ubuntu with Suricata installed               |
| **Attacker Machine** | Kali Linux (for simulating attacks)          |

---

## 📌 Task: Detecting Port Scanning using Suricata + Wazuh

---

### 🛠Step 1: Setting up Wazuh Agent with Suricata

1. **Install Wazuh agent** on Ubuntu:
    ```bash
    curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
    echo "deb https://packages.wazuh.com/4.x/apt stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
    sudo apt update && sudo apt install wazuh-agent
    ```

2. **Configure the agent**:
   - Edit: `/var/ossec/etc/ossec.conf`
   - Set `<address>wazuh-manager-ip</address>`

3. **Start agent**:
    ```bash
    sudo systemctl enable wazuh-agent
    sudo systemctl start wazuh-agent
    ```

---

### Step 2: Installing Suricata and Rules

1. **Install Suricata**:
    ```bash
    sudo apt install suricata -y
    ```

2. **Enable EVE JSON output**:
   - Edit `/etc/suricata/suricata.yaml`:
     ```yaml
     outputs:
       - eve-log:
           enabled: yes
           filetype: regular
           filename: /var/log/suricata/eve.json
     ```

3. **Update and install rules**:
    ```bash
    sudo suricata-update
    ```

4. **Start Suricata**:
    ```bash
    sudo systemctl enable suricata
    sudo systemctl start suricata
    ```

---

### Step 3: Simulate Attack using Kali Linux

On Kali Linux terminal, run a SYN scan:
```bash
nmap -sS -T4 <target-ip>
```
`-sS`: SYN scan

`-T4`: Faster scan timing

This scan should trigger Suricata detection rules for port scanning.

### Step 4: View Alerts in Wazuh Dashboard
Login to Wazuh Dashboard.

Navigate to Security Events → Choose agent.

Filter by Rule Group: Suricata

Look for alert like:

ET SCAN Nmap Synchronous Scan

##📤 Submission
Submit screenshots of:
- Suricata service running
- Alert in Wazuh Dashboard


## Learning Outcome
By completing this lab, you will:
- Understand the basics of IDS and Suricata.
- Install and configure Suricata to monitor traffic.
- Detect and respond to a port scanning attack.
- Visualize network alerts on Wazuh SIEM.
- Gain hands-on experience with EDR concepts.

