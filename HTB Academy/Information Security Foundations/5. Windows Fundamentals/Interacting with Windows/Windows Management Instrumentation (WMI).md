### Windows Management Instrumentation (WMI) Overview
WMI is a subsystem in PowerShell designed for system administration and monitoring. It consolidates management of devices and applications across networks and has been part of Windows since Windows 2000. The primary components of WMI are:

#### Components of WMI
- **WMI Service**: The Windows Management Instrumentation process, which runs automatically at boot and acts as an intermediary between WMI providers, the WMI repository, and managing applications.
- **Managed Objects**: Logical or physical components that can be managed by WMI.
- **WMI Providers**: Objects that monitor events or data related to specific objects.
- **Classes**: Used by WMI providers to pass data to the WMI service.
- **Methods**: Attached to classes to perform actions, such as starting or stopping processes on remote machines.
- **WMI Repository**: A database storing all static WMI-related data.
- **CIM Object Manager**: Requests data from WMI providers and returns it to the requesting application.
- **WMI API**: Allows applications to access the WMI infrastructure.
- **WMI Consumer**: Sends queries to objects via the CIM Object Manager.

![[Screenshot_20240912_154015.png]]
#### Uses of WMI
- **Status Information**: For local/remote systems.
- **Configuration**: Security settings on remote machines and applications.
- **Permissions**: Setting and changing user and group permissions.
- **System Properties**: Setting and modifying system properties.
- **Code Execution**: Running code.
- **Process Scheduling**: Scheduling tasks.
- **Logging**: Setting up logging.

#### WMIC Commands
- **Interactive Shell**: Open WMIC interactive shell by typing `WMIC` in the command prompt.
- **Direct Commands**: Run commands directly, e.g., `wmic computersystem get name` to retrieve the hostname.
- **Command Listing**: View a list of commands and aliases with `WMIC /?`.

#### WMIC Global Switches
- `/NAMESPACE`: Specifies the namespace path.
- `/ROLE`: Specifies the path for role definitions.
- `/NODE`: Specifies the server the alias operates against.
- `/IMPLEVEL`: Sets client impersonation level.
- `/AUTHLEVEL`: Sets client authentication level.
- `/LOCALE`: Specifies language ID.
- `/PRIVILEGES`: Enable or disable privileges.
- `/TRACE`: Outputs debugging information.
- `/RECORD`: Logs commands and output.
- `/INTERACTIVE`: Sets or resets interactive mode.
- `/FAILFAST`: Sets or resets FailFast mode.
- `/USER`: Specifies user for session.
- `/PASSWORD`: Specifies password for session login.
- `/OUTPUT`: Specifies output redirection mode.
- `/APPEND`: Specifies output redirection mode.
- `/AGGREGATE`: Sets or resets aggregate mode.
- `/AUTHORITY`: Specifies authority type.
- `/?[:<BRIEF|FULL>]`: Usage information.

**Example WMIC Command**
```
wmic os list brief
```
This command lists brief information about the operating system:
- **BuildNumber**: 19041
- **Organization**: Owner
- **RegisteredUser**: 00123-00123-00123-AAOEM
- **SystemDirectory**: C:\Windows\system32
- **Version**: 10.0.19041

#### Using WMI with PowerShell
- **Get-WmiObject**: Retrieves instances of WMI classes or information about available classes.
```
Get-WmiObject -Class Win32_OperatingSystem | select SystemDirectory, BuildNumber, SerialNumber, Version | ft
```
- **Invoke-WmiMethod**: Calls methods of WMI objects.
```
Invoke-WmiMethod -Path "CIM_DataFile.Name='C:\users\public\spns.csv'" -Name Rename -ArgumentList "C:\Users\Public\kerberoasted_users.csv"
```

## Questions
- Use WMI to find the serial number of the system.
	- 00329-10280-00000-AA938