### Introduction
- **Knowledge of Operating Systems for Penetration Testing:**
    - As a penetration tester, having a deep understanding of various technologies and operating systems is essential.
    - **Windows and Linux** are the most common operating systems encountered in assessments, whether in **on-premise environments** or the **cloud**.
    - Proficiency in these systems enables a penetration tester to:
        - **Attack and exploit vulnerabilities** within the operating systems themselves or applications running on them.
        - **Defend against attacks** by understanding the mechanisms and tools available to secure these environments.
        - Use them as **platforms for launching further penetration testing activities**, such as hosting exploit tools, setting up proxy chains, or managing payloads.
    - A thorough understanding of both operating systems significantly enhances effectiveness in diverse assessment scenarios.



### The Windows Operating System
- **Introduction and Evolution of Windows Operating Systems:**
    - **Windows Desktop:**
        - Microsoft introduced the Windows operating system on **November 20, 1985** as a graphical shell for MS-DOS.
        - Early versions introduced utilities like **File Manager**, **Program Manager**, and **Print Manager**.
        - **Windows 95** marked the first full integration of Windows and DOS, introducing **built-in Internet support** and debuting **Internet Explorer**.
        - Over a dozen versions have followed, including **Windows XP, Vista, 8**, and the current **Windows 11**.
        - Editions cater to various audiences, from **casual users** to **enterprise customers*.
    - **Windows Server:**
        - **Windows NT 3.1 Advanced Server (1993)** introduced Windows Server.
        - Over time, features like **IIS**, **networking protocols**, **Administrative Wizards**, and **Active Directory (Windows 2000)** were added.
        - **Windows Server 2003** introduced **server roles**, **firewall**, and **Volume Shadow Copy Service**.
        - **Windows Server 2008** included **failover clustering**, **Hyper-V**, and improvements to Active Directory.
        - Subsequent releases, including **Server 2012, Server 2016**, and **Server 2019**, brought features like **Kubernetes support** and **Linux container integration**.
- **Deprecation and Legacy Systems:**
    - Older versions, such as **Server 2008** and **2012**, are now **end-of-life** (security updates ceased on **January 14, 2020**).
    - Microsoft occasionally issues **out-of-band patches** for critical vulnerabilities, such as **SMBv1 (EternalBlue)**.
    - **Legacy systems** persist in organizations due to critical application dependencies or budgetary constraints.
- **Implications for Assessors:**
    - Assessors must understand:
        - **Version-specific features, misconfigurations, and vulnerabilities.**
        - How legacy systems increase an organization's **attack surface**.
        - Potential exploits and remediation strategies for unsupported environments.



### Windows Versions
- The following is a list of the major Windows operating systems and associated version numbers, which is shown in the table below.
![[Screenshot_20241109_115704.png]]
- We can use the [Get-WmiObject](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-wmiobject?view=powershell-5.1) [cmdlet](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/cmdlet-overview?view=powershell-7) to find information about the operating system. 
- This cmdlet can be used to get instances of WMI classes or information about available WMI classes. 
- There are a variety of ways to find the version and build number of our system. 
- We can easily obtain this information using the `win32_OperatingSystem` class, which shows that we are on a Windows 10 host, build number 19041.
```powershell-session
PS C:\htb> Get-WmiObject -Class win32_OperatingSystem | select Version,BuildNumber

Version    BuildNumber
-------    -----------
10.0.19041 19041
```
- Some other useful classes that can be used with `Get-WmiObject` are `Win32_Process` to get a process listing, `Win32_Service` to get a listing of services, and `Win32_Bios` to get [Basic Input/Output System](https://en.wikipedia.org/wiki/BIOS) (`BIOS`) information. T
- he BIOS is firmware installed on a computer's motherboard that controls the computer's essential functions, such as power management, input/output interfaces, and system configuration. 
- We can use the `ComputerName` parameter to get information about remote computers. `Get-WmiObject` can be used to start and stop services on local and remote computers, and more. 
- Further information about the cmdlet can be found [here](https://ss64.com/ps/get-wmiobject.html) and [here](https://adamtheautomator.com/get-wmiobject/).



### Accessing Windows
- #### Local Access Concepts
    - Local access refers to physically interacting with a computer using devices such as keyboards, mice, and screens.
    - Examples of local access devices include **smartphones, tablets, laptops, desktops**, and **Raspberry Pi** devices.
    - Organizations often design **security policies** and **controls** assuming employees work on-site using company-owned computers.
    - Remote work is increasingly supported, especially for **IT**, **software development**, and **Infosec** professionals, who may access multiple machines locally and remotely on a daily basis.
- #### Remote Access Concepts
    - Remote access allows a user to interact with a computer over a **network**, requiring initial local access to set up.
    - Examples of industries heavily reliant on remote access:
        - **Managed Service Providers (MSPs)** for centralized management and automation.
        - **Managed Security Service Providers (MSSPs)** for rapid responses to security issues.
    - Many organizations' **IT, development, and security teams** rely on remote access for:
        - Building applications.
        - Managing servers.
        - Administering workstations.
    - Common remote access technologies include:
        - **Virtual Private Networks (VPN).**
        - **Secure Shell (SSH).**
        - **File Transfer Protocol (FTP).**
        - **Virtual Network Computing (VNC).**
        - **Windows Remote Management (WinRM).**
        - **Remote Desktop Protocol (RDP).**
- #### Remote Desktop Protocol (RDP)
    - **RDP Architecture:**
        - Uses a **client/server model**:
            - The client specifies a target **IP address** or **hostname**.
            - The target computer acts as the **server**.
        - **Default port:** RDP listens on **3389**.
    - **Analogy:**
        - A **network subnet** is like a street in a town.
        - An **IP address** is a specific house on the street.
        - **Logical ports** are doors/windows used to access the house.
    - **Packet Routing:**
        - A **request packet** reaches the destination IP.
        - It is routed to a specific application based on the **logical port**.
    - For a deeper understanding of **IP addressing** and **protocol encapsulation**, refer to the [Introduction to Networking](https://academy.hackthebox.com/module/details/34) module.
- **Using RDP:**
    - RDP enables connection from a Linux or Windows host to a Windows target.
    - To connect from a Windows host, use the built-in **Remote Desktop Connection** app (`mstsc.exe`).
    - For more details on its basic usage, consult Microsoft's [documentation](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/mstsc).
![[UsingRemoteDesktopConnection_gif 1.png]]
- #### Remote Access Configuration
    - For **RDP** to function, **remote access** must be explicitly [enabled](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access) on the target system.
        - By default, **Windows operating systems** disable remote access for security reasons.
    - On **HTB Academy labs**, Windows targets are preconfigured to allow RDP access once you connect via **VPN**.
- #### Convenience Features
    - **Remote Desktop Connection** supports saving **connection profiles**, which store settings and credentials for specific remote systems.
        - IT administrators frequently use this feature to streamline access to multiple systems, enhancing efficiency.
![[SavingRDPConnections_gif 1.png]]
- As pentesters, we can benefit from looking for these saved Remote Desktop Files (`.rdp`) while on an engagement.
- Many other Remote Desktop client applications exist, some of which are listed in this Microsoft article called [Remote Desktop clients](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients). 
- We will not cover every Remote Desktop client application in this module.



### Using xfreerdp
- From a Linux-based attack host we can use a tool called [xfreerdp](https://linux.die.net/man/1/xfreerdp) to remotely access Windows targets. 
- You will notice that we use xfreerdp across multiple modules because of its ease of use, feature set, command line utility, and efficiency. 
- Check out the clip below to see basic usage from Pwnbox.
![[ConnectingwithXfreerdp_gif.png]]
- Remember that we can also copy and paste in xfreerdp commands in the command line, so we do not need to enter options manually. 
- There are several options available to us with xfreerdp, such as drive redirection to be able to transfer files to/from the target host, which are worth practicing and we will cover in other modules within HTB Academy.
- Other RDP clients exist, such as [Remmina](https://remmina.org/) and [rdesktop](http://www.rdesktop.org/), and we encourage you to experiment with others and see what works best for you. 
- Now that we have covered these concepts let's apply them by spawning the target below and connecting to it using RDP with the credentials provided.



### Connecting to the Windows Target
- Connect via Remote Desktop (RDP) using the following command, which is shown below.
```shell-session
secmancer@htb[/htb]$ xfreerdp /v:<targetIp> /u:htb-student /p:Password
```

> Note: It may take 1-2 minutes for your target instance to spawn.



### Questions
- What is the Build Number of the target workstation?
	- 19041
- Which Windows NT version is installed on the workstation? (i.e. Windows X - case sensitive)
	- Windows 10