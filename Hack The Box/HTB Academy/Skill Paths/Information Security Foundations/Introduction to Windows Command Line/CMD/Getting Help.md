### Introduction
- **Help Functionality**: Command Prompt includes a built-in help feature to assist users in understanding and utilizing commands.
- **Purpose**: Provides detailed information about commands, their usage, and syntax.
- **Use Cases**: Essential for environments with limited or no internet access, and for quick reference during tasks.



### Using the Help Functionality
- **Basic Help Command**:
  - Type `help` to list all built-in commands with brief descriptions.
    ```cmd
    C:\htb> help
    ```
    Example Output:
    ```
    ASSOC          Displays or modifies file extension associations.
    ATTRIB         Displays or changes file attributes.
    CD             Displays the name of or changes the current directory.
    CHKDSK         Checks a disk and displays a status report.
    ```
- **Detailed Help for Specific Commands**:
  - Use `help <command>` to get detailed information about a specific command.
    ```cmd
    C:\htb> help time
    ```
    Example Output:
    ```
    Displays or sets the system time.
    TIME [/T | time]
    ```
- **Commands Not Supported by Help**:
  - Some commands (e.g., `ipconfig`) are not supported by the `help` utility.
  - Use `command /?` for detailed information.
    ```cmd
    C:\htb> ipconfig /?
    ```



### Why Use the Help Utility?
- **Offline Resource**: Functions as an offline manual for CMD and DOS-compatible commands.
- **Scenario**: Useful in environments with restricted internet access (e.g., internal networks, firewalls).
- **Comparison**: Similar to Linux `man` pages.



### Additional Resources for Help
- **Online Resources**:
  - **Microsoft Documentation**: Comprehensive list of commands with detailed descriptions.
  - **ss64**: Quick reference for command-line tools (CMD, PowerShell, Bash, etc.).
- **Best Practices**: Use online resources when internet access is available for enhanced learning and troubleshooting.



### Basic Tips & Tricks
1. **Clearing the Screen**:
   - Use `cls` to clear the terminal window.
     ```cmd
     C:\htb> cls
     ```
2. **Command History**:
   - View previously run commands using `doskey /history`.
     ```cmd
     C:\htb> doskey /history
     ```
   - Navigate history using arrow keys, `Page Up`, `Page Down`, or function keys (`F1`-`F9`).
   - **Note**: Command history is session-specific and not persistent.
3. **Interrupting a Running Process**:
   - Use `Ctrl + C` to stop an active process.
     ```cmd
     C:\htb> ping 8.8.8.8
     ^C
     ```



### Key Commands and Shortcuts for Terminal History
| **Key/Command**       | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| `doskey /history`      | Prints the session's command history.                                           |
| `Page Up`              | Places the first command in history to the prompt.                              |
| `Page Down`            | Places the last command in history to the prompt.                               |
| `↑` (Up Arrow)         | Scrolls up through command history.                                             |
| `↓` (Down Arrow)       | Scrolls down through command history.                                           |
| `→` (Right Arrow)      | Types the previous command one character at a time.                             |
| `F3`                   | Retypes the entire previous command.                                            |
| `F5`                   | Cycles through previous commands.                                               |
| `F7`                   | Opens an interactive list of previous commands.                                 |
| `F9`                   | Enters a command based on its number in the history.                            |



### Exiting a Running Process
- **Interrupting Commands**:
  - Use `Ctrl + C` to stop a running process (e.g., `ping`).
    ```cmd
    C:\htb> ping 8.8.8.8
    ^C
    ```
- **Caution**: Interrupting processes may leave them incomplete or unstable.



### Summary
- The `help` utility is a vital offline resource for understanding and using Command Prompt commands.
- Use `help <command>` or `<command> /?` for detailed information.
- Leverage online resources like Microsoft Documentation and ss64 for additional support.
- Master basic tips and tricks like clearing the screen, navigating command history, and interrupting processes to enhance productivity.



### Questions
- If I wanted to view the help documentation for 'ipconfig', what command and/or modifier would I use? (full command string)
	- ipconfig /?
- What CLI equivalent "Help utility" exists on Linux hosts? (one word)
	- man
- Which CMD hotkey will open an interactive list of the previous commands we have ran?
	- F7