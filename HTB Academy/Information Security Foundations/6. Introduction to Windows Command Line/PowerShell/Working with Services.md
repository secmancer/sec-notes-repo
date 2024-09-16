#### Scenario:
- **Issue:** Mr. Tanaka reported a window popping up that he initially thought was a Windows update. Now, he is receiving alerts that Defender is turned off and his host is sluggish.
- **Objective:** Identify which Defender-related services are shut off and re-enable them if possible. Review event logs to investigate further.



#### Understanding Windows Services:
- **Definition:** Services are background processes that manage and maintain application components on the host. They typically do not require user interaction and have no direct user interface.
- **Categories:**
    - **Local Services:** Run with the local system account and affect only the local machine.
    - **Network Services:** Use network credentials to access network resources.
    - **System Services:** Core services essential for the operating system.



#### PowerShell Cmdlets for Services:
PowerShell provides the `Microsoft.PowerShell.Management` module for interacting with services. Here are some key cmdlets:

- **Get-Service:** Retrieves the status of services.
- **New-Service:** Creates a new service.
- **Remove-Service:** Deletes a service.
- **Restart-Service:** Restarts a service.
- **Resume-Service:** Resumes a paused service.
- **Set-Service:** Modifies the properties of a service.
- **Start-Service:** Starts a stopped service.
- **Stop-Service:** Stops a running service.
- **Suspend-Service:** Pauses a running service.


#### Getting Help:
To find information about service-related cmdlets:
```
Get-Help *-Service
```
#### Example Commands:
1. **Retrieve All Services:**
```
Get-Service
```
2. **Check Specific Service Status:**\
```
Get-Service -Name "ServiceName"
```
3. **Start a Service:**
```
Start-Service -Name "ServiceName"
```
4. **Stop a Service:**
```
Stop-Service -Name "ServiceName"
```
5. **Restart a Service:**
```
Restart-Service -Name "ServiceName"
```
6. **Set Service to Automatic Start:**
```
Set-Service -Name "ServiceName" -StartupType Automatic
```
7. **Check Service Dependencies:**
```
Get-Service -Name "ServiceName" | Select-Object -ExpandProperty ServicesDependedOn
```


#### Notes:
- **Permissions:** To manage or modify services, you must have the appropriate permissions. This typically requires administrative rights or specific permissions granted by domain groups.
- **Administrative Context:** Run PowerShell as an administrator for the necessary permissions to manage services.


#### Overview:
To effectively manage and troubleshoot services on a host, it's crucial to understand their status and configuration. Services can be in various states: Running, Stopped, or Paused. They can also be set to start automatically, manually, or with a delay.

#### Initial Service Overview:
- **Listing Services:** Use `Get-Service` to obtain a list of services.
- **Service Status:** Services can be Running, Stopped, or Paused.
- **Startup Type:** Services can be set to start Automatically, Manually, or Delayed.

#### Example Commands:
- **Retrieve and Display Services:**
    - Use `Get-Service` to list services.
    - Format the output with `Format-Table` to view `DisplayName` and `Status`.
- **Count Services:**
    - Use `Get-Service | Measure` to count the total number of services, e.g., 321 services.

#### Filtering for Specific Services:
- **Filter by Name:**
    - To focus on Defender-related services, use `Get-Service | Where-Object DisplayName -like '*Defender*'`.
    - Display relevant properties: `DisplayName`, `ServiceName`, and `Status`.

#### Managing Services:
- **Start a Service:**
    - Use `Start-Service -Name ServiceName` to start a stopped service. For example, `Start-Service WinDefend` to start Microsoft Defender Antivirus Service.
- **Verify Service Status:**
    - Use `Get-Service -Name ServiceName` to check the current status of the service.
- **Stop a Service:**
    - Use `Stop-Service -Name ServiceName` to stop a running service. For example, `Stop-Service Spooler` to stop the Spooler service.
- **Change Service Startup Type:**
    - Use `Set-Service -Name ServiceName -StartType Disabled` to change the startup type of a service. For example, `Set-Service -Name Spooler -StartType Disabled` to disable the Spooler service.

#### Additional Considerations:
- **Permissions:** Ensure you have administrative privileges to modify service configurations.
- **Service Removal:** `Remove-Service` cmdlet requires PowerShell version 7. For hosts running PowerShell 5.1, use `sc.exe` tool for service removal.

#### Security Note:
- **Investigate Odd Services:** If a service has an unusual display name or behavior, investigate further. For example, stop the service and consult with the security team if necessary.


#### Overview:
PowerShell allows us to manage and query services not only on local hosts but also remotely. This can be particularly useful in domain environments where multiple hosts need to be checked or managed.

#### Remote Service Queries:
- **Query Remote Services:**
    - Use `Get-Service -ComputerName RemoteHostName` to retrieve the list of services from a remote host. Replace `RemoteHostName` with the name of the remote computer.
- **Filter Remote Output:**
    - To filter services by status, use `Get-Service -ComputerName RemoteHostName | Where-Object {$_.Status -eq "Running"}`. This command will show only services that are currently running.

#### Using PowerShell Pipeline:
- **Object Handling:**
    - PowerShell treats all output as objects, including remote command output. This allows for powerful filtering and manipulation using the pipeline and `Where-Object` cmdlet.

#### Invoke-Command:
- **Run Commands Remotely:**
    - Use `Invoke-Command -ComputerName RemoteHostName -ScriptBlock {Get-Service -Name 'ServiceName'}` to run commands on multiple remote computers. Replace `RemoteHostName` with the remote computer name and `'ServiceName'` with the service name you want to query.
- **Example Usage:**
    - To check the status of the `windefend` service on multiple hosts, use `Invoke-Command -ComputerName RemoteHostName1,RemoteHostName2 -ScriptBlock {Get-Service -Name 'windefend'}`.

#### Breakdown of `Invoke-Command`:
- **Invoke-Command:** Initiates the command execution on specified computers.
- **ComputerName:** Lists the remote computers to query, separated by commas.
- **ScriptBlock:** Contains the commands to be executed remotely, enclosed in `{}`.

#### Scenario Application:
- **Investigate Service Anomalies:**
    - For services with unusual `DisplayName` values or other anomalies, use the `-ComputerName` parameter or `Invoke-Command` to query all hosts in the environment. This helps identify if other hosts are similarly affected.

#### Administrative Efficiency:
- **Power and Control:**
    - Managing services remotely streamlines administrative tasks and can help in quickly addressing issues across multiple hosts. This capability is crucial for effective system management and threat mitigation.

#### Next Steps:
- **Introduction to Windows Registry:**
    - The next section will cover the Windows Registry and how to interact with it on Windows hosts, providing additional tools for system management and troubleshooting.


## Questions
- What Cmdlet will show us the current services of a host?
	- Get-Service
- If we wanted to start the Windows Defender Service, what command would we use?
	- Start-Service WinDefend
- What Cmdlet will allow us to execute a command on a remote host?
	- Invoke-Command