### **Windows Services**

- **Definition**: Services are long-running processes that can start automatically at system boot and continue running in the background.
- **Purpose**: They handle various system functions, such as networking, diagnostics, and user management.
- **Management**: Services are managed via the Service Control Manager (SCM), accessible through `services.msc`.

### **Examining Services**
1. **Using `services.msc`**:
    - **Details**: Displays the service name, description, status, startup type, and user account.
    - **Log On Tab**: Shows the account under which the service runs, which can be crucial for understanding potential privilege issues.

1. **Using `sc` Command**:
    - **Query Service Configuration**: sc qc [ServiceName]
	- **Change Service Configuration**: sc config [ServiceName] binPath= [NewPath]
	- **Show Security Descriptor**: sc sdshow [ServiceName]
	- **Example**: Querying `wuauserv` (Windows Update service):
		- sc qc wuauserv
		- sc sdshow wuauserv

1. **Using PowerShell**:
	- **Get ACL**:
		- Get-Acl -Path HKLM:\System\CurrentControlSet\Services\[ServiceName] | Format-List
	- **Example**:
		- Get-Acl -Path HKLM:\System\CurrentControlSet\Services\wuauserv | Format-List

### **Service Permissions**
- **Default Service Accounts**:
    - **LocalService**: Minimal permissions on the local machine.
    - **NetworkService**: Limited permissions, used for network-related tasks.
    - **LocalSystem**: High privileges, often used by critical services.

- **Security Risks**:
    - **Misconfigurations**: Weak permissions can lead to privilege escalation or unauthorized access.
    - **Service Accounts**: Best practice to use dedicated accounts for services to minimize impact from account changes.


### **Tools**
- **Sysinternals Suite**:
    - **Process Explorer**: Enhanced Task Manager for detailed process information.
    - **Process Monitor**: Monitors file system, registry, and network activity.
    - **ProcDump**: Captures process dumps based on specific criteria.

- **Task Manager**:
    - **Tabs**:
        - **Processes**: Lists applications and background processes.
        - **Performance**: Displays system performance metrics.
        - **Startup**: Manages applications configured to start at boot.
        - **Services**: Lists and manages services.


### **Best Practices**
1. **Principle of Least Privilege**:
    - Run services with the least privileges necessary. Avoid using LocalSystem unless absolutely necessary.

1. **Service Accounts**:
    - Use dedicated service accounts for critical services to avoid issues related to account changes or deletions.

1. **Regular Audits**:
    - Periodically review service configurations and permissions to ensure they align with security policies.

1. **Automation**:
    - Use scripting with `sc` or PowerShell to manage services and permissions, especially in large environments.