### Introduction to CMD.exe
- **CMD.exe** is the default command-line interpreter for Windows.
- Originated from **COMMAND.COM** in DOS.
- Allows direct command execution by the OS.
- Efficient for system tasks with lower resource usage compared to GUI-based programs.
- Still relevant despite the popularity of PowerShell.



### Accessing Command Prompt
- **Local Access**: Direct physical or virtual access to the machine.
  - Methods:
    - `Windows key + R`, then type `cmd`.
    - Navigate to `C:\Windows\System32\cmd.exe`.
- **Remote Access**: Access over a network using virtual peripherals.
  - Protocols: SSH, PsExec, WinRM, RDP (avoid Telnet due to security risks).
  - Essential for sysadmins but poses security risks if misconfigured.



### Basic Usage
- **Navigation**: Similar to moving through directories in a file system.
- **Commands**:
  - `dir`: Lists contents of the current directory.
    - Example output includes file names, sizes, and modification dates.
- **Command Prompt Layout**:
  - Current path location.
  - Issued command.
  - Command output.

### Case Study: Windows Recovery
- **Recovery Mode**: Access Command Prompt via Windows installation disc.
  - Useful for troubleshooting but can be a security risk.
  - Example: Replacing `sethc.exe` with `cmd.exe` to gain SYSTEM privileges.



### Security Implications
- **Legacy Systems**: Older systems may rely heavily on CMD.exe.
- **Privilege Escalation**: Command Prompt can be used to bypass security measures.
- **Best Practices**: Ensure proper configuration of remote access tools and monitor for unauthorized access.



### Next Steps
- Explore built-in help features of CMD.exe for advanced usage and command references.



### Questions
- In what directory can the cmd executable be found? (just the folder name as answer)
	- System32