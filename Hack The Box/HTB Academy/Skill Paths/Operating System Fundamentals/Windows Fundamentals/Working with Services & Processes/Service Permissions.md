### **1. Importance of Windows Service Permissions**
- **Windows services run critical background processes** and can be misconfigured, leading to **security vulnerabilities**.
- **Attackers exploit service misconfigurations** to:
    - **Load malicious DLLs.**
    - **Execute applications without admin access.**
    - **Escalate privileges.**
    - **Maintain persistence (backdoors).**



### **Real-World Example of Misconfiguration**
- If a service is installed using **a regular user’s credentials** instead of a dedicated service account, disabling that user’s account could **break the service**.
- **Best practice:** Use **dedicated service accounts** for critical services.



### **2. Examining Services Using `services.msc`**
- **Opens Windows Service Manager GUI.**
- **Key fields to check:**
    - **Service Name** – Useful for command-line management.
    - **Path to Executable** – Shows where the service runs from (**vulnerable if directory permissions are weak**).
    - **Log On As** – Shows which account the service runs under (**LocalSystem, LocalService, NetworkService**).
    - **Recovery Options** – Can configure to run a program after a failure (**potential attack vector**).



### **3. Managing Services via Command Line**
- #### **Query Service Configuration (`sc qc`)**
```cmd
sc qc wuauserv
```
- **Example Output:**
```txt
SERVICE_NAME: wuauserv
        START_TYPE         : 3   DEMAND_START
        BINARY_PATH_NAME   : C:\WINDOWS\system32\svchost.exe -k netsvcs -p
        SERVICE_START_NAME : LocalSystem
```
- **Binary Path Name** – If **directory permissions are weak**, an attacker can replace the executable.
- **Start Type:**
    - `2` – **Automatic**
    - `3` – **Manual (on demand)**
    - `4` – **Disabled**
- #### **Query a Service on a Remote Machine**
```cmd
sc \\TARGET_IP query ServiceName
```
- #### **Start and Stop a Service**
```cmd
sc start wuauserv
sc stop wuauserv
```
- **Requires admin privileges** → Running without admin rights returns **Access Denied**.



### **4. Modifying Service Executables (Potential Attack)**
```cmd
sc config wuauserv binPath=C:\Windows\Malicious.exe
```
- **Replaces Windows Update service binary path with a malicious program**.
- **Common technique in privilege escalation attacks.**
- #### **Verify Change**
```cmd
sc qc wuauserv
```



### **5. Examining Service Permissions**
- #### **Using `sc sdshow` (Service Security Descriptor)**
```cmd
sc sdshow wuauserv
```
- **Example Output (SDDL Format):**
```txt
D:(A;;CCLCSWRPLORC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;SY)
```
- **D:** Discretionary Access Control List (DACL).
- **AU (Authenticated Users)** – Assigned permissions:
    - `CC` – Query service configuration.
    - `LC` – Query service status.
    - `RP` – Start service.
- **BA (Built-in Administrators)** – Full control.
- **SY (System)** – Full control.
- #### **Interpreting SDDL Entries**

|**Code**|**Permission Description**|
|---|---|
|`CC`|Query service configuration|
|`LC`|Query service status|
|`RP`|Start the service|
|`RC`|Read control|
|`BA`|Built-in Administrators|
|`AU`|Authenticated Users|
|`SY`|System|



### **6. Using PowerShell to View Service Permissions**
```powershell
Get-ACL -Path HKLM:\System\CurrentControlSet\Services\wuauserv | Format-List
```
- **Example Output:**
```txt
Owner  : NT AUTHORITY\SYSTEM
Group  : NT AUTHORITY\SYSTEM
Access : BUILTIN\Users Allow  ReadKey
         BUILTIN\Administrators Allow  FullControl
         NT AUTHORITY\SYSTEM Allow  FullControl
Sddl   : O:SYG:SYD:AI(A;ID;KR;;;BU)(A;ID;KA;;;BA)
```
- **Displays service owner and permission settings** in a structured format.
- **Shows SDDL output** similar to `sc sdshow` but with user-friendly formatting.



### **Key Takeaways**
- **Service misconfigurations can lead to privilege escalation.**  
- **Always use dedicated service accounts for critical services.**  
- **Weak directory permissions can allow attackers to replace executables.**  
- **Use `sc sdshow` and PowerShell to audit service permissions.**  
- **Best practice: Apply **least privilege principle** to services.**