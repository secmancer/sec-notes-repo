### **Graphical User Interface (GUI)**
- **Introduction**: The GUI concept was introduced in the late 1970s by Xerox PARC and was later adopted by Apple and Microsoft to make operating systems more user-friendly.
- **Purpose**: Designed to address usability concerns by providing a point-and-click interface, allowing users to interact with the system without needing to know command-line instructions.
- **Impact**: Enabled broader access to computers by non-technical users, making computing more accessible and intuitive.

### **Remote Desktop Protocol (RDP)**
- **Definition**: A proprietary Microsoft protocol that allows users to connect to remote systems and access their graphical user interface over a network.
- **Port**: Uses port 3389.
- **Usage**: Commonly used by system administrators for remote management and by users to access work computers from different locations (e.g., from home or while traveling).
- **Connection**: Users connect via RDP client software to a server running RDP software, experiencing the remote system's GUI as if they were physically present.

### **Windows Command Line Interfaces**
#### **Command Prompt (CMD)**
- **Overview**: A command-line interface used for running commands and scripts in Windows.
- **Common Commands**:
    - `ipconfig`: Displays IP configuration.
    - `schtasks`: Manages scheduled tasks.
    - `help <command>`: Displays help for a specific command.
- **Usage**: Can be used to execute single commands, create scripts, and perform administrative tasks.

#### **PowerShell**
- **Overview**: A command shell and scripting language built on the .NET Framework, designed for system administrators.
- **Cmdlets**: Small, single-function tools in PowerShell that follow the Verb-Noun format (e.g., `Get-ChildItem`).
- **Aliases**: Shortcuts for cmdlets (e.g., `cd` for `Set-Location`).
- **Help System**:
    - Use `Get-Help <cmdlet>` for cmdlet documentation.
    - `Update-Help` downloads and installs help files.
    - `Get-Help <cmdlet> -Online` opens online help in a web browser.
- **Execution Policy**:
    - **AllSigned**: Requires all scripts to be signed by a trusted publisher.
    - **Bypass**: No restrictions, no warnings.
    - **Default**: `Restricted` for desktop, `RemoteSigned` for servers.
    - **RemoteSigned**: Requires a digital signature for internet-downloaded scripts.
    - **Restricted**: Only individual commands are allowed, scripts are blocked.
    - **Undefined**: No specific policy set for the current scope.
    - **Unrestricted**: Allows all scripts but warns before running unsigned ones.
- **Changing Execution Policy**: Can be modified using `Set-ExecutionPolicy`. For example, `Set-ExecutionPolicy Bypass -Scope Process` changes the policy for the current session.

### **Examples**
- **Using CMD**:
    - To view all available commands: `help`
    - To get specific help for a command like `schtasks`: `help schtasks`
    - To get help for `ipconfig`: `ipconfig /?`

- **Using PowerShell**:
    - List all aliases: `Get-Alias`
    - Define a new alias: `New-Alias -Name "Show-Files" Get-ChildItem`
    - Get help for a cmdlet: `Get-Help Get-AppxPackage`


### Questions:
- What is the alias set for the ipconfig.exe command?
	- ifconfig
- Find the Execution Policy set for the LocalMachine scope.
	- unrestricted