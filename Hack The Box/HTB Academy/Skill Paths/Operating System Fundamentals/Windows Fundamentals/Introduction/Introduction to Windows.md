### **1. Importance of Windows in Penetration Testing**
- **Windows & Linux** are the most common operating systems encountered in assessments.
- **Understanding Windows** is essential for:
    - Identifying **vulnerabilities** and misconfigurations.
    - Using Windows **as a platform** for further testing activities.



### **2. Windows Operating System History**
- **First Windows OS:** Released on **November 20, 1985** (GUI shell for MS-DOS).
- **Windows 95:** First full integration of Windows and DOS, introducing **Internet Explorer**.
- **Windows XP, Vista, 7, 8, 10, and 11** – Evolution of desktop Windows versions.
- **Windows Server:**
    - **1993 (Windows NT 3.1 Advanced Server)** – Introduced early networking capabilities.
    - **Windows 2000 Server** – Introduced **Active Directory**.
    - **Windows Server 2008+** – Added security enhancements, **Hyper-V, failover clustering**.
    - **Windows Server 2019+** – Modern cloud and container support (**Kubernetes, Linux containers**).
- #### **End-of-Life Windows Versions**
	- **Windows Server 2008 & 2012** → No security updates after **January 14, 2020**.
	- **Microsoft provides out-of-band patches** for legacy Windows versions due to critical vulnerabilities (**e.g., SMBv1 EternalBlue**).



### **3. Identifying Windows Versions**
- **Get-WmiObject Cmdlet** – Retrieve Windows version and build number:    
    ```powershell
    Get-WmiObject -Class win32_OperatingSystem | select Version,BuildNumber
    ```
- **Example Output:**
    ```powershell
    Version    BuildNumber
    -------    -----------
    10.0.19041 19041
    ```
- Other useful WMI classes:
    - `Win32_Process` → Lists processes.
    - `Win32_Service` → Lists services.
    - `Win32_Bios` → Retrieves BIOS information.



### **4. Windows Access Methods**
- #### **Local Access**
	- Direct interaction with **laptops, desktops, servers**.
	- Involves **physical input (keyboard, mouse)** and **output (display, console logs)**.
- #### **Remote Access**
	- Accessing a system **over a network** (local or internet).
	- Common **remote access protocols/tools**:
	    - **VPN (Virtual Private Network)**
	    - **SSH (Secure Shell)**
	    - **FTP (File Transfer Protocol)**
	    - **VNC (Virtual Network Computing)**
	    - **WinRM (Windows Remote Management/PowerShell Remoting)**
	    - **RDP (Remote Desktop Protocol)** – **Focus of this module**



### **5. Remote Desktop Protocol (RDP)**
- **Default Port:** `3389`
- **Client-Server Model:**
    - **Client:** Initiates connection (e.g., Remote Desktop Connection `mstsc.exe`).
    - **Server:** Target Windows machine with **RDP enabled**.
- #### **Networking Concepts**
	- **IP Address** – Identifies a device on the network.
	- **Logical Port** – Identifies a service on a device.
	- **Packet Encapsulation** – Network data flows through IP and port-based routing.
- #### **RDP Clients**

| **Client**    | **Platform**                           |
| ------------- | -------------------------------------- |
| **mstsc.exe** | Windows built-in Remote Desktop client |
| **xfreerdp**  | Linux CLI-based RDP client             |
| **Remmina**   | GUI-based RDP client for Linux         |
| **rdesktop**  | Alternative Linux RDP client           |



### **6. Connecting to Windows via RDP**
- #### **Using `mstsc.exe` (Windows)**
```powershell
mstsc /v:<targetIp>
```
- #### **Using `xfreerdp` (Linux)**
```bash
xfreerdp /v:<targetIp> /u:htb-student /p:Password
```
- **Drive Redirection:** Allows file transfer between local and remote hosts.
- **Clipboard Sharing:** Enables copy-paste between systems.



### **Key Takeaways**
-  **Windows knowledge is critical** for penetration testing.  
- **Windows Server versions** have evolving security features.  
- **Remote access techniques** (RDP, SSH, VPN) are essential for testing.  
- **RDP uses port 3389**, and multiple **RDP clients exist** for Windows/Linux.



### Questions
- What is the Build Number of the target workstation?
	- 19041
- Which Windows NT version is installed on the workstation? (i.e. Windows X - case sensitive)
	- Windows 10