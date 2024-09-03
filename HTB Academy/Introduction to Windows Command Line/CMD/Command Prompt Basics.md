
**1. Overview of cmd.exe**
- **What is cmd.exe?**
    - The Command Prompt, known as cmd.exe or CMD, is the default command-line interpreter for Windows.
    - Based on the COMMAND.COM interpreter from DOS, it's present across nearly all Windows OS.
    - It allows users to input commands that are interpreted and executed by the OS, performing tasks like changing passwords or checking network status.
    - Unlike graphical-based programs, CMD is resource-efficient, requiring less CPU and memory.
- **Importance of cmd.exe**
    - Despite the rise of PowerShell, cmd.exe remains valuable, especially in scenarios where PowerShell is restricted or inaccessible.
- **Quick Story (Pentesting Scenario)**
    - During pentests, cmd.exe can be crucial when PowerShell is locked down. It can be used to gain further access and elevate privileges, demonstrating the importance of understanding legacy tools in modern environments.

**2. Accessing cmd.exe**
- **How to Access Command Prompt**
    - There are multiple methods to access cmd.exe, depending on your situation:
        - **Local Access:** Direct physical or virtual (e.g., Virtual Machine) access to the machine.
            - Methods to open cmd.exe locally:
                - **Windows Key + r:** Opens the run prompt, type `cmd` to access.
                - **File Explorer:** Navigate to `C:\Windows\System32\cmd.exe` to execute.
        - **Remote Access:** Accessing the machine via network, using tools like Telnet, SSH, PsExec, WinRM, or RDP.
            - **Scenario Example:**
                - If you're a system administrator managing machines across different regions, determining the best way to access the machine depends on factors like the user's location and network connectivity.

**3. Local vs. Remote Access**
- **Local Access:**
    - Direct interaction with the machine’s peripherals, no network required.
    - Useful for troubleshooting on-site.
- **Remote Access:**
    - Interacting with the machine over the network using virtual peripherals.
    - Offers convenience for sysadmins but poses security risks if not properly managed.

**4. Command Prompt Basics**
- **Navigating the Command Prompt**
    - The structure of CMD has remained consistent over the years.
    - Navigating the file system is like walking through hallways (directories) and rooms (files).
    - **Basic Command:** `dir`
        - Lists files and directories in the current directory.
        - Output includes details like file size and creation date.
- **Case Study: Windows Recovery**
    - **Scenario:**
        - In cases of user lockout or technical issues, you can access CMD via Windows Recovery Mode.
        - This can be done by booting from a Windows installation disc and choosing Repair Mode.
    - **Potential Risk:**
        - CMD in recovery mode can be misused to tamper with the filesystem, such as replacing the Sticky Keys executable with cmd.exe to gain unauthorized access.

**5. Next Steps**
- **Utilizing Built-In Help Features**
    - After gaining a basic understanding of cmd.exe, the next step is learning how to use its built-in help features for more advanced command-line tasks.


### Questions
- In what directory can the cmd executable be found? (just the folder name as answer)
	- System32