# **Day#26- Setting up Wazuh**

## **Objective**  
The objective of this task is to help students **set up a Wazuh Server using the Quick Start method** and **onboard an Ubuntu machine as an agent**. By completing this task, students will learn how to deploy **Wazuh for security monitoring, log analysis, and threat detection**.

---

## 🧠 **Introduction to EDR (Endpoint Detection and Response)**

**EDR** refers to tools that monitor, record, and analyze activities on endpoints (servers, desktops, laptops) to detect malicious behavior, help in incident response, and enable threat hunting.

---

## 🔎 **How Does a SOC Analyst Use EDR?**

SOC Analysts rely on EDR tools to:
- Detect suspicious behaviors (e.g., process injection, lateral movement)
- Investigate alerts and correlate activity over time
- Isolate or respond to infected endpoints
- Pull forensic artifacts like logs, memory dumps, and timelines
- Hunt for threat indicators (IOCs)

---

## 🏆 **Popular EDR Platforms**

| Platform           | Description                                              |
|--------------------|----------------------------------------------------------|
| **Wazuh**           | Open-source SIEM + EDR, host-based log monitoring, FIM   |
| **Microsoft Defender for Endpoint** | Native EDR for Windows with behavioral analytics   |
| **CrowdStrike Falcon**   | Cloud-based EDR with threat hunting capabilities     |
| **SentinelOne**     | Autonomous endpoint protection and rollback features     |
| **Elastic Endpoint (with ELK)** | Lightweight endpoint monitoring integrated into Elastic SIEM |

---

## **Lab Task: Setting up Wazuh EDR**  

### **Requirements**  
- **System 1:** Ubuntu 22.04/20.04 (Wazuh Server)  
- **System 2:** Ubuntu 22.04/20.04 (Agent Machine to be monitored)  
- **Minimum Hardware for Wazuh Server:**  
  - **CPU:** 4 vCPUs  
  - **RAM:** 8GB+  
  - **Storage:** 50GB+  
- **Network Connectivity:** Ensure both systems can communicate over the network.  
- **User Permissions:** Root or sudo privileges on both machines.  

---

### **Step 1: Install Wazuh Server Using Quick Start**
1. Download and run the Wazuh installation assistant.
```
curl -sO https://packages.wazuh.com/4.10/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```
Once the assistant finishes the installation, the output shows the access credentials and a message that confirms that the installation was successful.

```
INFO: --- Summary ---
INFO: You can access the web interface https://<WAZUH_DASHBOARD_IP_ADDRESS>
    User: admin
    Password: <ADMIN_PASSWORD>
INFO: Installation finished.
```
- You now have installed and configured Wazuh.

2. Access the Wazuh web interface with https://<WAZUH_DASHBOARD_IP_ADDRESS> and your credentials:

- Username: admin
- Password: <ADMIN_PASSWORD>

### Step 2: Onboard an Ubuntu Machine as a Wazuh Agent
1. Install the Wazuh Agent on the Ubuntu machine to be monitored:

```
curl -sO https://packages.wazuh.com/4.7/wazuh-agent-linux.sh && sudo bash wazuh-agent-linux.sh
```
2. Configure the Wazuh Agent to connect to the Wazuh Server:

```
sudo nano /var/ossec/etc/ossec.conf
```
Locate <address> and set it to the Wazuh Server IP:
```
<address>WAZUH-SERVER-IP</address>
```
3. Start the Wazuh Agent service:

```
sudo systemctl start wazuh-agent
```
4. Enable the agent to start at boot:

```
sudo systemctl enable wazuh-agent
```

### Step 3: Verify Agent Connection in Wazuh Dashboard
1. Open Wazuh Dashboard (http://<Wazuh-Server-IP>:5601).
2. Navigate to "Agents" in the Wazuh UI.
3. Check if the Ubuntu agent is listed as "Active".

## Submission
- Share a screenshot of the Wazuh dashboard showing the active agent.
- Share a screenshot of the Wazuh logs confirming successful agent onboarding.
- Write a short observation on how Wazuh helps in security monitoring.

## Conclusion
✅ Successfully installed Wazuh Server using the Quick Start method.    
✅ Deployed Wazuh Agent on an Ubuntu machine for monitoring.   
✅ Verified agent connection in the Wazuh Dashboard.    
✅ Learned how SOC analysts use Wazuh for security monitoring and log analysis.    


