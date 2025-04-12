# PowerShell for Security Analysts

---

## 1. **Introduction to PowerShell**
PowerShell is a powerful command-line shell and scripting language developed by Microsoft, designed specifically for system administration. It is built on the .NET framework and is widely used for automating tasks, managing configurations, and performing administrative tasks on both Windows and Linux systems.

### Why Should Security Analysts Learn PowerShell?
- **Automation and Efficiency**: Automate repetitive tasks such as log analysis, system audits, and security monitoring.
- **Incident Response**: Quickly collect forensic artifacts, investigate suspicious activities, and respond to incidents.
- **Threat Hunting**: Identify anomalous behaviors by querying system information and event logs.
- **Red Teaming and Blue Teaming**: Used by attackers for persistence and lateral movement, making it crucial for defenders to understand its capabilities.

---

## 2. **Overview of Cmdlets, Scripts, and the PowerShell Environment**

### 2.1 **Cmdlets**
- Cmdlets (pronounced "command-lets") are the building blocks of PowerShell. They are lightweight commands that perform specific operations.
- **Syntax**: `Verb-Noun` (e.g., `Get-Process`, `Set-Item`, `New-User`)
- **Example**:
    ```powershell
    Get-Process          # Lists all running processes
    Get-Service          # Displays all services on the system
    Get-EventLog -LogName Security  # Retrieves security event logs
    ```

### 2.2 **Scripts**
- Scripts are text files containing a series of PowerShell commands saved with the `.ps1` extension.
- They allow automation of complex tasks by executing multiple cmdlets in sequence.
- **Example Script (`Get-SystemInfo.ps1`)**:
    ```powershell
    # Get System Information
    Get-ComputerInfo
    Get-Process | Where-Object {$_.CPU -gt 100}  # High CPU usage processes
    Get-EventLog -LogName Security -Newest 10
    ```

### 2.3 **The PowerShell Environment**
- **Console and ISE**: PowerShell can be executed from the traditional console or the Integrated Scripting Environment (ISE).
- **Modules**: Packages containing cmdlets, functions, variables, and other resources.
- **Pipeline (`|`)**: Used to pass output from one cmdlet as input to another.
    ```powershell
    Get-Process | Where-Object {$_.CPU -gt 50} | Select-Object ProcessName, CPU
    ```

---

## 3. **Understanding the Execution Policy**
Execution Policy in PowerShell determines the conditions under which PowerShell loads configuration files and runs scripts.

### Types of Execution Policies
1. **Restricted**: Default setting, allows no scripts to run.
2. **AllSigned**: Only scripts signed by a trusted publisher can be run.
3. **RemoteSigned**: Local scripts can run, but scripts downloaded from the internet must be signed.
4. **Unrestricted**: Scripts are allowed to run without restrictions.
5. **Bypass**: No restrictions; used for automation.

### Checking and Setting Execution Policy
```powershell
Get-ExecutionPolicy        # Check current execution policy
Set-ExecutionPolicy RemoteSigned   # Set to RemoteSigned
```

###Best Practice for Security Analysts
- Always set the policy to RemoteSigned or AllSigned to prevent unauthorized scripts from running.
- Use Bypass only in controlled environments, such as for incident response scripts.

## 4. Use Cases for Security Analysts
### 4.1 Incident Response
- Collect logs and system artifacts for forensic analysis.
```powershell
Get-EventLog -LogName Security -Newest 100 | Export-Csv C:\Logs\SecurityLogs.csv
```

### 4.2 Threat Hunting
- Identify suspicious processes or unusual network activity.
```powershell
Get-Process | Where-Object { $_.CPU -gt 80 }
Get-NetTCPConnection | Where-Object { $_.RemotePort -eq 4444 }
```

### 4.3 Vulnerability Assessment
- Check for missing security patches.
```powershell
Get-HotFix | Where-Object { $_.InstalledOn -lt (Get-Date).AddMonths(-6) }
```

### 4.4 Security Audits and Compliance
- Audit user accounts and permissions.
```powershell
Get-LocalUser
Get-LocalGroupMember -Group "Administrators"
```

### 4.5 Automation and Scripting
- Automate repetitive security tasks like log cleanup or system health checks.
```powershell
Get-EventLog -LogName Application -EntryType Error -Newest 50 | Out-File C:\Logs\ErrorLogs.txt
```
## 5. PowerShell Basics
### 5.1 Basic Commands
```powershell
Get-Help Get-Process   # Display help for a cmdlet
Get-Command            # List all available cmdlets
Get-Module             # List all imported modules
```

### 5.2 Variables and Data Types
```powershell
$Name = "Security Analyst"
$Number = 42
$Array = @(1, 2, 3, 4)
```

### 5.3 Loops and Conditionals
```powershell
# If-Else Statement
$CPUUsage = Get-Process | Where-Object { $_.CPU -gt 80 }
If ($CPUUsage) {
    Write-Host "High CPU Usage Detected"
} Else {
    Write-Host "CPU Usage is Normal"
}

# ForEach Loop
$Processes = Get-Process
ForEach ($Process in $Processes) {
    Write-Host $Process.ProcessName
}
```

### 5.4 Functions
```powershell
Function Get-HighCPU {
    Param($Threshold = 50)
    Get-Process | Where-Object { $_.CPU -gt $Threshold }
}
Get-HighCPU -Threshold 80
```

## 6. PowerShell Command Cheatsheet for Security Analysts
### 6.1 System Information
```powershell
Get-ComputerInfo                    # System Information
Get-WmiObject Win32_OperatingSystem  # Detailed OS Information
```

### 6.2 Process and Service Monitoring
```powershell
Get-Process                         # List Running Processes
Get-Service                         # List Installed Services
Stop-Process -Name "notepad"         # Stop a 
```
### 6.3 Network Information
```powershell
Get-NetAdapter                      # Network Adapter Information
Get-NetTCPConnection                 # Active Network Connections
```

### 6.4 Event Log Analysis
```powershell
Get-EventLog -LogName Security -Newest 100
Get-WinEvent -LogName Application -MaxEvents 50
```

### 6.5 File and Directory Management
```powershell
Get-ChildItem -Path C:\Logs -Recurse  # List all files in a directory
Remove-Item -Path C:\Logs\*.log       # Delete all log files
```

### 6.6 User and Permissions Auditing
```powershell
Get-LocalUser                        # List all Local Users
Get-LocalGroup                       # List all Local Groups
Get-LocalGroupMember -Group "Admins"  # List Admin Group Members
```

## 7. Summary
- PowerShell is a versatile and powerful tool for Security Analysts.
- Use cmdlets to perform system audits, incident response, and threat hunting.
- Leverage scripts for automation of repetitive security tasks.
- Set execution policies securely (preferably RemoteSigned).
- Always review and understand scripts before execution to prevent malicious activities.
- Continuously learn and update your PowerShell skills to stay ahead of attackers.

