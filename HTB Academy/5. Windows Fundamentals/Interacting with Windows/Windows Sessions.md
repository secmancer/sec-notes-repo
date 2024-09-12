#### Interactive Logon
- **Definition**: A session initiated when a user logs into a local or domain system by providing credentials.
- **Methods**:
    - Direct login to the system.
    - Secondary logon session using the `runas` command.
    - Remote Desktop connection.

#### Non-Interactive Logon
- **Definition**: Accounts that do not require login credentials and are used by the operating system to run services and applications automatically.
- **Password**: Non-interactive accounts do not have passwords associated with them.
- **Purpose**: Used to start services at boot or run scheduled tasks without requiring user interaction.

#### Types of Non-Interactive Accounts
1. **Local System Account**
    - **Role**: Provides extensive privileges and is used for system-level tasks.
    - **Access**: Has full access to the local machine and often has more privileges than administrators.
    - **Usage**: Primarily used for system services and internal processes that require high-level access.
2. **Local Service Account**
    - **Role**: A less privileged account compared to the Local System account.
    - **Access**: Provides access to local resources with minimal privileges, typically for services that need limited local access and network access.
    - **Usage**: Often used by services that need access to local resources but do not require elevated permissions.
3. **Network Service Account**
    - **Role**: Similar to the Local Service account but with network access capabilities.
    - **Access**: Provides access to network resources with the same privileges as a standard user account.
    - **Usage**: Used for services that need to interact with network resources but do not need high-level local privileges.


![[Screenshot_20240912_153521 1.png]]
