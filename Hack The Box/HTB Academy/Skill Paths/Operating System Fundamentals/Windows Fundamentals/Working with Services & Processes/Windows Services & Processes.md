### Windows Services
- **Role of Services in Windows**: Services are critical for managing long-running processes, starting automatically at system boot, and running in the background even after user logout. 
- They handle key functions like networking, diagnostics, credential management, and Windows updates.
- **Custom Application Services**: Applications can be installed as services to provide continuous functionality, such as network monitoring on servers.
- **Management via Service Control Manager (SCM)**: The `services.msc` MMC add-in offers a GUI to manage services, showing details like Name, Description, Status, Startup Type, and associated user accounts.
- **Command-Line Management**: Services can also be managed using the command-line tool `sc.exe` or PowerShell cmdlets like `Get-Service`.
```powershell-session
PS C:\htb> Get-Service | ? {$_.Status -eq "Running"} | select -First 2 |fl


Name                : AdobeARMservice
DisplayName         : Adobe Acrobat Update Service
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32OwnProcess

Name                : Appinfo
DisplayName         : Application Information
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {RpcSs, ProfSvc}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32OwnProcess, Win32ShareProcess
```
- **Service States and Startup Types**: Services can be in states such as Running, Stopped, Paused, Starting, or Stopping. They can start manually, automatically, or with a delayed automatic startup at system boot.
- **Service Categories**: Windows categorizes services into Local Services, Network Services, and System Services.
- **Administrative Control**: Creating, modifying, and deleting services generally requires administrative privileges. Misconfigured service permissions are a common avenue for privilege escalation.
- **Critical System Services**: Certain critical services cannot be stopped or restarted without a system reboot. Updating files or resources used by these services requires restarting the system.
![[Screenshot_20241109_112520.png]]
- This [link](https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_components#Services) has a list of Windows components, including key services.



### Processes
- Processes run in the background on Windows systems. 
- They either run automatically as part of the Windows operating system or are started by other installed applications.
- Processes associated with installed applications can often be terminated without causing a severe impact on the operating system. 
- Certain processes are critical and, if terminated, will stop certain components of the operating system from running properly. 
- Some examples include the Windows Logon Application, System, System Idle Process, Windows Start-Up Application, Client Server Runtime, Windows Session Manager, Service Host, and Local Security Authority Subsystem Service (LSASS) process.



### Local Security Authority Subsystem Service (LSASS)
- `lsass.exe` is the process that is responsible for enforcing the security policy on Windows systems. 
- When a user attempts to log on to the system, this process verifies their log on attempt and creates access tokens based on the user's permission levels. LSASS is also responsible for user account password changes. 
- All events associated with this process (logon/logoff attempts, etc.) are logged within the Windows Security Log. LSASS is an extremely high-value target as several tools exist to extract both cleartext and hashed credentials stored in memory by this process.



### Sysinternals Tools
- The [SysInternals Tools suite](https://docs.microsoft.com/en-us/sysinternals) is a set of portable Windows applications that can be used to administer Windows systems (for the most part without requiring installation). 
- The tools can be either downloaded from the Microsoft website or by loading them directly from an internet-accessible file share by typing `\\live.sysinternals.com\tools` into a Windows Explorer window.
- For example, we can run procdump.exe directly from this share without downloading it directly to disk.
```cmd-session
C:\htb> \\live.sysinternals.com\tools\procdump.exe -accepteula

ProcDump v9.0 - Sysinternals process dump utility
Copyright (C) 2009-2017 Mark Russinovich and Andrew Richards
Sysinternals - www.sysinternals.com

Monitors a process and writes a dump file when the process exceeds the
specified criteria or has an exception.

Capture Usage:
   procdump.exe [-mm] [-ma] [-mp] [-mc Mask] [-md Callback_DLL] [-mk]
                [-n Count]
                [-s Seconds]
                [-c|-cl CPU_Usage [-u]]
                [-m|-ml Commit_Usage]
                [-p|-pl Counter_Threshold]
                [-h]
                [-e [1 [-g] [-b]]]
                [-l]
                [-t]
                [-f  Include_Filter, ...]
                [-fx Exclude_Filter, ...]
                [-o]
                [-r [1..5] [-a]]
                [-wer]
                [-64]
                {
                 {{[-w] Process_Name | Service_Name | PID} [Dump_File | Dump_Folder]}
                |
                 {-x Dump_Folder Image_File [Argument, ...]}
                }
				
<SNIP>
```
- The suite includes tools such as `Process Explorer`, an enhanced version of `Task Manager`, and `Process Monitor`, which can be used to monitor file system, registry, and network activity related to any process running on the system. 
- Some additional tools are TCPView, which is used to monitor internet activity, and PSExec, which can be used to manage/connect to systems via the SMB protocol remotely.
- These tools can be useful for penetration testers to, for example, discover interesting processes and possible privilege escalation paths as well as for lateral movement.



### Task Manager
- Windows Task Manager is a powerful tool for managing Windows systems. 
- It provides information about running processes, system performance, running services, startup programs, logged-in users/logged in user processes, and services.
- Task Manager can be opened by right-clicking on the taskbar and selecting `Task Manager`, pressing ctrl + shift + Esc, pressing ctrl + alt + del and selecting `Task Manager`, opening the start menu and typing `Task Manager`, or typing `taskmgr` from a CMD or PowerShell console.
![[taskmgr_png.png]]
![[Screenshot_20241109_112637.png]]
![[resource_monitor_png.png]]
![[Screenshot_20241109_112658.png]]



### Process Explorer
- [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer) is a part of the Sysinternals tool suite. 
- This tool can show which handles and DLL processes are loaded when a program runs. 
- Process Explorer shows a list of currently running processes, and from there, we can see what handles the process has selected in one view or the DLLs and memory-swapped files that have been loaded in another view. 
- We can also search within the tool to show which processes tie back to a specific handle or DLL. 
- The tool can also be used to analyze parent-child process relationships to see what child processes are spawned by an application and help troubleshoot any issues such as orphaned processed that can be left behind when a process is terminated.



### Questions
- Identify one of the non-standard update services running on the host. Submit the full name of the service executable (not the DisplayName) as your answer.
	- FoxItReaderUpdateService.exe