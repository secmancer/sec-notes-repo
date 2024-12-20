### Graphical User Interface
- **Introduction of GUI:**
    - The concept of a graphical user interface (GUI) was introduced in the late 1970s by Xerox Palo Alto Research Laboratory and later integrated into Apple and Microsoft operating systems to improve usability for everyday users.
    - GUIs allow users to interact with their operating systems and applications through a point-and-click interface, eliminating the need to memorize commands or know programming languages.
- **Widespread Appeal:**
    - The GUI made computers more accessible to a broader demographic, allowing people with no technical knowledge to use them effectively.
    - Systems administrators commonly use GUI-based tools for tasks like administering Active Directory, configuring IIS, and interacting with databases.



### Remote Desktop Protocol (RDP)
- **RDP Overview:**
    - RDP (Remote Desktop Protocol) is a proprietary Microsoft protocol that enables users to connect to a remote system over a network and access its graphical user interface (GUI).
    - The user connects through RDP client software to a target system running RDP server software, typically using port 3389 to establish a dedicated network channel for data transfer.
- **Common Uses:**
    - RDP allows users to interact with a system as if they were sitting directly at it, making it useful for system administrators to manage remote systems.
    - It is also commonly used for remote work, allowing users to access their work computers while traveling or working from home after connecting to a Virtual Private Network (VPN).



### Windows Command Line
- **Command-Line Interfaces (CLI):**
    - CLIs offer users greater control over systems, enabling them to perform a variety of administrative, day-to-day, and troubleshooting tasks.
    - Automation can be introduced through CLIs to speed up tasks, such as bulk user management (e.g., adding many users to a domain).
    - In Windows, users primarily interact with the system via **Command Prompt (CMD)** or **PowerShell**.
- **Windows Command Reference:**
    - The [Windows Command Reference](https://download.microsoft.com/download/5/8/9/58911986-D4AD-4695-BF63-F734CD4DF8F2/ws-commands.pdf) provides a comprehensive guide to Windows commands, including usage examples and syntax, and is recommended for familiarity.



### CMD
- **Command Prompt (cmd.exe):**
    - Used to enter and execute commands in Windows.
    - Supports one-off commands like `ipconfig` to view IP information or more advanced tasks like setting up scheduled tasks and creating scripts/batch files.
    - Can be opened via the Start Menu, by typing `cmd` in the run dialog, or directly from `C:\Windows\system32\cmd.exe`.
    - Typing `help` within Command Prompt will display a list of available commands.
```cmd-session
C:\htb> help
For more information on a specific command, type HELP command-name
ASSOC          Displays or modifies file extension associations.
ATTRIB         Displays or changes file attributes.
BREAK          Sets or clears extended CTRL+C checking.
BCDEDIT        Sets properties in boot database to control boot loading.
CACLS          Displays or modifies access control lists (ACLs) of files.
CALL           Calls one batch program from another.
CD             Displays the name of or changes the current directory.
CHCP           Displays or sets the active code page number.
CHDIR          Displays the name of or changes the current directory.
CHKDSK         Checks a disk and displays a status report.
CHKNTFS        Displays or modifies the checking of disk at boot time.
CLS            Clears the screen.
CMD            Starts a new instance of the Windows command interpreter.
COLOR          Sets the default console foreground and background colors.
COMP           Compares the contents of two files or sets of files.
COMPACT        Displays or alters the compression of files on NTFS partitions.
CONVERT        Converts FAT volumes to NTFS.  You cannot convert the
               current drive.
COPY           Copies one or more files to another location.

<SNIP>
```
- For more information about a specific command, we can type `help <command name>`.
```cmd-session
C:\htb> help schtasks

SCHTASKS /parameter [arguments]

Description:
    Enables an administrator to create, delete, query, change, run and
    end scheduled tasks on a local or remote system.

Parameter List:
    /Create         Creates a new scheduled task.

    /Delete         Deletes the scheduled task(s).

    /Query          Displays all scheduled tasks.

    /Change         Changes the properties of scheduled task.

    /Run            Runs the scheduled task on demand.

    /End            Stops the currently running scheduled task.

    /ShowSid        Shows the security identifier corresponding to a scheduled task name.

    /?              Displays this help message.

Examples:
    SCHTASKS
    SCHTASKS /?
    SCHTASKS /Run /?
    SCHTASKS /End /?
    SCHTASKS /Create /?
    SCHTASKS /Delete /?
    SCHTASKS /Query  /?
    SCHTASKS /Change /?
    SCHTASKS /ShowSid /?
```
- Note that certain commands have their own help menus, which can be accessed by typing `<command> /?`. 
- For example, information about the `ipconfig` command can be seen below.
```cmd-session
C:\htb> ipconfig /?

USAGE:
    ipconfig [/allcompartments] [/? | /all |
                                 /renew [adapter] | /release [adapter] |
                                 /renew6 [adapter] | /release6 [adapter] |
                                 /flushdns | /displaydns | /registerdns |
                                 /showclassid adapter |
                                 /setclassid adapter [classid] |
                                 /showclassid6 adapter |
                                 /setclassid6 adapter [classid] ]

where
    adapter             Connection name
                       (wildcard characters * and ? allowed, see examples)

    Options:
       /?               Display this help message
       /all             Display full configuration information.
       /release         Release the IPv4 address for the specified adapter.
       /release6        Release the IPv6 address for the specified adapter.
       /renew           Renew the IPv4 address for the specified adapter.
       /renew6          Renew the IPv6 address for the specified adapter.
       /flushdns        Purges the DNS Resolver cache.
       /registerdns     Refreshes all DHCP leases and re-registers DNS names
       /displaydns      Display the contents of the DNS Resolver Cache.
       /showclassid     Displays all the dhcp class IDs allowed for adapter.
       /setclassid      Modifies the dhcp class id.
       /showclassid6    Displays all the IPv6 DHCP class IDs allowed for adapter.
       /setclassid6     Modifies the IPv6 DHCP class id.

<SNIP
```



### PowerShell
- **Windows PowerShell:**
    - A command shell designed for system administrators.
    - Provides an interactive command prompt and a powerful scripting environment.
    - Built on the .NET Framework, enabling advanced interaction with the operating system.
    - Gives direct access to the file system, and most commands used in Command Prompt can also be executed in PowerShell.



### Cmdlets
- **PowerShell Cmdlets:**
    - Cmdlets are small, single-function tools built into PowerShell.
    - There are over 100 core cmdlets, with many additional ones available, or users can create their own.
    - Cmdlets follow the `Verb-Noun` format (e.g., `Get-ChildItem`).
    - They can accept arguments or flags to modify behavior. For example:
        - `Get-ChildItem` lists the current directory.
        - `Get-ChildItem -Recurse` lists the current directory and all subdirectories.
        - `Get-ChildItem -Path C:\Users\Administrator\Documents` lists contents of a specific directory.
        - `Get-ChildItem -Path C:\Users\Administrator\Downloads -Recurse` lists all subdirectories' contents recursively within the specified directory.



### Aliases
- Many cmdlets in PowerShell also have aliases. 
- For example, the aliases for the cmdlet `Set-Location`, to change directories, is either `cd` or `sl`. 
- Meanwhile, the aliases for `Get-ChildItem` are `ls` and `gci`. 
- We can view all available aliases by typing `Get-Alias`.
```powershell-session
PS C:\htb> get-alias

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           % -> ForEach-Object
Alias           ? -> Where-Object
Alias           ac -> Add-Content
Alias           asnp -> Add-PSSnapin
Alias           cat -> Get-Content
Alias           cd -> Set-Location
Alias           CFS -> ConvertFrom-String                          3.1.0.0    Microsoft.PowerShell.Utility
Alias           chdir -> Set-Location
Alias           clc -> Clear-Content
Alias           clear -> Clear-Host
Alias           clhy -> Clear-History
Alias           cli -> Clear-Item
Alias           clp -> Clear-ItemProperty
```
- We can also set up our own aliases with `New-Alias` and get the alias for any cmdlet with `Get-Alias -Name`.
```powershell-session
PS C:\htb> New-Alias -Name "Show-Files" Get-ChildItem
PS C:\> Get-Alias -Name "Show-Files"

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           Show-Files
```
- PowerShell has a help system for cmdlets, functions, scripts, and concepts.
- This is not installed by default, but we can either run the `Get-Help <cmdlet-name> -Online` command to open the online help for a cmdlet or function in our web browser. 
- We can type `Update-Help` to download and install help files locally.
```powershell-session
PS C:\htb> help

TOPIC
    Windows PowerShell Help System

SHORT DESCRIPTION
    Displays help about Windows PowerShell cmdlets and concepts.

LONG DESCRIPTION
    Windows PowerShell Help describes Windows PowerShell cmdlets,
    functions, scripts, and modules, and explains concepts, including
    the elements of the Windows PowerShell language.

    Windows PowerShell does not include help files, but you can read the
    help topics online, or use the Update-Help cmdlet to download help files
    to your computer and then use the Get-Help cmdlet to display the help
    topics at the command line.

    You can also use the Update-Help cmdlet to download updated help files
    as they are released so that your local help content is never obsolete.

    Without help files, Get-Help displays auto-generated help for cmdlets,
    functions, and scripts.


  ONLINE HELP
    You can find help for Windows PowerShell online in the TechNet Library
    beginning at http://go.microsoft.com/fwlink/?LinkID=108518.

    To open online help for any cmdlet or function, type:

        Get-Help <cmdlet-name> -Online
		
<SNIP>
```
- Typing a command such as `Get-Help Get-AppPackage` will return just the partial help unless the Help files are installed.
```powershell-session
PS C:\htb>  Get-Help Get-AppPackage

NAME
    Get-AppxPackage

SYNTAX
    Get-AppxPackage [[-Name] <string>] [[-Publisher] <string>] [-AllUsers] [-PackageTypeFilter {None | Main |
    Framework | Resource | Bundle | Xap | Optional | All}] [-User <string>] [-Volume <AppxVolume>]
    [<CommonParameters>]


ALIASES
    Get-AppPackage


REMARKS
    Get-Help cannot find the Help files for this cmdlet on this computer. It is displaying only partial help.
        -- To download and install Help files for the module that includes this cmdlet, use Update-Help.
```



### Running Scripts
- **PowerShell ISE (Integrated Scripting Environment):**
    - The PowerShell ISE is a powerful tool for writing, testing, and debugging PowerShell scripts.
    - It includes features like autocomplete and command lookup, which help users quickly write and correct commands.
    - Users can write scripts and run them within the same console, making it easier to test and debug.
- **Running PowerShell Scripts:**
    - PowerShell scripts can be executed in several ways:
        - **Locally:** By running the script directly in the PowerShell ISE or from the command line.
        - **From memory:** Scripts can be loaded into memory using a download cradle or by invoking a script's functions after it has been loaded.
```powershell-session
PS C:\htb> .\PowerView.ps1;Get-LocalGroup |fl

Description     : Users of Docker Desktop
Name            : docker-users
SID             : S-1-5-21-674899381-4069889467-2080702030-1004
PrincipalSource : Local
ObjectClass     : Group

Description     : VMware User Group
Name            : __vmware__
SID             : S-1-5-21-674899381-4069889467-2080702030-1003
PrincipalSource : Local
ObjectClass     : Group

Description     : Members of this group can remotely query authorization attributes and permissions for resources on
                  this computer.
Name            : Access Control Assistance Operators
SID             : S-1-5-32-579
PrincipalSource : Local
ObjectClass     : Group

Description     : Administrators have complete and unrestricted access to the computer/domain
Name            : Administrators
SID             : S-1-5-32-544
PrincipalSource : Local

<SNIP>
```
- One common way to work with a script in PowerShell is to import it so that all functions are then available within our current PowerShell console session: `Import-Module .\PowerView.ps1`. 
- We can then either start a command and cycle through the options or type `Get-Module` to list all loaded modules and their associated commands.
```powershell-session
PS C:\htb> Get-Module | select Name,ExportedCommands | fl


Name             : Appx
ExportedCommands : {[Add-AppxPackage, Add-AppxPackage], [Add-AppxVolume, Add-AppxVolume], [Dismount-AppxVolume,
                   Dismount-AppxVolume], [Get-AppxDefaultVolume, Get-AppxDefaultVolume]...}

Name             : Microsoft.PowerShell.LocalAccounts
ExportedCommands : {[Add-LocalGroupMember, Add-LocalGroupMember], [Disable-LocalUser, Disable-LocalUser],
                   [Enable-LocalUser, Enable-LocalUser], [Get-LocalGroup, Get-LocalGroup]...}

Name             : Microsoft.PowerShell.Management
ExportedCommands : {[Add-Computer, Add-Computer], [Add-Content, Add-Content], [Checkpoint-Computer,
                   Checkpoint-Computer], [Clear-Content, Clear-Content]...}

Name             : Microsoft.PowerShell.Utility
ExportedCommands : {[Add-Member, Add-Member], [Add-Type, Add-Type], [Clear-Variable, Clear-Variable], [Compare-Object,
                   Compare-Object]...}

Name             : PSReadline
ExportedCommands : {[Get-PSReadLineKeyHandler, Get-PSReadLineKeyHandler], [Get-PSReadLineOption,
                   Get-PSReadLineOption], [Remove-PSReadLineKeyHandler, Remove-PSReadLineKeyHandler],
                   [Set-PSReadLineKeyHandler, Set-PSReadLineKeyHandler]...}
```



### Execution Policy
- Sometimes we will find that we are unable to run scripts on a system.
- This is due to a security feature called the `execution policy`, which attempts to prevent the execution of malicious scripts.
![[Screenshot_20241109_111823.png]]
- Below is an example of the current execution policy for all scopes.
```powershell-session
PS C:\htb> Get-ExecutionPolicy -List

        Scope ExecutionPolicy
        ----- ---------------
MachinePolicy       Undefined
   UserPolicy       Undefined
      Process       Undefined
  CurrentUser       Undefined
 LocalMachine    RemoteSigned
```
- **Execution Policy in PowerShell:**
	- The **execution policy** in PowerShell is a safety feature designed to control the conditions under which scripts can run. However, it is not a strict security control, as users can easily bypass it under certain conditions.
	- Users can bypass the execution policy by:
	    - Typing script contents directly into the PowerShell window.
	    - Downloading and executing the script.
	    - Encoding the script as a command.
	    - Modifying the execution policy (if the user has the appropriate rights).
	    - Setting the execution policy for the current session without affecting the system-wide policy.
- To change the execution policy for the current session, you can use the following commands to do that below.
```powershell-session
PS C:\htb> Set-ExecutionPolicy Bypass -Scope Process

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```
- We can now see that the execution policy has been changed.
```powershell-session
PS C:\htb>  Get-ExecutionPolicy -List

        Scope ExecutionPolicy
        ----- ---------------
MachinePolicy       Undefined
   UserPolicy       Undefined
      Process          Bypass
  CurrentUser       Undefined
 LocalMachine    RemoteSigned
```



### Questions
 - What is the alias set for the ipconfig.exe command?
	 - ifconfig
- Find the Execution Policy set for the LocalMachine scope.
	- unrestricted