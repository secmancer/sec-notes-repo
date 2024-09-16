**Overview:**
- **Purpose**: Explore file and directory operations in PowerShell.
- **Tasks**: Creating, modifying, and deleting files and directories.
- **File Permissions**: Introduction to file permissions and enumeration.


**PowerShell Cmdlets:**
- **Common Cmdlets**: Use cmdlets like `Get`, `Set`, `New`, `Remove`, etc.
- **Efficiency**: Combine commands in a single shell session for streamlined operations.



**Cmdlets for File and Directory Operations:**

|Cmdlet|Description|
|---|---|
|`Get-Item`|Retrieves an item (file or directory)|
|`Set-Item`|Changes the properties of an item|
|`New-Item`|Creates a new item (file or directory)|
|`Remove-Item`|Deletes an item (file or directory)|
|`Copy-Item`|Copies an item (file or directory)|
|`Move-Item`|Moves an item (file or directory)|
|`Get-ChildItem`|Lists the contents of a directory|
|`Rename-Item`|Renames an item (file or directory)|

![[Screenshot_20240915_213348.png]]


### Scenario: Setting Up Files and Directories for Mr. Tanaka
**Objective:** Create a folder structure and files as requested by Mr. Tanaka for SOP documentation.
**1. Folder Structure:**
- **Top-Level Folder:**
    - SOPs
        - Physical Sec
        - Cyber Sec
        - Training
**2. Commands Used:**
- **Finding Our Place:**
```
PS C:\htb> Get-Location
Path
----
C:\Users\MTanaka

PS C:\Users\MTanaka> cd Documents
PS C:\Users\MTanaka\Documents>
```
- **Creating Main Folder:**
```
PS C:\Users\MTanaka\Documents> New-Item -Name "SOPs" -Type Directory
```
- **Creating Nested Folders:**
```
PS C:\Users\MTanaka\Documents> cd SOPs
PS C:\Users\MTanaka\Documents\SOPs> mkdir "Physical Sec"
PS C:\Users\MTanaka\Documents\SOPs> mkdir "Cyber Sec"
PS C:\Users\MTanaka\Documents\SOPs> mkdir "Training"
```
- **Verifying Directory Structure:**
```
PS C:\Users\MTanaka\Documents\SOPs> Get-ChildItem
```
**3. Creating Files:**
- **Creating Files in Each Folder:**
```
PS C:\Users\MTanaka\Documents\SOPs> New-Item "Readme.md" -ItemType File

PS C:\Users\MTanaka\Documents\SOPs\Physical Sec> New-Item "Physical-Sec-draft.md" -ItemType File

PS C:\Users\MTanaka\Documents\SOPs\Cyber Sec> New-Item "Cyber-Sec-draft.md" -ItemType File

PS C:\Users\MTanaka\Documents\SOPs\Training> New-Item "Employee-Training-draft.md" -ItemType File
```
- **Adding Content to Files:**
```
PS C:\Users\MTanaka\Documents\SOPs> Add-Content .\Readme.md "Title: Insert Document Title Here`nDate: x/x/202x`nAuthor: MTanaka`nVersion: 0.1 (Draft)"
```
Repeat the content addition for other files in their respective directories.
**4. Renaming Files:**
- **Renaming a Single File:**
```
PS C:\Users\MTanaka\Documents\SOPs\Cyber Sec> Rename-Item .\Cyber-Sec-draft.md -NewName "Infosec-SOP-draft.md"
```
- Renaming Multiple Files:
```
PS C:\Users\MTanaka\Desktop> Get-ChildItem -Path *.txt | Rename-Item -NewName {$_.name -replace ".txt",".md"}
```
**5. Summary:**
- **Folder Structure**: Created using `New-Item` and `mkdir` commands.
- **Files Creation**: Utilized `New-Item` to create files and `Add-Content` to add content.
- **Renaming Files**: Employed `Rename-Item` for individual and bulk file renaming.


**Note:**
- **Automation**: Repetitive tasks can be automated with scripts and PowerShell modules for efficiency.


### File & Directory Permissions

**Overview:** Permissions in a host system define who can access specific files or directories and what actions they can perform. Properly managing permissions helps maintain security by ensuring that data access is limited to authorized users and that the principle of "need to know" is adhered to.
**Key Permission Types:**
- **Full Control:**
    - Allows complete access, including modifying permissions, changing ownership, reading, writing, and executing the file or folder.
- **Modify:**
    - Permits reading, writing, and deleting files and folders.
- **List Folder Contents:**
    - Enables viewing and listing the contents of folders and subfolders and executing files within folders (applies only to folders).
- **Read and Execute:**
    - Allows viewing file contents and executing executable files (.ps1, .exe, .bat, etc.).
- **Write:**
    - Grants the ability to create new files and subfolders and add content to existing files.
- **Read:**
    - Permits viewing and listing folders and subfolders and reading file contents.
- **Traverse Folder:**
    - Allows access to files or subfolders within a directory tree without granting access to the parent directory's contents. Useful for selective access control.



**Permissions Inheritance:**
- **Inheritance in NTFS:**
    - Permissions set on a parent directory can be inherited by its child files and subdirectories. This feature simplifies managing permissions by applying changes to multiple objects simultaneously.
- **Disabling Inheritance:**
    - Inheritance can be disabled for specific files, folders, or subfolders. When disabled, permissions must be set manually for the affected objects.


**Complexity of Permissions:**
- **CLI Limitations:**
    - While managing permissions through the command-line interface (CLI) is possible, it can be complex and cumbersome. For comprehensive permission management, it's often more efficient to use graphical user interfaces or dedicated modules, such as the Windows Fundamentals Module.


**Next Steps:**
- **Upcoming Topics:**
    - In future lessons, we'll explore finding and filtering content within files on the host, further enhancing your CLI skills.


## Questions
- What Cmdlet has an alias of " cat" ?
	- Get-Content
- What Cmdlet can we use to create new files and folders?
	- New-Item
- Using the skills discussed in this section, practice creating, editing, and removing files and directories on the target host provided. Type COMPLETE as the answer below when you are ready to move on.
	- COMPLETE