### **Interactive Logon**
- **Definition**: An interactive logon is a session initiated when a user logs on directly to a Windows system. This can be done:
    - **Locally**: By physically logging in at the console.
    - **Remotely**: Using Remote Desktop Connection.
    - **Command Line**: Through the `runas` command for running programs with different credentials.

- **Characteristics**:
    - Requires user credentials (username and password).
    - Provides a user interface for interaction.
    - Includes sessions initiated via graphical logon or command-line tools.

### **Non-Interactive Accounts**
- **Definition**: Non-interactive accounts are used by the system to perform tasks without requiring user input or login credentials. They are typically used for running services and scheduled tasks.

#### **Types of Non-Interactive Accounts**
1. **Local System Account**
    - **Description**: Known as `NT AUTHORITY\SYSTEM`, this account is the most powerful in Windows systems.
    - **Privileges**: Has extensive system privileges, more than those of local administrators.
    - **Usage**: Used by the operating system for various system-level tasks and services.
    - **Characteristics**: This account does not have a password and is not designed for interactive logon.

1. **Local Service Account**
    - **Description**: Known as `NT AUTHORITY\LocalService`.
    - **Privileges**: Has limited privileges compared to the Local System account. Provides a restricted environment similar to a local user account.
    - **Usage**: Used to run services with minimal rights.
    - **Characteristics**: This account does not have a password and is used for services that do not require extensive system privileges.

1. **Network Service Account**
    - **Description**: Known as `NT AUTHORITY\NetworkService`.
    - **Privileges**: Similar to a standard domain user account but with limited local privileges. Can interact with network resources.
    - **Usage**: Used for services that need to interact with network resources using the computer's credentials.
    - **Characteristics**: This account also does not have a password and is used for network operations that require authentication.

### **Summary**
- **Interactive Logon**: Requires user credentials and allows direct interaction with the system.
- **Non-Interactive Accounts**:
    - **Local System Account**: Highest privilege level, used for system-level tasks.
    - **Local Service Account**: Restricted privileges, used for running services with limited rights.
    - **Network Service Account**: Similar to a domain user, used for network operations.