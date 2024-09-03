### What Are Environment Variables?

- **Definition**: Environment variables are dynamic values that affect how processes and applications operate. They store configuration settings and system information used by various programs and scripts.
- **Usage**: These variables define system paths, application settings, and user preferences.

### Scope of Environment Variables

- **Global Scope**: These variables are accessible across the entire system and can be used by all users. Examples include `%SYSTEMROOT%` and `%PATH%`.
- **Local Scope**: These variables are specific to the current user or process and are not visible to other users or processes unless explicitly shared.

### Scope Types in Windows

1. **System (Machine) Scope**:
    
    - **Description**: Variables set for all users on the computer.
    - **Permissions**: Requires Local Administrator or Domain Administrator rights.
    - **Registry Location**: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment`
2. **User Scope**:
    
    - **Description**: Variables specific to the current user session.
    - **Permissions**: Accessible by the current user, Local Administrator, or Domain Administrator.
    - **Registry Location**: `HKEY_CURRENT_USER\Environment`
3. **Process Scope**:
    
    - **Description**: Variables that exist only during the life of the process that created them.
    - **Permissions**: Inherited from System/User scopes, only accessible within the process.
    - **Registry Location**: Not stored in the registry; managed in process memory.

### Viewing Environment Variables

- **Using `set`**: Lists all environment variables or a specific one if you provide its name.
- **Using `echo`**: Shows the value of a specific environment variable.

### Managing Environment Variables

- **Using `set`**: Makes temporary changes that only last for the current session.
- **Using `setx`**: Makes permanent changes saved in the registry and applied to new sessions.
- **Removing Variables**: You can clear a variable's value using `setx` to effectively remove it.

### Important Environment Variables

- **%PATH%**: Specifies directories where executable files are located.
- **%OS%**: Indicates the operating system version.
- **%SYSTEMROOT%**: Refers to the Windows system folder, typically `C:\Windows`.
- **%LOGONSERVER%**: Shows the login server for the current user.
- **%USERPROFILE%**: Points to the current user's home directory.
- **%ProgramFiles%**: Path where installed programs are located (`C:\Program Files`).
- **%ProgramFiles(x86)%**: Path where 32-bit programs are installed on 64-bit systems (`C:\Program Files (x86)`).


### Questions
- What variable scope allows for universal access?
	- Global