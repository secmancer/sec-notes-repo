**Importance of Knowledge**
- Understanding both Windows and Linux operating systems is crucial for penetration testers.
- Most systems encountered during assessments, whether on-premise or in the cloud, are based on these two operating systems.
- It’s essential to know how to attack and defend these systems and utilize them for further penetration testing activities.

### The Windows Operating System

**History and Evolution**
- **Initial Release**: November 20, 1985, as a graphical shell for MS-DOS.
- **Early Versions**: Introduced Windows File Manager, Program Manager, and Print Manager.
- **Windows 95**: Integrated Windows with DOS and introduced Internet Explorer.
- **Subsequent Releases**: Windows XP, Vista, 7, 8, 8.1, and 10. The latest is Windows 11.
- **Windows Server**: First released in 1993 with Windows NT 3.1 Advanced Server. Introduced Active Directory with Windows 2000 and various features in subsequent versions, including Server 2003, 2008, 2012, 2016, and 2019.

**Windows Version Lifecycle**
- Older versions become deprecated and no longer receive updates.
- **End of Life**: Windows Server 2008 and 2012 as of January 14, 2020. Only Server 2012 R2 and later are currently supported.
- **Legacy Systems**: Organizations may still run older, unsupported versions for critical applications.


**Version Numbers**
- Windows NT 4: 4.0
- Windows 2000: 5.0
- Windows XP: 5.1
- Windows Server 2003/R2: 5.2
- Windows Vista/Server 2008: 6.0
- Windows 7/Server 2008 R2: 6.1
- Windows 8/Server 2012: 6.2
- Windows 8.1/Server 2012 R2: 6.3
- Windows 10/Server 2016/2019: 10.0

![[Screenshot_20240912_151126.png]]


**Getting System Information with PowerShell**
- **Command**: `Get-WmiObject -Class win32_OperatingSystem | select Version,BuildNumber`
    - Example Output:
        - Version: 10.0.19041
        - BuildNumber: 19041

**Useful WMI Classes**
- **Win32_Process**: Lists processes.
- **Win32_Service**: Lists services.
- **Win32_Bios**: Provides BIOS information.

**Accessing Windows**
- **Local Access**: Using a keyboard, mouse, or other input devices directly connected to the computer.
- **Remote Access**: Accessing a computer over a network.

**Remote Access Technologies**
- **VPN**: Virtual Private Network.
- **SSH**: Secure Shell.
- **FTP**: File Transfer Protocol.
- **VNC**: Virtual Network Computing.
- **WinRM**: Windows Remote Management (PowerShell Remoting).
- **RDP**: Remote Desktop Protocol.


### Remote Desktop Protocol (RDP)
**Overview**
- **Architecture**: Client/server model. Client specifies target IP or hostname.
- **Default Port**: 3389.
- **Usage**: Connect to a Windows target from both Windows and Linux hosts.

**Connecting Using RDP**
- **Windows Client**: Use Remote Desktop Connection (`mstsc.exe`).
    - Allows saving connection profiles for convenience.

**Using xfreerdp**
- **Command**: `xfreerdp /v:<targetIp> /u:htb-student /p:Password`
- **Features**: Drive redirection, file transfer, command-line options.
- **Other Clients**: Remmina, rdesktop. Experiment with different clients to find the best fit.

**Example Command**
- **Connect to Windows Target**:
```
xfreerdp /v:<targetIp> /u:htb-student /p:Password
```
- Note: Target instance may take 1-2 minutes to spawn.

### Questions
- What is the Build Number of the target workstation?
	- 19041
- Which Windows NT version is installed on the workstation? (i.e. Windows X - case sensitive)
	- Windows 10