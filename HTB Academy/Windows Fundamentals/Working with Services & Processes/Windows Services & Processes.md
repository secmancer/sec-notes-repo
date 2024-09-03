### **Windows Services**
- **Functionality**: Services are long-running background processes that start automatically and continue running without user intervention.
- **Management**: Managed via the Service Control Manager (SCM), accessible through `services.msc`. Services can also be managed via the command line with `sc.exe` and PowerShell cmdlets like `Get-Service`.
- **Service Statuses**: Includes Running, Stopped, Paused, Starting, and Stopping.
- **Categories**: Local Services, Network Services, System Services.
- **Critical System Services**: Includes processes like `smss.exe`, `csrss.exe`, `lsass.exe`, and `svchost.exe`, which are vital for system operations and security.
- **Permissions**: Service management usually requires administrative privileges, and misconfigurations can lead to privilege escalation.

### **Processes**
- **Functionality**: Background operations, either part of the OS or started by applications.
- **Critical Processes**: Examples include Windows Logon Application, System Idle Process, and LSASS (`lsass.exe`), which is crucial for security policy enforcement and credential handling.
- **Sysinternals Tools**: Includes tools like Process Explorer and ProcDump for in-depth process analysis and troubleshooting.

### **Task Manager**
- **Tabs**:
    - **Processes**: Lists running applications and background processes.
    - **Performance**: Displays resource usage (CPU, memory, disk, etc.).
    - **App History**: Shows resource usage by applications over time.
    - **Startup**: Manages applications configured to start at boot.
    - **Users**: Shows logged-in users and their resource usage.
    - **Details**: Provides detailed information on running processes.
    - **Services**: Shows service information and can access the Services add-in.

### **Process Explorer**
- **Features**: Displays detailed information about process handles, DLLs, and memory usage. It helps analyze process relationships and troubleshoot issues.

### Questions:
- Identify one of the non-standard update services running on the host. Submit the full name of the service executable (not the DisplayName) as your answer.
	- FoxItReaderUpdateService.exe