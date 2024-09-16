**Purpose**: Understand environment variables, their uses, and how to manage them in Windows. Explore the concepts of variable scope and the different scopes of environment variables in Windows.

**What is an Environment Variable?**
- **Definition**: Environment variables are settings that are applied globally and are used by the operating system and applications to reference data and run scripts. They are not case-sensitive and can include spaces and numbers in their names, but cannot start with a number or include an equal sign.
- **Format**: Referenced in Windows using `%VARIABLE_NAME%`, e.g., `%SUPER_IMPORTANT_VARIABLE%`.
- **Common Usage**: Environment variables speed up application functions and script execution by providing a standardized way to reference system and user data.


**Variable Scope**
- **Global Scope**: Variables that are accessible from anywhere within the system or application. Example: `%WINDIR%` which shows the Windows directory for any user.
- **Local Scope**: Variables that are only accessible within a specific context or session. Example: A user-defined variable that is not visible to other users.
    - **Example**:
        - **Global Variable**:
            
            - Command for User Alice and Bob:
                - `echo %WINDIR%`
            - Output:
                - `C:\Windows` (Both users see the same result because `%WINDIR%` is a global variable.)
        - **Local Variable**:
            
            - **Alice**:
                - Command: `set SECRET=HTB{5UP3r_53Cr37_V4r14813}`
                - Command: `echo %SECRET%`
                - Output: `HTB{5UP3r_53Cr37_V4r14813}`
            - **Bob**:
                - Command: `echo %SECRET%`
                - Output: `%SECRET%` or `Environment variable %SECRET% not defined` (Bob cannot see Alice's local variable.)


**Types of Environment Variable Scopes in Windows**
- **System Scope**: Variables that are defined for the entire system and are available to all users and processes. Examples include `%SYSTEMROOT%`, `%PATH%`.
- **User Scope**: Variables that are specific to a particular user and are only available in their context. Examples include `%USERPROFILE%`, `%TEMP%`.
- **Process Scope**: Variables that are defined for the duration of a process. These variables are temporary and exist only while the process is running. They are considered a sub-scope of both System and User scopes.


**Managing Environment Variables in Windows**
- **Viewing Environment Variables**:
    - **Command Prompt**: Use `set` to display all environment variables.
    - **Specific Variable**: Use `echo %VARIABLE_NAME%` to view the value of a specific variable.
- **Setting Environment Variables**:
    - **Command Prompt**: Use `set VARIABLE_NAME=value` to create or modify a local environment variable.
    - **System Properties**:
        - Access via Control Panel > System and Security > System > Advanced system settings > Environment Variables.
        - Here, you can add, edit, or delete system and user environment variables.
- **Temporary Variables**:
    - Created and used within a single command session and lost after the session ends.

![[Screenshot_20240915_195842.png]]



**Viewing Environment Variables**
- **Using `set`**:
    - **Command**: `set` (prints all environment variables in the current session)
    - **Example**:
        - `C:\Users\htb\Desktop> set %SYSTEMROOT%`
        - Output: `Environment variable C:\Windows not defined` (This happens because `%SYSTEMROOT%` is not being set here, just referenced.)


**Using `echo`**:
- **Command**: `echo %VARIABLE_NAME%` (prints the value of a specific environment variable)
- **Example**:
    - `C:\Users\htb> echo %PATH%`
    - Output: Displays the current value of `%PATH%`


**Managing Environment Variables**
- **Commands**: `set` vs. `setx`
    - **`set`**:
        - **Scope**: Temporary, only for the current command line session.
        - **Usage**: Modify variables temporarily.
        - **Example**:
            - `C:\htb> set DCIP=172.16.5.2`
            - **Validation**: `C:\htb> echo %DCIP%` shows the value `172.16.5.2`
            - **Note**: Variable will disappear after the session ends.


**`setx`**:
- **Scope**: Permanent, changes are saved in the registry and available in new command prompt sessions.
- **Usage**: Create, edit, or delete environment variables permanently.
- **Example for Creation**:
    - `C:\htb> setx DCIP 172.16.5.2`
    - Output: `SUCCESS: Specified value was saved.`
- **Example for Editing**:
    - `C:\htb> setx DCIP 172.16.5.5`
    - Output: `SUCCESS: Specified value was saved.`
- **Validation**: `C:\htb> echo %DCIP%` shows the new value `172.16.5.5`
- **Note**: Changes take effect in new command prompt sessions or after logon.


**Creating Environment Variables**
- **Using `set`**:
    - **Command**: `set VARIABLE_NAME=value`
    - **Example**:
        - `C:\htb> set DCIP=172.16.5.2`
        - **Validation**: `C:\htb> echo %DCIP%` shows the value `172.16.5.2`
- **Using `setx`**:
    - **Command**: `setx VARIABLE_NAME value`
    - **Example**:
        - `C:\htb> setx DCIP 172.16.5.2`
        - Output: `SUCCESS: Specified value was saved.`


**Editing Environment Variables**
- **Using `setx`**:
    - **Command**: `setx VARIABLE_NAME new_value`
    - **Example**:
        - `C:\htb> setx DCIP 172.16.5.5`
        - Output: `SUCCESS: Specified value was saved.`
        - **Validation**: `C:\htb> echo %DCIP%` shows the updated value `172.16.5.5`


**Removing Environment Variables**
- **Using `setx`**:
    - **Command**: `setx VARIABLE_NAME ""` (Clears the value of the variable, effectively removing it.)
    - **Example**:
        - `C:\htb> setx DCIP ""`
        - Output: `SUCCESS: Specified value was saved.`
        - **Verification**:
            - `C:\htb> set DCIP` shows `Environment variable DCIP not defined`
            - `C:\htb> echo %DCIP%` shows `%DCIP%` (Variable no longer defined.)


**Importance of Environment Variables in Enumeration**
- **Security Implications**: Environment variables can reveal sensitive information about the system and user accounts in clear text. As an attacker, enumerating these variables can provide valuable insights into the target environment.


**Key Environment Variables to Be Aware Of**
- **`PATH`**:
    - **Description**: Lists directories where executable programs are located.
    - **Usage**: Reveals paths where executables are searched, which may include sensitive or non-standard directories.
    - **Command**: `echo %PATH%`
- **`SYSTEMROOT`**:
    - **Description**: Indicates the directory where the Windows operating system is installed.
    - **Usage**: Can be used to locate system files and directories.
    - **Command**: `echo %SYSTEMROOT%`
- **`TEMP` and `TMP`**:
    - **Description**: Directories used for temporary files.
    - **Usage**: May contain temporary files or executables that could be useful.
    - **Command**: `echo %TEMP%` and `echo %TMP%`
- **`USERPROFILE`**:
    - **Description**: Path to the current user's profile directory.
    - **Usage**: Provides information about the user's home directory and potentially sensitive files.
    - **Command**: `echo %USERPROFILE%`
- **`USERNAME`**:
    - **Description**: Name of the currently logged-in user.
    - **Usage**: Useful for identifying the user context and potentially targeting user-specific files.
    - **Command**: `echo %USERNAME%`
- **`COMPUTERNAME`**:
    - **Description**: Name of the computer.
    - **Usage**: Helps identify the machine, which can be useful for network enumeration and mapping.
    - **Command**: `echo %COMPUTERNAME%`
- **`HOMEDRIVE` and `HOMEPATH`**:
    - **Description**: Drive and path to the current user's home directory.
    - **Usage**: Provides additional information about the user’s home directory location.
    - **Command**: `echo %HOMEDRIVE%` and `echo %HOMEPATH%`
- **`PROGRAMFILES` and `PROGRAMFILES(x86)`**:
    - **Description**: Directories where applications are installed.
    - **Usage**: Can reveal the installation directories of applications, which might include sensitive applications or misconfigured ones.
    - **Command**: `echo %PROGRAMFILES%` and `echo %PROGRAMFILES(x86)%`


**Practical Use Cases for Enumeration**
- **Identifying System Configuration**: By examining these variables, attackers can gather information about the system configuration, software installations, and user profiles.
- **Locating Sensitive Files**: Variables such as `TEMP`, `USERPROFILE`, and `PROGRAMFILES` can lead to directories containing sensitive files or configuration details.
- **Mapping the Environment**: Variables like `COMPUTERNAME`, `PATH`, and `SYSTEMROOT` help in understanding the network and system layout, which can be useful for further exploitation.


**Caution**
- **Security**: Since environment variables are accessible in clear text, they should be carefully managed to avoid exposing sensitive information.
- **Ethical Considerations**: Always ensure that enumeration and information gathering are performed within the bounds of legal and ethical guidelines.


![[Screenshot_20240915_195856.png]]

**Overview of Environment Variables**
- **Scope**: We’ve explored how environment variables function and their significance in enumeration on a Windows system.
- **Key Variables**: Variables such as `PATH`, `SYSTEMROOT`, `TEMP`, `USERPROFILE`, `USERNAME`, `COMPUTERNAME`, `HOMEDRIVE`, `HOMEPATH`, `PROGRAMFILES`, and `PROGRAMFILES(x86)` provide critical information about the system and user environment.


**Additional Information**
- **Complete List**: The information provided is just a fraction of what can be learned from environment variables. For a comprehensive list, refer to the detailed resources available online.
- **Guidance**: Use the provided variables as a starting point for enumeration to gain insights into the host and target environment.


**Best Practices**
- **Modifications**: When dealing with system-wide environment variables, proceed with caution. Always create new variables rather than modifying existing ones unless necessary.
- **Scripts and Tools**: If modifications are required for scripts or tools, ensure they are done thoughtfully to avoid unintended system impacts.


**Moving Forward**
- **Next Topic**: Transition to working with services on the host using the command line. This will involve learning about service management and interactions to further understand and control the system environment.


## Questions
- What variable scope allows for universal access?
	- Global