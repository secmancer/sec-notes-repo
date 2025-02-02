### **What Are Environment Variables?**
- **Definition**: Key-value pairs used by the system and applications for configuration.
- **Scope**: Available across different users and processes.
- **Format**: Usually written in uppercase with underscores:
    ```cmd
    %EXAMPLE_VARIABLE%
    ```
- **Usage**: Referenced by applications, scripts, and commands.



### **Variable Scope**
1. **Global**:
    - Accessible by all users and applications.
    - Example:
        ```cmd
        C:\Users\alice> echo %WINDIR%
        C:\Windows
        ```
2. **Local**:
    - Exists only within the current session or process.
    - Example:
        ```cmd
        C:\Users\alice> set SECRET=HTB{SECRET_VALUE}
        C:\Users\alice> echo %SECRET%
        HTB{SECRET_VALUE}
        
        C:\Users\bob> echo %SECRET%
        %SECRET%  (Not accessible)
        ```



### **Types of Environment Variable Scopes**

|**Scope**|**Description**|**Permissions**|**Storage Location**|
|---|---|---|---|
|**System**|OS-defined, accessible by all users.|Admin required|`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment`|
|**User**|Defined per user, not accessible by others.|Current user/Admin|`HKEY_CURRENT_USER\Environment`|
|**Process**|Temporary, exists only in the running process.|Current process|Stored in memory|



### **Viewing Environment Variables**
1. **Using `set`** (Displays all variables)
    ```cmd
    C:\Users\htb\Desktop> set
    ```
2. **Using `echo`** (Displays a specific variable)
    ```cmd
    C:\Users\htb\> echo %PATH%
    ```



### **Managing Environment Variables**
- ##### **Creating Variables**
	1. **Using `set`** (Temporary)
    ```cmd
    C:\htb> set DCIP=172.16.5.2
    C:\htb> echo %DCIP%
    172.16.5.2
    ```
	2. **Using `setx`** (Permanent)
    ```cmd
    C:\htb> setx DCIP 172.16.5.2
    SUCCESS: Specified value was saved.
    ```
- ##### **Editing Variables**
```cmd
C:\htb> setx DCIP 172.16.5.5
SUCCESS: Specified value was saved.
```
- ##### **Removing Variables**
```cmd
C:\htb> setx DCIP ""
SUCCESS: Specified value was saved.

C:\htb> echo %DCIP%
%DCIP%  (No value assigned)
```



### **Important Environment Variables**

| **Variable**          | **Description**                                                       |
| --------------------- | --------------------------------------------------------------------- |
| `%PATH%`              | Directories where executables are located.                            |
| `%OS%`                | Current operating system name.                                        |
| `%SYSTEMROOT%`        | Expands to `C:\Windows`, contains system files.                       |
| `%LOGONSERVER%`       | Shows the login server of the user.                                   |
| `%USERPROFILE%`       | Location of the active user's home directory (`C:\Users\{username}`). |
| `%ProgramFiles%`      | Path to installed x64 programs (`C:\Program Files`).                  |
| `%ProgramFiles(x86)%` | Path to installed x86 (32-bit) programs (`C:\Program Files (x86)`).   |



### **Key Takeaways**
- **Global variables** apply to all users; **local variables** are user-specific.
- **Process scope variables** are temporary and exist only in a session.
- `set` modifies variables **temporarily**, while `setx` makes **permanent** changes.
- Environment variables store **system-critical** data and should be handled carefully.
- Attackers can use these variables for **information gathering**, while defenders must secure them.



### Questions
- What command string will stop a service named 'red-light'? (full command as the answer)
	- sc stop red-light
- What Windows executable will allow us to create, query, and modify services on a host?
	- sc