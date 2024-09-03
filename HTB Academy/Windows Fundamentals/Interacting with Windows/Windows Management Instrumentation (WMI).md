### Key Components of WMI
- **WMI Service**: The core service that runs in the background and interacts with WMI providers and applications.
- **Managed Objects**: Logical or physical components managed by WMI.
- **WMI Providers**: Objects that monitor and provide data about specific managed objects.
- **Classes**: Structures used by WMI providers to pass data to the WMI service.
- **Methods**: Actions attached to classes that perform operations, such as starting or stopping processes.
- **WMI Repository**: A database storing all static WMI data.
- **CIM Object Manager**: Requests data from WMI providers and returns it to applications.
- **WMI API**: Allows applications to access WMI.
- **WMI Consumer**: Sends queries to objects through the CIM Object Manager.

### Uses of WMI
- Retrieving status information for local/remote systems.
- Configuring security settings on remote machines and applications.
- Managing user and group permissions.
- Modifying system properties.
- Executing code and scheduling processes.
- Setting up logging.

### WMIC Overview
WMIC is a command-line utility for WMI. It is now deprecated but still used in many environments:
- **Command Example**: `wmic os list brief` - Retrieves a brief summary of the operating system information.
- **Switches**: Adjust the behavior and output of WMIC commands (e.g., `/NAMESPACE`, `/AUTHLEVEL`, `/USER`, etc.).

### PowerShell and WMI
- **Get-WmiObject**: Retrieves instances of WMI classes. Example: `Get-WmiObject -Class Win32_OperatingSystem` gets OS information.
- **Invoke-WmiMethod**: Calls methods of WMI objects. Example: Renaming a file with `Invoke-WmiMethod -Path "CIM_DataFile.Name='C:\users\public\spns.csv'" -Name Rename -ArgumentList "C:\Users\Public\kerberoasted_users.csv"`.

WMI provides powerful capabilities for both system administration and offensive security operations. It can be used for tasks ranging from monitoring and managing systems to conducting advanced enumeration and lateral movement in security assessments.


### Questions:
- Use WMI to find the serial number of the system.
	- 00329-10280-00000-AA938