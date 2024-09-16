**Introduction to `sc`**
- **Purpose**: `sc` is a command line utility for managing and interacting with Windows services and the Service Control Manager.
- **Capabilities**: It allows querying, modifying, and managing services both locally and remotely.


**Basic Usage**
- **Command Structure**: `sc <server> [command] [service name] <option1> <option2>...`
    - **"server"**: The server to connect to (e.g., "\ServerName").
    - **[command]**: The action to perform (e.g., query, start, stop).
    - **[service name]**: The specific service to act upon.
    - **"option1", "option2"**: Additional options for the command.


**Common Commands and Options**
- **Query Services**
    - `sc query`: Enumerates status for active services and drivers.
    - `sc query eventlog`: Displays status for the eventlog service.
    - `sc queryex eventlog`: Displays extended status for the eventlog service.
    - `sc query type= driver`: Enumerates only active drivers.
    - `sc query type= service`: Enumerates only Win32 services.
    - `sc query state= all`: Enumerates all services and drivers.
    - `sc query bufsize= 50`: Enumerates with a 50-byte buffer.
    - `sc query ri= 14`: Enumerates with resume index = 14.
    - `sc queryex group= ""`: Enumerates active services not in a group.
    - `sc query type= interact`: Enumerates all interactive services.
    - `sc query type= driver group= NDIS`: Enumerates all NDIS drivers.


**Using `sc` as an Attacker**
- **Determine Running Services**: Use `sc query` to list active services and drivers on the host.
- **Disable Antivirus**: Locate the antivirus service using `sc query` and attempt to disable or stop it.
- **Modify Services**: Utilize commands to start, stop, or modify services as needed.


**Example Commands**
- **Check All Services**: `sc query state= all`
- **Check Specific Service**: `sc query <service name>`
- **Extended Status**: `sc queryex <service name>`
- **Start Service**: `sc start <service name>`
- **Stop Service**: `sc stop <service name>`
- **Pause Service**: `sc pause <service name>`


**Help and Syntax**
- **Basic Help**: Run `sc` without parameters to get a description and list of commands.
- **Further Help**: Use `sc [command]` for more detailed help on specific commands.


**Querying Services**
- **Purpose**: Querying services allows us to gather information about running services, including their state, process ID (PID), and service type.
- **Command**:
    - `sc query type= service`
- **Note**: Ensure correct spacing for query parameters. For example, `type= service` is correct.


**Example Output**
- **SERVICE_NAME**: Name of the service.
- **DISPLAY_NAME**: Description or display name of the service.
- **TYPE**: Service type (e.g., WIN32).
- **STATE**: Current state (e.g., RUNNING).
- **WIN32_EXIT_CODE**: Exit code for the last operation.
- **SERVICE_EXIT_CODE**: Exit code of the service.
- **CHECKPOINT**: Checkpoint for service startup.
- **WAIT_HINT**: Time in milliseconds to wait for the service to start.


**Checking Windows Defender**
- **Command**: `sc query windefend`
- **Outcome**:
    - Service is running.
    - Access Denied errors may occur if the current user does not have sufficient permissions to stop or pause the service.


**Stopping Services**
- **Command**: `sc stop <service name>`
- **Example**: Stopping the `windefend` service may be restricted to SYSTEM accounts, highlighting the importance of understanding permission levels.
- **Output**:
    - **STATE**: Shows the service transition (e.g., STOP_PENDING, STOPPED).



**Starting Services**
- **Command**: `sc start <service name>`
- **Example**: Restarting the `Spooler` service.
- **Output**:
    - **STATE**: Shows the service status transition (e.g., START_PENDING, RUNNING).
    - **PID**: Process ID of the service after it starts.


**Practical Considerations**
- **Permissions**: Stopping or starting certain services might require administrator or SYSTEM permissions.
- **Service Dependencies**: Some services may not respond to start/stop commands if other services depend on them.
- **Logging and Alerts**: Attempting to stop or start services with insufficient permissions may generate logs and alerts, potentially revealing unauthorized activity.


**Example Commands and Outputs**
- **Query All Services**:
    - `sc query type= service`
    - **Output**: List of running services and their statuses.
- **Stop Service**:
    - `sc stop Spooler`
    - **Output**: Transition state of the service.
- **Start Service**:
    - `sc start Spooler`
    - **Output**: State change to RUNNING with updated PID.


Modifying services on a system is a potent technique for attackers to control system behavior and persistence. Services can be altered to disable them, change their startup behavior, or modify their executable path. Here’s a detailed guide on how to work with services, using an example of disabling Windows Updates.


**Disabling Windows Updates Using `sc`**
1. **Service Configuration**
    - Use the `sc config` command to modify existing services.
    - Changes are recorded in the Windows registry and Service Control Manager (SCM).
    - Changes become effective after restarting the service.
    **Note:** Modifying services can lead to permanent changes. Exercise caution to avoid unintended consequences.


**Services for Windows Updates**
- Windows Update relies on:
    - `wuauserv` (Windows Update Service)
    - `bits` (Background Intelligent Transfer Service)


**Checking Service Status**
- Check the current status of these services:
```
C:\WINDOWS\system32> sc query wuauserv
C:\WINDOWS\system32> sc query bits
```
Example Output:
```
SERVICE_NAME: wuauserv
    TYPE               : 30  WIN32
    STATE              : 1  STOPPED

SERVICE_NAME: bits
    TYPE               : 30  WIN32
    STATE              : 4  RUNNING
```


**Stopping Services**
- Stop the services if they are running:
```
C:\WINDOWS\system32> sc stop bits
```


**Disabling Services**
- Change the start type of the services to `disabled`:
```
C:\WINDOWS\system32> sc config wuauserv start= disabled
[SC] ChangeServiceConfig SUCCESS

C:\WINDOWS\system32> sc config bits start= disabled
[SC] ChangeServiceConfig SUCCESS
```


**Verifying Service Status**
- Ensure that services are disabled and cannot be started:
```
C:\WINDOWS\system32> sc start wuauserv
[SC] StartService FAILED 1058: The service cannot be started, either because it is disabled or because it has no enabled devices associated with it.

C:\WINDOWS\system32> sc start bits
[SC] StartService FAILED 1058: The service cannot be started, either because it is disabled or because it has no enabled devices associated with it.
```
**Note:** To revert changes, set `start= auto` to re-enable the services.

#### Key Points
- **Permissions:** Modifying services typically requires elevated privileges. Ensure you have the necessary permissions to make these changes.
- **Impact:** Disabling critical services like Windows Update can leave a system vulnerable to exploits. This technique can be useful for maintaining persistence but also risks detection if not done stealthily.
- **Reversal:** To undo changes and restore normal functionality, re-enable services by setting their start type to `auto`.


In addition to using `sc` for managing services, there are several other commands you can use to query and display information about services. Each tool provides different details and may be useful in various contexts.


#### Using `tasklist`
- **Purpose:** Lists all currently running processes along with their associated services.
- **Command:**
```
tasklist /svc
```
- **Example Output:**
```
Image Name                     PID Services
========================= ======== ============================================
System Idle Process              0 N/A
System                           4 N/A
Registry                       108 N/A
smss.exe                       412 N/A
csrss.exe                      612 N/A
wininit.exe                    684 N/A
csrss.exe                      708 N/A
services.exe                   768 N/A
lsass.exe                      796 KeyIso, SamSs, VaultSvc
winlogon.exe                   856 N/A
svchost.exe                    984 BrokerInfrastructure, DcomLaunch, PlugPlay,
                                 Power, SystemEventsBroker
...
```
- **Usage:** Provides a full list of processes with their respective PID and the services hosted under each process, useful for identifying what services are associated with which processes.


#### Using `net start`
- **Purpose:** Lists all currently running services.
- **Command:**
```
net start
```
- **Example Output:**
```
These Windows services are started:

   Application Information
   AppX Deployment Service (AppXSVC)
   AVCTP service
   Background Tasks Infrastructure Service
   Base Filtering Engine
   BcastDVRUserService_3321a
   Capability Access Manager Service
   ...
```
- **Usage:** Shows a list of all active services on the system. Similar commands include `net stop`, `net pause`, and `net continue` for managing services.


#### Using `wmic`
- **Purpose:** Provides a wide range of information about services and other system components. Note that WMIC is deprecated in current Windows versions.
- **Command:**
```
wmic service list brief
```
- **Example Output:**
```
ExitCode  Name                                      ProcessId  StartMode  State    Status
1077      AJRouter                                  0          Manual     Stopped  OK
1077      ALG                                       0          Manual     Stopped  OK
1077      AppIDSvc                                  0          Manual     Stopped  OK
0         Appinfo                                   5016       Manual     Running  OK
1077      AppMgmt                                   0          Manual     Stopped  OK
1077      AppReadiness                              0          Manual     Stopped  OK
1077      AppVClient                                0          Disabled   Stopped  OK
0         AppXSvc                                   9996       Manual     Running  OK
...
```
- **Usage:** Lists all services with details such as Name, ProcessId, StartMode, State, and Status. Provides a comprehensive view of service configuration.


#### Important Notes
- **`tasklist`** is useful for linking services to processes but does not show service configuration details.
- **`net start`** offers a straightforward view of running services but lacks detailed information on service configuration.
- **`wmic`** provides extensive service information but is deprecated and should be used cautiously, with consideration for future compatibility.

As penetration testers, interacting with Windows services is a critical part of privilege escalation and other activities. Since GUI access to a host isn't always available, proficiency with command-line tools is essential.


#### Key Points:
1. **Command-Line Interaction**:
    - Mastering command-line tools for managing Windows services is crucial when GUI access is not possible.
    - Various commands can be used to query, start, stop, and modify services.
2. **Command-Line Tools**:
    - **`sc`**: Primary tool for querying, starting, stopping, and configuring services.
    - **`tasklist /svc`**: Provides a list of running processes and associated services.
    - **`net start`**: Lists all currently running services.
    - **`wmic service list brief`**: Offers detailed information about services but is deprecated in newer Windows versions.
3. **PowerShell Equivalents**:
    - PowerShell provides equivalent commands for managing services, which will be covered in a later section.
    - PowerShell commands offer advanced features and more granular control compared to `cmd.exe` tools.
4. **Transition to Windows Scheduled Tasks**:
    - After mastering command-line service management, understanding Windows Scheduled Tasks is the next step.
    - Scheduled Tasks can be used for persistence and automating tasks, which are important for both offensive and defensive security operations.


#### Next Steps:
- **Explore PowerShell Commands**: Learn how to perform similar actions using PowerShell, which provides enhanced capabilities for managing and monitoring services.
- **Study Windows Scheduled Tasks**: Understand how to leverage Scheduled Tasks for various security purposes, including maintaining persistence and automating actions.

## Questions
- What command string will stop a service named 'red-light'? (full command as the answer)
	- sc stop red-light
- What Windows executable will allow us to create, query, and modify services on a host?
	- sc