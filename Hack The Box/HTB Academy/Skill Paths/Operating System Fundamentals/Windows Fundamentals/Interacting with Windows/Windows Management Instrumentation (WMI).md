### **1. Overview of WMI**
- **Windows Management Instrumentation (WMI) is a subsystem of PowerShell** for system monitoring & management.
- **Comes pre-installed in Windows since Windows 2000.**
- **Allows for centralized device and application management across corporate networks.**



### **Key Components of WMI**

| **Component**          | **Description**                                                                                             |
| ---------------------- | ----------------------------------------------------------------------------------------------------------- |
| **WMI Service**        | Background process that manages communication between WMI providers, repository, and managing applications. |
| **Managed Objects**    | Logical or physical components that can be managed by WMI.                                                  |
| **WMI Providers**      | Objects that monitor events/data related to a specific object.                                              |
| **Classes**            | Used by WMI providers to pass data to the WMI service.                                                      |
| **Methods**            | Attached to classes and allow actions (e.g., starting/stopping processes).                                  |
| **WMI Repository**     | Database storing all static WMI-related data.                                                               |
| **CIM Object Manager** | Handles requests from WMI providers and applications.                                                       |
| **WMI API**            | Allows applications to access the WMI infrastructure.                                                       |
| **WMI Consumer**       | Sends queries to objects via the CIM Object Manager.                                                        |



### **2. Use Cases of WMI**
-  **Monitoring & managing local/remote systems.**  
- **Configuring security settings on remote machines/applications.**  
- **Managing users & groups, modifying system properties.**  
- **Executing code & scheduling tasks.**  
- **Logging & auditing system events.**



### **3. Using WMI in Windows Command Prompt**
- **Interactive WMI shell:**
    ```cmd
    wmic
    ```
- **Run WMI command directly:**
    ```cmd
    wmic computersystem get name
    ```
- **View available WMIC commands:**
    ```cmd
    wmic /?
    ```
- **Get brief OS information:**
    ```cmd
    wmic os list brief
    ```
- **Example Output:**
    ```
    BuildNumber  Organization  RegisteredUser  SerialNumber             SystemDirectory      Version
    19041                      Owner           00123-00123-00123-AAOEM  C:\Windows\system32  10.0.19041
    ```



### **4. Using WMI in PowerShell**
- **PowerShell provides more flexibility via `Get-WmiObject` and `Invoke-WmiMethod`.**
- #### **Retrieve OS Information**
```powershell
Get-WmiObject -Class Win32_OperatingSystem | select SystemDirectory,BuildNumber,SerialNumber,Version | ft
```
- **Example Output:**
```
SystemDirectory     BuildNumber SerialNumber            Version
---------------     ----------- ------------            -------
C:\Windows\system32 19041       00123-00123-00123-AAOEM 10.0.19041
```
- #### **Rename a File using WMI**
```powershell
Invoke-WmiMethod -Path "CIM_DataFile.Name='C:\users\public\spns.csv'" -Name Rename -ArgumentList "C:\Users\Public\kerberoasted_users.csv"
```
- **Example Output:**
```
ReturnValue      : 0
```
- (Where `ReturnValue = 0` indicates success.)



### **5. WMI for Blue Team & Red Team**
- **For Blue Team (Defensive Security):**
	- **Monitor system performance & security logs.**
	- **Configure & enforce security policies remotely.**
	- **Automate system administration tasks.**
- **For Red Team (Offensive Security & Penetration Testing):**
	- **Enumerate system information & users.**
	- **Execute commands & schedule tasks remotely.**
	- **Leverage WMI for lateral movement & persistence.**



### **Summary**
- **WMI is a powerful tool for system management, automation, and remote administration.**
- **PowerShell provides deeper integration & control over WMI.**  
- **WMI is widely used by both system administrators & attackers (for lateral movement and persistence).**



### Questions
- Use WMI to find the serial number of the system.
	- 00329-10280-00000-AA938