### Key Concepts:

- **Services**: These are background processes that handle various functions on a Windows operating system, such as managing applications, network connections, and system security.
- **PowerShell Cmdlets for Services**:
    - **Get-Service**: Retrieves the status of services.
    - **Start-Service**: Starts a stopped service.
    - **Stop-Service**: Stops a running service.
    - **Set-Service**: Modifies the properties of a service, such as its startup type.

### Practical Application:

1. **Identifying Issues**: Use `Get-Service` to list services and identify any that are not running as expected, such as those related to security (e.g., Windows Defender).
2. **Filtering Output**: Narrow down the list of services to specific ones of interest using the `Where-Object` cmdlet.
3. **Managing Services**: Start or stop services based on the troubleshooting requirements, ensuring that critical services are operational.
4. **Remote Management**: Use `Invoke-Command` or `-ComputerName` to manage services on remote hosts, enabling you to maintain multiple systems efficiently.

### Scenario Recap:

In the given scenario, the administrator needs to address potential security issues on Mr. Tanaka's host by checking and managing Windows Defender services. By using PowerShell, the admin can quickly identify and restart the necessary services, ensuring the system is protected. The scenario also highlights the importance of investigating unusual service names, which could indicate tampering or security threats.

### Questions
- What Cmdlet will show us the current services of a host?
	- Get-Service
- If we wanted to start the Windows Defender Service, what command would we use?
	- Start-Service WinDefend
- What Cmdlet will allow us to execute a command on a remote host?
	- Invoke-Command