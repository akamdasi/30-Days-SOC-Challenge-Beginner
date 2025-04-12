# **Day#17: Splunk Basics: On board Linux Machine**

## **Objective**  
The objective of this task is to help students **set up Splunk Universal Forwarder on a remote Ubuntu machine** and **ingest syslog data into a central Splunk server**. By completing this task, students will learn how to forward logs from a remote system to a Splunk indexer.

---

## **Lab Setup**  
### **Requirements**  
- **Splunk Server:** Installed on a central **Ubuntu machine** (Refer to Task #18 for installation).  
- **Remote Ubuntu Machine:** The system that will send syslogs to the Splunk server.  
- **Splunk Universal Forwarder (UF):** Installed on the remote machine.  
- **Network Access:** The Splunk server must be reachable from the remote Ubuntu machine.  

---

## **Steps to Configure Universal Forwarder for Remote Syslog Ingestion**

### **Step 1: Download and Install Splunk Universal Forwarder on the Remote Machine**
1. Open **Terminal** on the remote Ubuntu machine.  
2. Download Splunk Universal Forwarder:  
   ```bash
   wget -O splunkforwarder-ubuntu.deb https://download.splunk.com/products/universalforwarder/releases/latest/linux/splunkforwarder-latest-linux-2.0-amd64.deb
   ```
3. Install the Universal Forwarder:
```
sudo dpkg -i splunkforwarder-ubuntu.deb
```
4. Move to the Splunk Forwarder directory:
```
cd /opt/splunkforwarder/bin
```
5. Accept the license and enable Splunk Universal Forwarder at boot:
```
sudo ./splunk enable boot-start --accept-license
```

### Step 2: Configure Universal Forwarder to Send Syslogs to Splunk Server
1. Open Terminal and navigate to Splunk UF:
```
cd /opt/splunkforwarder/bin
```
2. Set the Splunk indexer (Splunk Server) as the forwarding destination:
```
sudo ./splunk add forward-server <splunk-server-ip>:9997
```
- Replace <splunk-server-ip> with the IP address of the Splunk indexer.
- Port 9997 is the default forwarding port.

### Step 3: Configure Syslog Monitoring on the Remote Machine
1. Add a monitoring input for syslog:
```
sudo ./splunk add monitor /var/log/syslog -index main -sourcetype syslog
```
2. Add a monitoring input for authentication logs (optional):
```
sudo ./splunk add monitor /var/log/auth.log -index main -sourcetype authlog
```
3. Restart the Universal Forwarder:
```
sudo ./splunk restart
```

### Step 4: Enable Receiving on Splunk Indexer
1. On the Splunk Server, open Terminal and run:

```
sudo /opt/splunk/bin/splunk enable listen 9997
```
- This allows the Splunk indexer to receive forwarded logs on port 9997.
2. Verify that the Universal Forwarder is connected:

```
sudo /opt/splunk/bin/splunk list forward-server
```
- The output should show the remote Ubuntu machine actively forwarding logs.

### Step 5: Verify Log Ingestion in Splunk
1. Open Splunk Web Interface (http://<splunk-server-ip>:8000).
2. Go to Search & Reporting and run the following query:
```
index=main sourcetype=syslog | table _time host sourcetype message
```
3. If logs from the remote machine appear, syslog forwarding is successful.

## Conclusion
✅ Successfully installed Splunk Universal Forwarder on the remote Ubuntu machine.    
✅ Configured log forwarding to a central Splunk server.    
✅ Verified syslog ingestion in Splunk using the Search feature.    
✅ Learned how SOC analysts centralize logs from multiple systems for monitoring.   

## Submission
- Share a screenshot of Splunk Web showing ingested syslogs from the remote Ubuntu machine.
- Write a short observation on how centralized log collection improves security monitoring.

