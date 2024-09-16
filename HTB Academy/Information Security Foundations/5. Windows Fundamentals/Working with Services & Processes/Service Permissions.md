#### Importance of Service Permissions
- **Services**: Critical components for managing long-running processes in Windows OS.
- **Threat Vectors**: Misconfigured service permissions can be exploited to:
    - Load malicious DLLs
    - Execute applications without admin rights
    - Escalate privileges
    - Maintain persistence


#### Common Issues
- **Misconfigurations**: Often caused by third-party software or admin errors during installation.
- **Impact**: Misconfigurations can lead to service failures, downtime, and productivity loss.
- **Example**: DHCP service failure due to misconfigured service account if the original user (e.g., Bob) leaves the organization.


#### Best Practices
- **Service Accounts**: Use dedicated service accounts instead of using personal admin accounts for running critical network services.
- **Principle of Least Privilege**: Ensure services run with the least amount of privileges necessary.



#### Key Built-in Service Accounts
- **LocalService**
- **NetworkService**
- **LocalSystem**


#### Service Management Tools
- **services.msc**:
    - View and manage service details
    - Important properties: Path to executable, Log On credentials, Recovery options
- **sc Command**:
    - **Query Service Configuration**: `sc qc <service_name>`
        - Example: `sc qc wuauserv`
    - **Start/Stop Services**: `sc start <service_name>`, `sc stop <service_name>`
    - **Change Configuration**: `sc config <service_name> binPath= <path_to_executable>`
        - Example: `sc config wuauserv binPath=C:\Winbows\Perfectlylegitprogram.exe`
    - **Display Security Descriptor**: `sc sdshow <service_name>`
        - Example: `sc sdshow wuauserv`
- **PowerShell**:
    - **Get Service ACL**: `Get-Acl -Path HKLM:\System\CurrentControlSet\Services\<service_name> | Format-List`
        - Example: `Get-Acl -Path HKLM:\System\CurrentControlSet\Services\wuauserv | Format-List`
    - **Security Descriptor Definition Language (SDDL)**:
        - Describes permissions in a formatted string.


#### Example Analysis of Security Descriptors
- **SDDL Components**:
    - **DACL** (Discretionary Access Control List): Defines permissions for users/groups.
    - **SACL** (System Access Control List): Logs access attempts.
    - **Format**:
        - `D: (A;;CCLCSWRPLORC;;;AU)`:
            - `D:` - DACL permissions
            - `AU` - Authenticated Users
            - `A;;` - Access is Allowed
            - `CC` - SERVICE_QUERY_CONFIG permission, etc.