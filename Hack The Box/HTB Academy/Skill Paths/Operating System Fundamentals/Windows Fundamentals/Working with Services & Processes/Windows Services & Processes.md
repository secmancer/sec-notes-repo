### **### **1. Windows Services**
- **Background processes** that run without user interaction.
- **Can start automatically on boot** and run even after user logout.
- **Managed by the Service Control Manager (SCM)**.
- **Accessed via:**
    - **GUI:** `services.msc`
    - **Command Line:** `sc.exe` or PowerShell `Get-Service`



### **Listing Running Services (PowerShell)**
```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
```



### **Example Output**
```powershell
Name                : AdobeARMservice
DisplayName         : Adobe Acrobat Update Service
Status              : Running
CanStop             : True
ServiceType         : Win32OwnProcess
```



### **Service Startup Types**

| **Startup Type**              | **Behavior**             |
| ----------------------------- | ------------------------ |
| **Automatic**                 | Starts at system boot.   |
| **Automatic (Delayed Start)** | Starts after boot delay. |
| **Manual**                    | Starts only when needed. |
| **Disabled**                  | Cannot be started.       |



### **2. Critical Windows Services**

|**Service**|**Description**|
|---|---|
|`smss.exe`|Manages Windows sessions.|
|`csrss.exe`|Handles Windows UI and shutdowns.|
|`wininit.exe`|Handles system initialization after boot.|
|`logonui.exe`|Manages the login screen.|
|`lsass.exe`|Handles authentication and security policies.|
|`services.exe`|Manages service startup and shutdown.|
|`winlogon.exe`|Handles user login and screen locking.|
|`System`|Manages Windows kernel processes.|
|`svchost.exe`|Runs multiple system services using DLLs.|



### **3. Processes in Windows**
- **Can be system-initiated or user-initiated.**
- **Critical processes cannot be terminated** without causing system instability.
- **Common system processes:**
    - `winlogon.exe` – Manages user logins.
    - `lsass.exe` – Handles user authentication.
    - `svchost.exe` – Runs Windows services from DLLs.



### **Viewing Running Processes (PowerShell)**

```powershell
Get-Process | Select-Object -First 5
```



### **4. Local Security Authority Subsystem Service (`lsass.exe`)**
- **Handles Windows authentication** (logins, password changes).
- **Stores credentials in memory** → Target for credential dumping attacks.
- **Logged authentication events in:**
    ```cmd
    eventvwr.msc → Windows Logs → Security
    ```



### **5. Sysinternals Suite (Advanced Windows Tools)**
- **Microsoft SysInternals tools help analyze Windows internals.**
- Can be accessed **without installation** via:
    ```cmd
    \\live.sysinternals.com\tools
    ```



### **Example: Running ProcDump Remotely**
```cmd
\\live.sysinternals.com\tools\procdump.exe -accepteula
```



### **Useful Sysinternals Tools**

|**Tool**|**Function**|
|---|---|
|**Process Explorer**|Advanced Task Manager, shows running processes, handles, and DLLs.|
|**Process Monitor**|Tracks file system, registry, and network activity.|
|**TCPView**|Monitors network connections.|
|**PSExec**|Remotely execute processes via SMB.|



### **6. Windows Task Manager**
- **Opened via:**
    - `Ctrl + Shift + Esc`
    - `Ctrl + Alt + Del → Task Manager`
    - `taskmgr` command



### **Task Manager Tabs & Functions**

|**Tab**|**Description**|
|---|---|
|**Processes**|Lists running applications and background processes.|
|**Performance**|CPU, memory, disk, and network usage graphs.|
|**App History**|Shows app resource usage over time.|
|**Startup**|Manages programs that start on boot.|
|**Users**|Displays active users and their resource consumption.|
|**Details**|Displays process details (PID, status, CPU usage).|
|**Services**|Shows system services (can start/stop services).|



### **7. Process Explorer (Sysinternals)**
- **Shows process parent-child relationships.**
- **Monitors DLLs and handles associated with processes.**
- **Used for detecting malware and rogue processes.**



### **Key Takeaways**
- **Windows services run in the background** and can start on boot.  
- **Critical processes like `lsass.exe` store credentials in memory** (high-value target).  
- **Sysinternals tools provide deep insight into Windows system activity.**  
- **Task Manager & Process Explorer help manage and analyze processes.**



### Questions
- Identify one of the non-standard update services running on the host. Submit the full name of the service executable (not the DisplayName) as your answer.
	- FoxItReaderUpdateService.exe