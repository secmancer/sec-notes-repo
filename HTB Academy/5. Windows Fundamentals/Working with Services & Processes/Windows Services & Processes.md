#### Overview
- **Windows Services**: Long-running processes that start automatically at system boot and continue running in the background even if the user logs out. Managed via the Service Control Manager (SCM), accessible through `services.msc`.
    
- **Windows Service Management**:
    - **GUI**: Accessed via `services.msc` (MMC add-in).
    - **Command Line**: Managed using `sc.exe` or PowerShell cmdlets such as `Get-Service`.

#### Service Information
- **Service Attributes**:
    - **Name**: Internal identifier.
    - **DisplayName**: Human-readable name.
    - **Status**: Current state (Running, Stopped, Paused, Starting, Stopping).
    - **Startup Type**: Automatic, Manual, or Disabled.
    - **User Account**: The account under which the service runs.
- **Example Output**:
    - `AdobeARMservice`:
        - **Status**: Running
        - **ServiceType**: Win32OwnProcess
    - `Appinfo`:
        - **Status**: Running
        - **ServiceType**: Win32OwnProcess, Win32ShareProcess


#### Service Categories
- **Local Services**
- **Network Services**
- **System Services**

![[Screenshot_20240912_153003.png]]
#### Critical System Services
- **smss.exe**: Session Manager SubSystem.
- **csrss.exe**: Client Server Runtime Process.
- **wininit.exe**: Starts the Wininit .ini file.
- **logonui.exe**: User login facilitator.
- **lsass.exe**: Local Security Authentication Server.
- **services.exe**: Manages services.
- **winlogon.exe**: Secure attention sequence and user profile handling.
- **System**: Background system process running the Windows kernel.
- **svchost.exe**: Hosts system services running from DLLs, using RPCSS or DCOM/PnP.

#### Processes
- **Processes**: Run in the background and can be automatic or application-driven. Critical processes include:
    - **Windows Logon Application**
    - **System Idle Process**
    - **Client Server Runtime**
    - **Local Security Authority Subsystem Service (LSASS)**: Manages security policies, logons, and user account password changes. High-value target for credential extraction.

#### Sysinternals Tools
- **Sysinternals Suite**: Portable applications for Windows administration.
    - **Common Tools**:
        - **ProcDump**: Monitors and dumps process data based on specified criteria.
        - **Process Explorer**: Enhanced Task Manager, shows handles, DLLs, and process relationships.
        - **Process Monitor**: Monitors file system, registry, and network activity.
        - **TCPView**: Monitors network activity.
        - **PSExec**: Manages systems via SMB protocol.
- **Usage Example**:
```
\\live.sysinternals.com\tools\procdump.exe -accepteula
```

#### Task Manager
- **Access Methods**:
    - Right-click on the taskbar
    - `ctrl + shift + esc`
    - `ctrl + alt + del` and select Task Manager
    - Start menu search
    - `taskmgr` in CMD or PowerShell

![[Screenshot_20240912_153016.png]]

- **Tabs**:
    - **Processes**: List of running applications and background processes, with resource usage.
    - **Performance**: CPU, memory, disk, network, GPU usage; includes Resource Monitor.
    - **App History**: Resource usage over time per application.
    - **Startup**: Applications configured to start at boot and their impact.
    - **Users**: Logged-in users and their process/resource usage.
    - **Details**: Process details, including PID, CPU, and memory usage.
    - **Services**: Name, PID, description, and status of each installed service.

![[Screenshot_20240912_153023.png]]
#### Process Explorer
- **Functionality**:
    - Shows handles and DLLs loaded by processes.
    - Displays parent-child process relationships.
    - Helps troubleshoot orphaned processes and analyze process details.

## Questions:
- Identify one of the non-standard update services running on the host. Submit the full name of the service executable (not the DisplayName) as your answer.
	- FoxItReaderUpdateService.exe