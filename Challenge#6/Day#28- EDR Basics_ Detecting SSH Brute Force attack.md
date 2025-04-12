# **Task #28: EDR Basics: Detecting SSH Brute Force attack**

## **Objective**  
The objective of this task is to help students **detect SSH brute-force attacks** on an Ubuntu machine using **Wazuh’s security monitoring capabilities**. Students will simulate an SSH brute-force attack, analyze logs, and detect suspicious authentication attempts using Wazuh alerts.

---

## **Preparation: Configure Wazuh Agent on Ubuntu Target Machine**  

### **Requirements**  
- **Wazuh Server:** Installed and running (Refer to Task #26).  
- **Ubuntu 22.04/20.04 (Target Machine).**  
- **Wazuh Agent installed on the Ubuntu machine.**  
- **SSH enabled on the target machine.**  
- **Admin or sudo access on the target machine.**  

### **Step 1: Install Wazuh Agent on Ubuntu**  
1. Download and install the **Wazuh Agent** on the target machine:  
   ```bash
   curl -sO https://packages.wazuh.com/4.7/wazuh-agent-linux.sh && sudo bash wazuh-agent-linux.sh
   ```
2. Configure the agent to connect to the Wazuh Server:
```
sudo nano /var/ossec/etc/ossec.conf
```
- Locate <address> and set it to the Wazuh Server IP:
```
<address>WAZUH-SERVER-IP</address>
```
3. Restart the Wazuh Agent service:
```
sudo systemctl restart wazuh-agent
```

## Attack Simulation & Detection

### Step 1: Simulate an SSH Brute-Force Attack Using Hydra

1. From the attacker machine, install Hydra:

```
sudo apt update && sudo apt install hydra -y
```

2. Run the following command to simulate an SSH brute-force attack:

```
hydra -l ubuntu -P /usr/share/wordlists/rockyou.txt <target-IP> ssh
```
- Replace `<target-IP>` with the Ubuntu target machine’s IP address.
- `-l ubuntu` specifies the username to attack.
- `-P /usr/share/wordlists/rockyou.txt` uses a password list for brute-forcing SSH.
3. If a valid password is found, Hydra will display:

```
[22][ssh] host: <target-IP> login: ubuntu password: <password>
```

### Step 2: Detect SSH Brute Force Attempts in Wazuh
1. Open the Wazuh Dashboard (http://<Wazuh-Server-IP>:5601).
2. Navigate to Security Events and run below query
```
rule.id:(5551 OR 5712)
```
4. Look for logs indicating:
- Multiple failed SSH login attempts from the same IP.
- High volume of authentication failures in a short period.
- Successful logins after repeated failed attempts (possible compromise).

## Conclusion
✅ Successfully configured Wazuh Agent on an Ubuntu machine for SSH monitoring.   
✅ Simulated SSH brute-force attacks using Hydra.   
✅ Detected brute-force attempts in Wazuh logs and alerts.   
✅ Learned how SOC analysts investigate authentication attacks using SIEM tools.   

## Submission
- Share a screenshot of the Wazuh dashboard showing SSH brute-force detection alerts.
- Share a screenshot of logs confirming multiple failed SSH attempts.
- Write a short observation on how SSH brute-force detection helps in security monitoring and threat prevention.
sql
Copy
Edit
