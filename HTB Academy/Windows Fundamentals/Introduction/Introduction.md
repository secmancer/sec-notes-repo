### Windows Operating System Overview
1. **History and Evolution:**
    - **Windows 1.0:** Released on November 20, 1985, as a graphical shell for MS-DOS.
    - **Windows 95:** Integrated Windows and DOS with built-in Internet support and introduced Internet Explorer.
    - **Windows XP, Vista, 7, 8, 10, 11:** Each version introduced new features and improvements, with Windows 11 being the latest as of now.
    - **Windows Server:** Released in 1993 with Windows NT 3.1 Advanced Server and evolved through versions like Server 2003, 2008, 2012, 2016, and 2019, adding features like Active Directory, Hyper-V, and advanced security options.

1. **Version Support:**
    - Older versions such as Server 2008 and 2012 are deprecated and may not receive updates unless under special support contracts.
    - Windows Server 2012 R2 and later are currently supported.

1. **Useful PowerShell Cmdlets:**
    - `Get-WmiObject -Class win32_OperatingSystem`: Retrieves information about the OS version and build number.
    - `Win32_Process`: Provides a listing of processes.
    - `Win32_Service`: Provides a listing of services.
    - `Win32_Bios`: Provides BIOS information.

1. **Command Example:**
	- Get-WmiObject -Class win32_OperatingSystem | select Version,BuildNumber
	- This command provides details about the Windows version and build number.

### Remote Access Concepts
1. **Local vs. Remote Access:**
    - **Local Access:** Involves interacting with a computer directly (keyboard, mouse, screen).
    - **Remote Access:** Allows interaction with a computer over a network, often used for management and administration.

1. **Common Remote Access Methods:**
    - **VPN:** Secure connection over the internet.
    - **SSH:** Secure Shell, commonly used for Unix-based systems.
    - **FTP:** File Transfer Protocol for file transfers.
    - **VNC:** Virtual Network Computing for remote desktop access.
    - **WinRM:** Windows Remote Management for remote administration.
    - **RDP:** Remote Desktop Protocol for remote graphical user interface access.

### Remote Desktop Protocol (RDP)
1. **Overview:**
    - RDP uses a client/server model where the client connects to a server over port 3389.
    - Allows graphical remote access to Windows systems.

1. **Using RDP:**
    - **Windows Host:** Use the Remote Desktop Connection (mstsc.exe) application.
    - **Linux Host:** Use `xfreerdp`, a command-line tool, for connecting to Windows targets.

1. **Connecting with `xfreerdp`:**
	- Basic Command:
		- xfreerdp /v:targetIp /u:htb-student /p:Password
	- Options include drive redirection for file transfers.

1. **Additional Tools:**
	- **Remmina** and **rdesktop** are alternative RDP clients on Linux.

### Questions:
- What is the Build Number of the target workstation?
	- 19041

- Which Windows NT version is installed on the workstation? (i.e. Windows X - case sensitive)
	- Windows 10