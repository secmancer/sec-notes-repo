This section covers file and directory management in PowerShell, emphasizing creating, modifying, and deleting files and directories while touching on file permissions. Here's a summary and breakdown of the key concepts and commands:

### **Key PowerShell Commands for File & Folder Management:**

- **`Get-Item (gi)`**: Retrieve an object (file, folder, etc.).
- **`Get-ChildItem (ls/dir/gci)`**: List contents of a directory or registry hive.
- **`New-Item (ni/mkdir)`**: Create new files, folders, symlinks, etc.
- **`Set-Item (si)`**: Modify the properties of an object.
- **`Copy-Item (cp/ci)`**: Copy an object.
- **`Rename-Item (ren/rni)`**: Rename an object.
- **`Remove-Item (rm/del/rmdir)`**: Delete an object.
- **`Get-Content (cat/type)`**: Display content within a file.
- **`Add-Content (ac)`**: Append content to a file.
- **`Set-Content (sc)`**: Overwrite content in a file.
- **`Clear-Content (clc)`**: Clear content of files without deleting the file.
- **`Compare-Object (diff/compare)`**: Compare objects, including content.

### **Scenario: Setting Up a Folder Structure**

**Task:** Create a folder structure and files for SOP documentation.

1. **Navigate to Mr. Tanaka's Documents Folder:**
    
    - `Get-Location`: Shows the current directory.
    - `cd Documents`: Changes the directory to `Documents`.
2. **Create the Main Directory:**
    
    - `New-Item -name "SOPs" -type directory`: Creates a new folder named `SOPs`.
3. **Create Nested Folders:**
    
    - `cd SOPs`: Navigate to the `SOPs` directory.
    - `mkdir "Physical Sec"`: Creates the `Physical Sec` folder.
    - `mkdir "Cyber Sec"`: Creates the `Cyber Sec` folder.
    - `mkdir "Training"`: Creates the `Training` folder.
4. **Create Markdown Files in Each Folder:**
    
    - `new-Item "Readme.md" -ItemType File`: Creates `Readme.md` in `SOPs`.
    - `new-Item "Physical-Sec-draft.md" -ItemType File`: Creates `Physical-Sec-draft.md` in `Physical Sec`.
    - `new-Item "Cyber-Sec-draft.md" -ItemType File`: Creates `Cyber-Sec-draft.md` in `Cyber Sec`.
    - `new-Item "Employee-Training-draft.md" -ItemType File`: Creates `Employee-Training-draft.md` in `Training`.
5. **Add Content to Files:**
    
    - `Add-Content .\Readme.md "Title: Insert Document Title Here\nDate: x/x/202x\nAuthor: MTanaka\nVersion: 0.1 (Draft)"`: Adds specified content to `Readme.md`.
6. **Rename a File:**
    
    - `Rename-Item .\Cyber-Sec-draft.md -NewName Infosec-SOP-draft.md`: Renames `Cyber-Sec-draft.md` to `Infosec-SOP-draft.md`.
7. **Bulk Rename Files:**
    
    - `get-childitem -Path *.txt | rename-item -NewName {$_.name -replace ".txt",".md"}`: Renames all `.txt` files to `.md` in a directory.

### **File & Directory Permissions Overview:**

Permissions control who can access and modify files and directories, critical for maintaining security. Key permission types include:

- **Full Control**: Complete control over the object, including changing permissions and ownership.
- **Modify**: Allows reading, writing, and deleting files.
- **List Folder Contents**: View and list folders and subfolders (applies to folders only).
- **Read and Execute**: View content and run executables.
- **Write**: Create new files, subfolders, and add content to files.
- **Read**: View and list files and folders.

### Questions
- What Cmdlet has an alias of " cat" ?
	- Get-Content
- What Cmdlet can we use to create new files and folders?
	- New-Item
- Using the skills discussed in this section, practice creating, editing, and removing files and directories on the target host provided. Type COMPLETE as the answer below when you are ready to move on.
	- COMPLETE