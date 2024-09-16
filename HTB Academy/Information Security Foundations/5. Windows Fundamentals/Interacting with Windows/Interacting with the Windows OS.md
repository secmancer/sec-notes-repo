### Graphical User Interface (GUI)
- **Introduction**:
    - The GUI concept was developed in the late 1970s by Xerox Palo Alto Research Laboratory.
    - Added to Apple and Microsoft OS to enhance usability for everyday users who may struggle with command-line interfaces.
    - Provides an interactive point-and-click interface for interacting with the OS and applications.
- **Impact**:
    - Widely increased computer accessibility and appeal.
    - Users interact with their computer without needing to memorize commands or programming languages.
    - Commonly used by system administrators for tasks such as managing Active Directory, configuring IIS, or interacting with databases.


### Remote Desktop Protocol (RDP)
- **Overview**:
    - Proprietary Microsoft protocol for connecting to a remote system over a network and obtaining a GUI.
    - Users connect using RDP client software to a system running RDP server software.
- **Details**:
    - Uses port 3389 for a dedicated network channel.
    - Allows users to access the GUI as if they were physically at the computer.
    - Frequently used by system administrators and for remote work when connected via a VPN.


### Windows Command Line
- **Command-Line Interfaces (CLI)**:
    - Provides greater control for various tasks including administration, troubleshooting, and automation.
    - Main interfaces: Command Prompt (CMD) and PowerShell.
- **Command Prompt (CMD)**:
    - Used for entering and executing commands.
    - Commands examples:
        - `ipconfig`: View IP address information.
        - `schtasks`: Manage scheduled tasks.
        - `help`: Display command help.
    - Commands can be combined with `/` for options (e.g., `ipconfig /?`).

### PowerShell
- **Overview**:
    - Designed for system administrators with a command shell and scripting environment.
    - Built on .NET Framework, offering direct OS interface and scripting capabilities.
- **Cmdlets**:
    - Single-function tools in PowerShell.
    - Format: Verb-Noun (e.g., `Get-ChildItem` to list directory contents).
    - Cmdlets take arguments (e.g., `Get-ChildItem -Recurse`).
- **Aliases**:
    - Shortcuts for cmdlets (e.g., `cd` for `Set-Location`).
    - View aliases with `Get-Alias`.
- **Help System**:
    - Use `Get-Help <cmdlet-name>` for detailed cmdlet information.
    - Update help files with `Update-Help`.
- **Running Scripts**:
    - PowerShell ISE (Integrated Scripting Environment) allows for script creation and debugging.
    - Scripts can be run locally or imported using `Import-Module`.
- **Execution Policy**:
    - Controls script execution to prevent malicious scripts.
    - Policies include:
        - `AllSigned`, `Bypass`, `Default`, `RemoteSigned`, `Restricted`, `Undefined`, `Unrestricted`.
    - Change policy with `Set-ExecutionPolicy` (e.g., `Set-ExecutionPolicy Bypass -Scope Process`).

![[Screenshot_20240912_153630 1.png]]

## Questions
- What is the alias set for the ipconfig.exe command?
	- ifconfig
- Find the Execution Policy set for the LocalMachine scope.
	- unrestricted