**Help Functionality Overview**  
The Command Prompt offers a built-in help function that provides detailed information about the available system commands and how to utilize them. This section covers the following:
- How to use the help function
- Importance of the help function
- External resources for additional help
- Tips and tricks for effective Command Prompt usage


#### How to Get Help
- Typing `help` in the Command Prompt without parameters displays a list of built-in commands, offering basic information about each command's usage.
    Example:
    - **Command:** `help`
    - **Output:** Displays commands like `ASSOC`, `ATTRIB`, and `CHKDSK` with short descriptions.
- For detailed help on a specific command, type `help <command name>`.  
    Example:
    - **Command:** `help time`
    - **Output:** Detailed information on how to use the `time` command.
- Some commands, such as `ipconfig`, do not support the help utility directly but suggest using `/?` for more information.



#### Importance of the Help Utility
- The help utility serves as an **offline manual** for commands on systems where **network access is unavailable**.
- **Scenario Example:** In an internal network engagement with restricted Internet access, the help function becomes crucial for retrieving command syntax.
- The utility bridges the gap for users needing to perform tasks without the ability to quickly search online resources.

#### Additional Help Resources
- **Online Resources:**
    - **Microsoft Documentation:** A comprehensive list of CMD commands with detailed descriptions.
    - **SS64:** A quick reference for command-line tools across platforms (CMD, PowerShell, Bash).
- These resources provide an extended guide when Internet access is available.

![[Screenshot_20240913_095115.png]]

#### Tips & Tricks for Using Command Prompt
- **Clearing the Screen:**
    - Use the command `cls` to clear all previous command outputs and refresh the terminal.
- **Command History:**
    - The Command Prompt stores a history of the commands you've run in a session.
    - Use the up and down arrow keys to navigate through previous commands or `doskey /history` to view all commands from the current session.
    Example:
    - **Command:** `doskey /history`
    - **Output:** A list of commands run, such as `systeminfo`, `cls`, `ipconfig`.
- **Useful Key Shortcuts for Command History:**
    - **F3:** Retypes the last command.
    - **F5:** Cycles through previous commands.
    - **F7:** Opens a list of previous commands.
    - **F9:** Executes a command by its number in history.
- **Exiting a Running Process:**
    - Use `Ctrl + C` to interrupt and stop a running process, especially when a command is stuck or non-responsive.
    Example:
    - **Command:** `ping 8.8.8.8`
    - **Action:** Press `Ctrl + C` to stop the ping process.


## Questions
- If I wanted to view the help documentation for 'ipconfig', what command and/or modifier would I use? (full command string)
	- ipconfig /?
- What CLI equivalent "Help utility" exists on Linux hosts? (one word)
	- man
- Which CMD hotkey will open an interactive list of the previous commands we have ran?
	- F7