# **Task #27: EDR Basics: FIM using Wazuh**

## **Objective**  
The objective of this task is to help students **detect and investigate unauthorized file changes** on a Windows machine using **Wazuh File Integrity Monitoring (FIM)**. Students will learn how to monitor **sensitive files for unauthorized modifications, simulate an attack by modifying a file, and analyze alerts in Wazuh**.

---

## **Preparation: Configure Wazuh Agent on Windows Target Machine**  

### **Requirements**  
- **Wazuh Server:** Installed and running (Refer to Task #26).  
- **Windows 10/11 or Windows Server 2019/2022 (Target Machine).**  
- **Wazuh Agent installed on Windows Machine.**  
- **Admin or PowerShell access on Windows Machine.**  

### **Step 1: Install Wazuh Agent on Windows**  
1. Download the **Wazuh Agent** from:  
   [https://packages.wazuh.com/4.x/windows/wazuh-agent-4.x.msi](https://packages.wazuh.com/4.x/windows/wazuh-agent-4.x.msi)  
2. Run the installer and enter the **Wazuh Server IP** when prompted.  
3. Start the Wazuh Agent service:  
   ```powershell
   Start-Service WazuhSvc
   ```

### Step 2: Configure File Integrity Monitoring (FIM) in Wazuh
1. Open Wazuh Manager Configuration on the Wazuh Server:
```
sudo nano /var/ossec/etc/ossec.conf
```
2. Add the following configuration under <syscheck> to monitor sensitive files on Windows:
```
<syscheck>
    <frequency>600</frequency>
    <directories check_all="yes">C:\Users\Public\Documents</directories>
</syscheck>
```
- This monitors changes in the Public Documents folder.
3. Restart Wazuh Manager to apply changes:
```
sudo systemctl restart wazuh-manager
```

## Attack Simulation & Detection

### Step 1: Simulate an Unauthorized File Change on Windows
1. Open PowerShell (Run as Administrator) on the Windows machine.
2. Create a test file in the monitored directory:
```
echo "Sensitive data" > C:\Users\Public\Documents\important.txt
```
3. Modify the file content to simulate unauthorized changes:
```
echo "Unauthorized modification detected" >> C:\Users\Public\Documents\important.txt
```
4. Delete the file to simulate data tampering:
```
Remove-Item C:\Users\Public\Documents\important.txt -Force
```

### Step 2: Detect Unauthorized File Changes in Wazuh
1. Open the Wazuh Dashboard (http://<Wazuh-Server-IP>:5601).
2. Navigate to Security Events → File Integrity Monitoring (FIM).
3. Run the following search query in Wazuh to filter FIM logs:
```
rule.group:FIM AND data.win.eventdata.targetFilename:"C:\\Users\\Public\\Documents\\important.txt"
```
4. Look for logs indicating:
- File Created
- File Modified
- File Deleted

## Conclusion
✅ Successfully configured File Integrity Monitoring (FIM) in Wazuh.    
✅ Simulated unauthorized file modifications and deletions on a Windows system.    
✅ Detected file changes in Wazuh logs and dashboard alerts.    
✅ Learned how SOC analysts investigate unauthorized file changes for threat detection.   

## Submission
- Share a screenshot of the Wazuh dashboard showing detected file changes.
- Share a screenshot of logs confirming file modifications or deletions.
- Write a short observation on how Wazuh’s File Integrity Monitoring helps in security investigations.
