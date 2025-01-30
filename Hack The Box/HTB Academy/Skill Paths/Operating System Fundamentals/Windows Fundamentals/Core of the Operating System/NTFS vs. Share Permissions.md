### **1. Windows Security & SMB Vulnerabilities**
- **Windows dominates the global OS market**, making it a primary target for malware.
- **Malware spreads through network shares** with **weak permissions**.
- **EternalBlue vulnerability (SMBv1)** still affects **unpatched** Windows systems.
- **SMB (Server Message Block)**: Windows protocol for **file and printer sharing** in enterprise environments.



### **2. NTFS vs. Share Permissions**

|**Permission Type**|**Applies To**|**Scope**|
|---|---|---|
|**NTFS Permissions**|Files & folders|**Always applies**, whether accessed locally or remotely.|
|**Share Permissions**|Network shares (via SMB)|**Only applies when accessing resources over the network.**|

- **NTFS permissions** apply to all file operations **locally and remotely**.
- **Share permissions** apply **only when accessed via SMB (over a network)**.
- **Both permissions apply together** when accessing a network share.



### **3. Share Permissions**

|**Permission**|**Description**|
|---|---|
|**Full Control**|Modify, delete, read, and change permissions on files and folders.|
|**Change**|Read, edit, delete, and add files and subfolders.|
|**Read**|View files and subfolders but not modify them.|



### **4. NTFS Permissions**

|**Permission**|**Description**|
|---|---|
|**Full Control**|Modify, delete, move files/folders, and change NTFS permissions.|
|**Modify**|Read, write, modify, and delete files and folders.|
|**Read & Execute**|View and execute files.|
|**List Folder Contents**|View folder structure and files.|
|**Read**|View file contents.|
|**Write**|Create files and modify existing ones.|

- #### **NTFS Special Permissions**

|**Permission**|**Description**|
|---|---|
|**Traverse Folder / Execute File**|Allows users to access subfolders even if parent permissions deny access.|
|**Delete**|Allows file and folder deletion.|
|**Take Ownership**|Allows users to take ownership of files and folders.|



### **5. Creating a Network Share (SMB)**
- #### **Steps to Create a Share (Windows GUI)**
	1. **Create a folder** (e.g., `Company Data`) on the desktop.
	2. **Right-click → Properties → Sharing tab → Advanced Sharing**.
	3. **Enable sharing**, set **permissions**, and limit the number of users.
	4. **Set NTFS permissions** (Security tab) for granular access control.
- #### **Checking Available Shares (Linux)**
```bash
smbclient -L SERVER_IP -U htb-student
```
- **Example Output:**
```txt
Sharename       Type      Comment
---------       ----      -------
ADMIN$          Disk      Remote Admin
C$              Disk      Default share
Company Data    Disk      
IPC$            IPC       Remote IPC
```
- #### **Connecting to a Share (Linux)**
```bash
smbclient '\\SERVER_IP\Company Data' -U htb-student
```
- If access is **denied**, check **Windows Defender Firewall** settings.



### **6. Windows Defender Firewall Considerations**
- **Firewall blocks external SMB connections** unless explicitly allowed.
- **Three Firewall Profiles**:
    - **Public** – Used for untrusted networks (e.g., coffee shop Wi-Fi).
    - **Private** – Used for trusted networks (e.g., home or office).
    - **Domain** – Used for corporate environments (Active Directory).
- **Instead of disabling the firewall, allow SMB connections using inbound rules**.



### **7. Mounting an SMB Share in Linux**
```bash
sudo mount -t cifs -o username=htb-student,password=Academy_WinFun! //SERVER_IP/"Company Data" /home/user/Desktop/
```
- If the command fails, install CIFS utilities:
```bash
sudo apt-get install cifs-utils
```



### **8. Monitoring SMB Shares**
- #### **View Active Shares on Windows**
```cmd
net share
```
- **Example Output:**
```txt
Share name   Resource                        Remark
-------------------------------------------------------------------------------
C$           C:\                             Default share
IPC$                                         Remote IPC
ADMIN$       C:\WINDOWS                      Remote Admin
Company Data C:\Users\htb-student\Desktop\Company Data
```
- #### **Monitor Shares via Computer Management**
	- Open **Computer Management → Shared Folders**.
	- View **Shares, Sessions, Open Files**.
- #### **Check SMB Activity in Event Viewer**
	- **Logs track file access, authentication attempts, and errors**.
	- Useful for **troubleshooting and detecting unauthorized access**.



### **Key Takeaways**
-  **NTFS permissions apply locally and remotely**; **Share permissions apply only over SMB**.
- **Firewall rules must be configured** for SMB access.  
- **Event Viewer & Computer Management** help **monitor SMB activity**.  
- **Attackers often exploit weak share permissions**, making **proper access control critical**.



### Questions
- What protocol discussed in this section is used to share resources on the network using Windows? (Format: case sensitive)
	- SMB
- What is the name of the utility that can be used to view logs made by a Windows system? (Format: 2 words, 1 space, not case sensitive)
	- Event Viewer
- What is the full directory path to the Company Data share we created?
	- C:\Users\htb-student\Desktop\Company Data