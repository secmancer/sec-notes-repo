### Introduction
- **Windows Event Logs** are invaluable for SOC Analysts and IT Administrators to monitor, collect, and categorize network-wide events, aiding in proactive defense against suspicious activity.
- **Attackers** can exploit event logs for reconnaissance, disruption, or hiding traces, and sometimes uncover sensitive information like credentials during penetration testing.
- Enumerating event logs provides insights into an organization’s logging configuration (default or granular).
- Key topics discussed include:
    - The purpose and function of the Windows Event Log.
    - Types of information logged and storage locations.
    - Using the `wevtutil` command-line utility to interact with logs.
    - Utilizing PowerShell cmdlets for log management.



### What is the Windows Event Log?
- **Events** are actions or occurrences identifiable by hardware or software, categorized as:
    - **User-Generated Events**: Mouse movements, keyboard input, etc.
    - **Application-Generated Events**: Updates, crashes, memory usage, etc.
    - **System-Generated Events**: Uptime, updates, driver activity, logins, etc.
- **Event Logging** is a standardized, centralized method for recording key software and hardware events, as defined by Microsoft:
    - It enables consistent handling of event data from various sources.
- **Windows Event Log**:
    - A core Windows service managing events and logs.
    - Provides an API for applications to manage their own logs.
    - Runs at system initialization and operates within another executable's context.
- Before querying Event Logs via **cmd.exe** or **PowerShell**, it’s essential to understand:
    - Types of events.
    - Log elements.
    - Additional foundational concepts.



### Event Log Categories and Types
- The main four log categories include application, security, setup, and system. 
- Another type of category also exists called `forwarded events`.
![[Screenshot_20241111_140734.png]]



### Event Types
- There are five types of events that can be logged on Windows systems.
![[Screenshot_20241111_140754.png]]



### Event Severity Levels
- Each log can have one of five severity levels associated with it, denoted by a number.
![[Screenshot_20241111_140816.png]]



### Elements of a Windows Event Log
- The Windows Event Log provides information about hardware and software events on a Windows system. 
- All event logs are stored in a standard format and include the following elements:
	- `Log name`: As discussed above, the name of the event log where the events will be written. By default, events are logged for `system`, `security`, and `applications`.
	- `Event date/time`: Date and time when the event occurred
	- `Task Category`: The type of recorded event log
	- `Event ID`: A unique identifier for sysadmins to identify a specific logged event
	- `Source`: Where the log originated from, typically the name of a program or software application
	- `Level`: Severity level of the event. This can be information, error, verbose, warning, critical
	- `User`: Username of who logged onto the host when the event occurred
	- `Computer`: Name of the computer where the event is logged
- There are many Event IDs that an organization can monitor to detect various issues. 
- In an Active Directory environment, [this list](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/appendix-l--events-to-monitor) includes key events that are recommended to be monitored for to look for signs of a compromise.
- [This](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/) searchable database of Event IDs is worth perusing to understand the depth of logging possible on a Windows system.



### Windows Event Log Technical Details
- The Windows Event Log is handled by the `EventLog` services. 
- On a Windows system, the service's display name is `Windows Event Log`, and it runs inside the service host process [svchost.exe](https://en.wikipedia.org/wiki/Svchost.exe). 
- It is set to start automatically at system boot by default. 
- It is difficult to stop the EventLog service as it has multiple dependency services.
- If it is stopped, it will likely cause significant system instability. 
- By default, Windows Event Logs are stored in `C:\Windows\System32\winevt\logs` with the file extension `.evtx`.
```powershell-session
PS C:\htb> ls C:\Windows\System32\winevt\logs

    Directory: C:\Windows\System32\winevt\logs


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        11/16/2022   2:19 PM        7409664 Application.evtx
-a----         6/14/2022   8:20 PM          69632 HardwareEvents.evtx
-a----         6/14/2022   8:20 PM          69632 Internet Explorer.evtx
-a----         6/14/2022   8:20 PM          69632 Key Management Service.evtx        
-a----         8/23/2022   7:01 PM          69632 Microsoft-Client-License-Flexible-P
                                                  latform%4Admin.evtx
-a----        11/16/2022   2:19 PM        1052672 Microsoft-Client-Licensing-Platform
                                                  %4Admin.evtx


<SNIP>
```
- We can interact with the Windows Event log using the [Windows Event Viewer](https://en.wikipedia.org/wiki/Event_Viewer) GUI application via the command line utility [wevtutil](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil), or using the [Get-WinEvent](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-7.3) PowerShell cmdlet. 
- Both `wevtutil` and `Get-WinEvent` can be used to query Event Logs on both local and remote Windows systems via cmd.exe or PowerShell.



### Interacting with the Windows Event Log - wevtutil
- The [wevtutil](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil) command line utility can be used to retrieve information about event logs. It can also be used to export, archive, and clear logs, among other commands.
- #### Wevtutil without Parameters
```cmd-session
C:\htb> wevtutil /?

Windows Events Command Line Utility.

Enables you to retrieve information about event logs and publishers, install
and uninstall event manifests, run queries, and export, archive, and clear logs.

Usage:

You can use either the short (for example, ep /uni) or long (for example,
enum-publishers /unicode) version of the command and option names. Commands,
options and option values are not case-sensitive.

Variables are noted in all upper-case.

wevtutil COMMAND [ARGUMENT [ARGUMENT] ...] [/OPTION:VALUE [/OPTION:VALUE] ...]

Commands:

el | enum-logs          List log names.
gl | get-log            Get log configuration information.
sl | set-log            Modify configuration of a log.
ep | enum-publishers    List event publishers.
gp | get-publisher      Get publisher configuration information.
im | install-manifest   Install event publishers and logs from manifest.
um | uninstall-manifest Uninstall event publishers and logs from manifest.
qe | query-events       Query events from a log or log file.
gli | get-log-info      Get log status information.
epl | export-log        Export a log.
al | archive-log        Archive an exported log.
cl | clear-log          Clear a log.

<SNIP>
```
- We can use the `el` parameter to enumerate the names of all logs present on a Windows system.
- #### Enumerating Log Sources
```cmd-session
C:\htb> wevtutil el

AMSI/Debug
AirSpaceChannel
Analytic
Application
DirectShowFilterGraph
DirectShowPluginControl
Els_Hyphenation/Analytic
EndpointMapper
FirstUXPerf-Analytic
ForwardedEvents
General Logging
HardwareEvents

<SNIP>
```
- With the `gl` parameter, we can display configuration information for a specific log, notably whether the log is enabled or not, the maximum size, permissions, and where the log is stored on the system.
- #### Gathering Log Information
```cmd-session
C:\htb> wevtutil gl "Windows PowerShell"

name: Windows PowerShell
enabled: true
type: Admin
owningPublisher:
isolation: Application
channelAccess: O:BAG:SYD:(A;;0x2;;;S-1-15-2-1)(A;;0x2;;;S-1-15-3-1024-3153509613-960666767-3724611135-2725662640-12138253-543910227-1950414635-4190290187)(A;;0xf0007;;;SY)(A;;0x7;;;BA)(A;;0x7;;;SO)(A;;0x3;;;IU)(A;;0x3;;;SU)(A;;0x3;;;S-1-5-3)(A;;0x3;;;S-1-5-33)(A;;0x1;;;S-1-5-32-573)
logging:
  logFileName: %SystemRoot%\System32\Winevt\Logs\Windows PowerShell.evtx
  retention: false
  autoBackup: false
  maxSize: 15728640
publishing:
  fileMax: 1
```
- The `gli` parameter will give us specific status information about the log or log file, such as the creation time, last access and write times, file size, number of log records, and more.
```cmd-session
C:\htb> wevtutil gli "Windows PowerShell"

creationTime: 2020-10-06T16:57:38.617Z
lastAccessTime: 2022-10-26T19:05:21.533Z
lastWriteTime: 2022-10-26T19:05:21.533Z
fileSize: 11603968
attributes: 32
numberOfLogRecords: 9496
oldestRecordNumber: 1
```
- There are many ways we can query for events. 
- For example, let's say we want to display the last 5 most recent events from the Security log in text format. 
- Local admin access is needed for this command.
- #### Querying Events
```cmd-session
C:\htb> wevtutil qe Security /c:5 /rd:true /f:text

Event[0]
  Log Name: Security
  Source: Microsoft-Windows-Security-Auditing
  Date: 2022-11-16T14:54:13.2270000Z
  Event ID: 4799
  Task: Security Group Management
  Level: Information
  Opcode: Info
  Keyword: Audit Success
  User: N/A
  User Name: N/A
  Computer: ICL-WIN11.greenhorn.corp
  Description: 
A security-enabled local group membership was enumerated.

Subject:
        Security ID:            S-1-5-18
        Account Name:           ICL-WIN11$
        Account Domain:         GREENHORN
        Logon ID:               0x3E7

Group:
        Security ID:            S-1-5-32-544
        Group Name:             Administrators
        Group Domain:           Builtin

Process Information:
        Process ID:             0x56c
        Process Name:           C:\Windows\System32\svchost.exe

Event[1]
  Log Name: Security
  Source: Microsoft-Windows-Security-Auditing
  Date: 2022-11-16T14:54:13.0160000Z
  Event ID: 4672
  Task: Special Logon
  Level: Information
  Opcode: Info
  Keyword: Audit Success
  User: N/A
  User Name: N/A
  Computer: ICL-WIN11.greenhorn.corp
  Description:
Special privileges assigned to new logon.

Subject:
        Security ID:            S-1-5-21-4125911421-2584895310-3954972028-1001        
        Account Name:           htb-student
        Account Domain:         ICL-WIN11
        Logon ID:               0x8F211

Privileges:             SeSecurityPrivilege
                        SeTakeOwnershipPrivilege
                        SeLoadDriverPrivilege
                        SeBackupPrivilege
                        SeRestorePrivilege
                        SeDebugPrivilege
                        SeSystemEnvironmentPrivilege
                        SeImpersonatePrivilege
                        SeDelegateSessionUserImpersonatePrivilege

Event[2]
  Log Name: Security
  Source: Microsoft-Windows-Security-Auditing
  Date: 2022-11-16T14:54:13.0160000Z
  Event ID: 4624
  Task: Logon
  Level: Information
  Opcode: Info
  Keyword: Audit Success
  User: N/A
  User Name: N/A
  Computer: ICL-WIN11.greenhorn.corp
  Description:
An account was successfully logged on.

Subject:
        Security ID:            S-1-5-18
        Account Name:           ICL-WIN11$
        Account Domain:         GREENHORN
        Logon ID:               0x3E7


<SNIP>
```
- We can also export events from a specific log for offline processing. 
- Local admin is also needed to perform this export.
- #### Exporting Events
```cmd-session
C:\htb> wevtutil epl System C:\system_export.evtx
```



### Interacting with the Windows Event Log - PowerShell
- Similarly, we can interact with Windows Event Logs using the [Get-WinEvent](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-7.3) PowerShell cmdlet. 
- Like with the `wevtutil` examples, some commands require local admin-level access.
- To start, we can list all logs on the computer, giving us the number of records in each log.
- #### PowerShell - Listing All Logs
```powershell-session
PS C:\htb> Get-WinEvent -ListLog *

LogMode   MaximumSizeInBytes RecordCount LogName
-------   ------------------ ----------- -------
Circular            15728640         657 Windows PowerShell
Circular            20971520       10713 System
Circular            20971520       26060 Security
Circular            20971520           0 Key Management Service
Circular             1052672           0 Internet Explorer
Circular            20971520           0 HardwareEvents
Circular            20971520        6202 Application
Circular             1052672             Windows Networking Vpn Plugin Platform/Op...
Circular             1052672             Windows Networking Vpn Plugin Platform/Op... 
Circular             1052672           0 SMSApi
Circular             1052672          61 Setup
Circular            15728640          24 PowerShellCore/Operational
Circular             1052672          99 OpenSSH/Operational
Circular             1052672          46 OpenSSH/Admin

<SNIP>
```
- We can also list information about a specific log. Here we can see the size of the `Security` log.
- #### Security Log Details
```powershell-session
PS C:\htb> Get-WinEvent -ListLog Security

LogMode   MaximumSizeInBytes RecordCount LogName
-------   ------------------ ----------- -------
Circular            20971520       26060 Security
```
- We can query for the last X number of events, looking specifically for the last five events using the `-MaxEvents` parameter. 
- Here we will list the last five events recorded in the Security log. 
- By default, the newest logs are listed first. If we want to get older logs first, we can reverse the order to list the oldest ones first using the `-Oldest` parameter.
- #### Querying Last Five Events
```powershell-session
PS C:\htb> Get-WinEvent -LogName 'Security' -MaxEvents 5 | Select-Object -ExpandProperty Message

An account was logged off.

Subject:
        Security ID:            S-1-5-111-3847866527-469524349-687026318-516638107-1125189541-6052
        Account Name:           sshd_6052
        Account Domain:         VIRTUAL USERS
        Logon ID:               0x8E787

Logon Type:                     5

This event is generated when a logon session is destroyed. It may be positively correlated with a logon event using the Logon ID value. Logon IDs are only unique between reboots on the same computer.
Special privileges assigned to new logon.

Subject:
        Security ID:            S-1-5-18
        Account Name:           SYSTEM
        Account Domain:         NT AUTHORITY
        Logon ID:               0x3E7

Privileges:             SeAssignPrimaryTokenPrivilege
                        SeTcbPrivilege
                        SeSecurityPrivilege
                        SeTakeOwnershipPrivilege
                        SeLoadDriverPrivilege
                        SeBackupPrivilege
                        SeRestorePrivilege
                        SeDebugPrivilege
                        SeAuditPrivilege
                        SeSystemEnvironmentPrivilege
                        SeImpersonatePrivilege
                        SeDelegateSessionUserImpersonatePrivilege
An account was successfully logged on.

<SNIP>
```
- We can dig deeper and look at specific event IDs in specific logs. 
- Let's say we only want to look at logon failures in the Security log, checking for Event ID [4625: An account failed to log on](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625). 
- From here, we could use the `-ExpandProperty` parameter to dig deeper into specific events, list logs from oldest to newest, etc.
- #### Filtering for Logon Failures
```powershell-session
PS C:\htb> Get-WinEvent -FilterHashTable @{LogName='Security';ID='4625 '}

   ProviderName: Microsoft-Windows-Security-Auditing

TimeCreated                      Id LevelDisplayName Message
-----------                      -- ---------------- -------
11/16/2022 2:53:16 PM          4625 Information      An account failed to log on....  
11/16/2022 2:53:16 PM          4625 Information      An account failed to log on.... 
11/16/2022 2:53:12 PM          4625 Information      An account failed to log on.... 
11/16/2022 2:50:36 PM          4625 Information      An account failed to log on.... 
11/16/2022 2:50:29 PM          4625 Information      An account failed to log on.... 
11/16/2022 2:50:21 PM          4625 Information      An account failed to log on....

<SNIP>
```
- We can also look at only events with a specific information level. Let's check all System logs for only `critical` events with information level `1`. Here we see just one log entry where the system did not reboot cleanly.
```powershell-session
PS C:\htb> Get-WinEvent -FilterHashTable @{LogName='System';Level='1'} | select-object -ExpandProperty Message

The system has rebooted without cleanly shutting down first. This error could be caused if the system stopped re
```
- Practice more with `wevtutil` and `Get-WinEvent` to become more comfortable with searching logs. 
- Microsoft provides some [examples](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-7.3) for `Get-WinEvent`, while [this site](https://www.thewindowsclub.com/what-is-wevtutil-and-how-do-you-use-it) shows examples for `wevtutil`, and [this site](https://4sysops.com/archives/search-the-event-log-with-the-get-winevent-powershell-cmdlet/) has some additional examples for using `Get-WinEvent`.



### Moving On
- The **Windows Event Log** is a powerful tool for logging and monitoring when configured properly, allowing granular control over what is logged.
- Sensitive data, such as passwords, can sometimes be found in logs, highlighting its importance for both **penetration testers** and **blue teamers**.
- **SIEM tools** enhance log management by forwarding logs and setting up alerts for specific Event IDs (e.g., Kerberoasting or Password Spraying).
- Mastery of Event Logs is essential:
    - **Penetration testers**: Use logs to gather environmental insights and potentially extract sensitive data.
    - **Blue teamers**: Leverage Event Logs for effective alerting and monitoring.
- The next topic will explore **networking operations via the command line** on Windows systems.



### Questions
- Explore the targets provided and practice your Event Log PowerShell Kung-Fu. Type COMPLETE as the answer when finished.
	- COMPLETE