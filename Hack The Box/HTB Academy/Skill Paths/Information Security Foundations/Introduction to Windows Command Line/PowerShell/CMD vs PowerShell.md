### **Overview**
- CMD (`cmd.exe`) is the traditional Windows command-line interpreter.
- PowerShell is the modern successor, offering more flexibility and functionality.
- PowerShell is also a **scripting language**, unlike CMD.



### **Differences Between CMD and PowerShell**

|Feature|CMD|PowerShell|
|---|---|---|
|**Language**|Batch and basic CMD commands only|Supports Batch, CMD, PowerShell cmdlets, and aliases|
|**Command Chaining**|Cannot pass output between commands|Can pass command output as an object|
|**Output Format**|Text only|Objects (structured data)|
|**Execution Model**|Commands execute sequentially|Can run multiple commands in parallel|

- PowerShell integrates **extensively** with Windows systems and **supports Linux**.
- It is built on the `.NET framework` and **uses an object-based model** rather than text-based output.



### **Why Choose PowerShell Over CMD?**
- **For IT Administrators**:
    - Automates **server provisioning, AD user management, file permissions, Azure interactions, and email setup**.
    - Supports **cloud-based** (Microsoft 365, Azure) and **on-premises** environments.
- **For Infosec (Pentesting & SOC Analysts)**:
    - Allows for **importing modules/tools** for penetration testing.
    - **Logging capabilities** can expose attack activity (less stealthy than CMD).



### **Ways to Access PowerShell**
1. **Windows Search** → Type "PowerShell" and open.
2. **Windows Terminal** → Supports multiple CLI environments.
3. **Windows PowerShell ISE** → An IDE for PowerShell scripting.
4. **CMD** → Run PowerShell using:
    ```cmd
    powershell
    ```



### **Exploring PowerShell**
- **Prompt Format**:
    ```
    PS C:\Users\htb-student> ipconfig
    ```
    - `PS` = PowerShell
    - `C:\Users\htb-student>` = Current directory
    - `ipconfig` = Executed command
- Almost all CMD commands work in PowerShell.



### **Getting Help in PowerShell**
- **Basic Help Command**:
    ```powershell
    Get-Help <cmdlet>
    ```
- Example:
    ```powershell
    Get-Help Test-Wsman
    ```
- **Updating Help Documentation**:
    ```powershell
    Update-Help
    ```
- **Viewing Detailed Help**:
    ```powershell
    Get-Help <cmdlet> -detailed
    ```
- **Viewing Examples**:
    ```powershell
    Get-Help <cmdlet> -examples
    ```
- **Online Help**:
    ```powershell
    Get-Help <cmdlet> -online
    ```



### **Checking the Current Location**
- Use `Get-Location` to determine the current working directory.    
    ```powershell
    Get-Location
    ```



### **Listing Directory Contents**
- Use `Get-ChildItem` to list files and folders.
    ```powershell
    Get-ChildItem
    ```
- Example output:
    ```
    Mode   LastWriteTime         Length Name
    ----   -------------         ------ ----
    d----- 10/26/2021  10:26 PM         Documents
    d----- 1/28/2021   7:05 PM          Downloads
    d----- 9/26/2022  12:27 PM          Pictures
    ```



### **Changing Directories**
- Use `Set-Location` to navigate:
    ```powershell
    Set-Location .\Documents\
    ```
- Using absolute paths:
    ```powershell
    Set-Location C:\Users\DLarusso\Documents
    ```



### **Displaying File Contents**
- Use `Get-Content` to read a file:
    ```powershell
    Get-Content Readme.md
    ```



### **Finding Commands in PowerShell**
- **Get a list of all available commands:**
    ```powershell
    Get-Command
    ```
- **Search commands by verb:**
    ```powershell
    Get-Command -verb get
    ```
- **Search commands by noun:**
    ```powershell
    Get-Command -noun windows*
    ```



### **Checking Command History**
- Use `Get-History` to see past commands from the current session.
    ```powershell
    Get-History
    ```
- Re-run a command using:
    ```powershell
    r <command_id>
    ```
- **Persistent History** (`PSReadLine` stores commands across sessions):
    ```powershell
    Get-Content C:\Users\DLarusso\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
    ```



### **Clearing the Screen**
- Clear the terminal:
    ```powershell
    Clear-Host
    ```
- Aliases:
    ```powershell
    cls  # Same as Clear-Host
    ```



### **Useful PowerShell Hotkeys**

|Hotkey|Description|
|---|---|
|`CTRL + R`|Searchable history|
|`CTRL + L`|Clear the screen|
|`Escape`|Clears the current command line|
|`↑ / ↓`|Scroll through command history|
|`F7`|Shows an interactive history list|



### **Tab Completion**
- Press `TAB` to autocomplete commands and paths.



### **Using Aliases**
- View existing aliases:
    ```powershell
    Get-Alias
    ```
- Common Aliases:
    |Alias|Command|
    |---|---|
    |`pwd`|`Get-Location`|
    |`ls`|`Get-ChildItem`|
    |`cd`|`Set-Location`|
    |`cat`|`Get-Content`|
    |`clear`|`Clear-Host`|
    |`curl`|`Invoke-WebRequest`|
- **Create a custom alias:**
    ```powershell
    Set-Alias -Name gh -Value Get-Help
    ```



### **Conclusion**
- Mastering **navigation, searching, and history** in PowerShell is essential.
- **Aliases, hotkeys, and tab completion** improve efficiency.
- Next steps: **exploring PowerShell modules and cmdlets.**



### Questions
- What command string can we use to view the help documentation for the command Get-Location? (full string)
	- Get-Help Get-Location
- What command can we use to show us our current location on the host system?
	- Get-Location
- What hotkey can be used to clear our input line completely?
	- ESCAPE