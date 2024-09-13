### CMD vs PowerShell Overview
- **CMD.exe** and **PowerShell** are both built-in command-line interfaces on Windows.
- Both offer control over the OS, automation of tasks, and management of applications.
- **CMD.exe** has been available since 1981, while **PowerShell** was introduced in 2006 and is more powerful.

### Penetration Testing Perspective
- Learning to use **Windows tools**, commands, and third-party applications for tasks like:
    - **Reconnaissance**
    - **Exploitation**
    - **Exfiltration**
- This module is designed to build knowledge for administering Windows hosts via the command line and prepare for more advanced **HTB Academy** modules.

![[Screenshot_20240913_094348.png]]

### Key Differences: PowerShell vs Command Prompt

|Feature|PowerShell|Command Prompt|
|---|---|---|
|**Year Introduced**|2006|1981|
|**Command Compatibility**|Runs batch commands + cmdlets|Runs batch commands only|
|**Command Aliases**|Supported|Not supported|
|**Output Type**|Objects|Text|
|**Piping Support**|Cmdlet output can be piped|Command output cannot be piped|
|**Execution**|Supports sequential cmdlets|Commands run sequentially|
|**Integrated Scripting Environment**|Available (ISE)|Not available|
|**Programming Libraries**|Access to .NET libraries|No access|
|**Cross-platform Availability**|Available on Linux|Windows only|

- PowerShell is a **scripting language** with rich features, whereas **Command Prompt** is limited to basic batch commands and text-based outputs.

### Scenario for the Module
- You are a system administrator aiming to learn **penetration testing** and deepen your understanding of **PowerShell** and **CMD**.
- Your goal is to gain the skills to impress your **Internal Red Team Lead** and become a **Command Line Ninja**.

### Connection Instructions
- To complete lab exercises, you'll connect to several Windows hosts using **SSH**.
- Use the following format to connect:
    - `ssh htb-student@<IP-Address>`
- After logging in with your password, you can begin exploring the tasks via CLI.
