**Command Prompt** (cmd.exe) is the default command-line interpreter for Windows, originating from the DOS-based **COMMAND.COM**.
- It allows users to input commands directly, enabling tasks like password changes and network status checks with minimal system resources compared to GUI-based programs.
- While often overshadowed by **PowerShell**, cmd.exe is still valuable for tasks, particularly when PowerShell is restricted or unavailable (e.g., through AppLocker).

### Importance in Pentesting
- **CMD.exe** remains useful in environments where PowerShell is disabled or locked down.
- Legacy software still exists in modern operating systems, and **knowing cmd.exe** helps navigate these systems for tasks such as **privilege escalation**.


### Accessing CMD
- There are two primary types of access:
    1. **Local Access**: Direct physical or virtual (e.g., VM) access without needing a network connection.
        - Methods to access CMD locally:
            - `Windows Key + R`, then type `cmd`
            - Navigate to `C:\Windows\System32\cmd.exe`
    2. **Remote Access**: Access via network using tools like **SSH**, **PsExec**, **WinRM**, or **RDP**.


### Local Access Example
- Open **cmd.exe** locally using `Windows + R` or direct path navigation.
- Once opened, it displays a prompt like:
```
Microsoft Windows [Version 10.0.19044.2006]
(c) Microsoft Corporation. All rights reserved.

C:\Users\htb>
```
- Commands can now be entered directly into the shell.


### Remote Access Example
- **Remote access** uses virtual peripherals to control a machine over a network. Tools include:
    - **SSH** (preferred for security)
    - **Telnet** (insecure and deprecated)
    - **PsExec**
    - **WinRM**
    - **RDP**
- Remote access can pose security risks if improperly configured, potentially exposing the environment to attackers if credentials are compromised.


### Basic Navigation in CMD
- **CMD.exe** has remained consistent over the decades in its navigation style.
- Navigation in CMD is akin to walking through directories:
    - **dir**: Lists files and directories in the current folder.
    - **cd**: Changes the directory.


**Example of the `dir` Command**
```
C:\Users\htb\Desktop> dir

Volume in drive C has no label.
Volume Serial Number is DAE9-5896

Directory of C:\Users\htb\Desktop

06/11/2021  11:59 PM    <DIR>          .
06/11/2021  11:59 PM    <DIR>          ..
06/11/2021  11:57 PM                 0 file1.txt
06/11/2021  11:57 PM                 0 file2.txt
06/11/2021  11:57 PM                 0 file3.txt
```


### Windows Recovery Mode Case Study
- In recovery situations (e.g., user lockout), the **Command Prompt** can be accessed via **Recovery Mode** after booting from a Windows installation disc.
- **Security concern**: The cmd.exe binary can replace **Sticky Keys** (`sethc.exe`) to gain unauthorized access with **SYSTEM** privileges by pressing Shift 5 times at the login screen.


## Questions
- In what directory can the cmd executable be found? (just the folder name as answer)
	- System32