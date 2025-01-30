### **1. Graphical User Interface (GUI)**
- **Introduced in the late 1970s** to make computers more accessible.
- **Allows users to interact with OS and applications using graphical elements** (e.g., icons, windows, menus).
- **Administrators use GUI tools** for managing Active Directory, IIS, and databases.



### **2. Remote Desktop Protocol (RDP)**
- **Proprietary Microsoft protocol for remote access to Windows GUI.**
- **Uses TCP/UDP port 3389** for communication.
- **Common use cases:**
    - System administration.
    - Remote work.
    - Accessing a work computer via VPN.



### **3. Windows Command Line**
- #### **Command Prompt (CMD)**
	- **cmd.exe** is used to execute Windows commands.
	- **Basic usage:**
	    - `help` → Lists available commands.
	    - `<command> /?` → Shows command-specific help.
	    - Examples:
	        - `ipconfig /all` → Shows IP configuration.
	        - `schtasks /query` → Lists scheduled tasks.
- #### **PowerShell**
	- **More advanced command-line shell for system administration.**
	- **Built on .NET Framework, allowing deeper OS integration.**
	- **Supports scripting, automation, and custom functions.**
- #### **PowerShell Cmdlets (Verb-Noun format)**

|**Cmdlet**|**Description**|
|---|---|
|`Get-ChildItem`|Lists directory contents (alias: `ls`, `gci`).|
|`Set-Location`|Changes directory (alias: `cd`, `sl`).|
|`Get-Alias`|Lists all command aliases.|
|`Import-Module`|Loads PowerShell modules.|
|`Get-Module`|Lists loaded modules.|

- #### **PowerShell Help System**
	- `Get-Help <cmdlet>` → Shows basic help.
	- `Get-Help <cmdlet> -Online` → Opens full documentation online.
	- `Update-Help` → Downloads the latest help files.



### **4. Running PowerShell Scripts**
- **PowerShell ISE (Integrated Scripting Environment) supports script execution & debugging.**
- **Scripts can be run using:**
    - **Direct execution:** `.\script.ps1`
    - **Importing as a module:** `Import-Module .\script.ps1`
    - **Loading in memory:** `iex (New-Object Net.WebClient).DownloadString('<URL>')`



### **5. PowerShell Execution Policy**
- **Security feature that controls script execution.**
- **Policies:**
    |**Policy**|**Description**|
    |---|---|
    |**Restricted**|Blocks all scripts.|
    |**AllSigned**|Allows only signed scripts.|
    |**RemoteSigned**|Allows local scripts; requires signatures for downloaded scripts.|
    |**Unrestricted**|Allows all scripts but prompts before running downloaded ones.|
    |**Bypass**|No restrictions.|
- **View current policy:**
    ```powershell
    Get-ExecutionPolicy -List
    ```
- **Change execution policy (session only):**
    ```powershell
    Set-ExecutionPolicy Bypass -Scope Process
    ```



### **Security Considerations**
- **GUI is user-friendly but less efficient for advanced tasks.**  
- **CMD is limited; PowerShell offers better scripting and automation.**  
- **PowerShell execution policy can be bypassed, so it should not be relied on for security.**



### Questions
- What is the alias set for the ipconfig.exe command?
	- ifconfig
- Find the Execution Policy set for the LocalMachine scope.
	- unrestricted