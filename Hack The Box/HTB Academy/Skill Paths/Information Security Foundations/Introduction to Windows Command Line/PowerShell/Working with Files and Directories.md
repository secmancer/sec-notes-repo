### Introduction
- We already know how to navigate around the host and manage users and groups utilizing only PowerShell; now, it is time to explore files and directories. 
- In this section, we will experiment with creating, modifying, and deleting files and directories, along with a quick introduction to file permissions and how to enumerate them. 
- By now, we should be familiar with the `Get, Set, New` verbs, among others, so we will speed this up with our examples by combining several commands into a single shell session.



### Creating/Moving/Deleting Files & Directories
- Many of the cmdlets we will discuss in this section can apply to working with files and folders, so we will combine some of our actions to work more efficiently (as any good pentester or sysadmin should strive to.). 
- The table below lists the commonly used cmdlets used when dealing with objects in PowerShell.
![[Screenshot_20241110_211749.png]]

> **Scenario: Greenhorn's new Security Chief, Mr. Tanaka, has requested that a set of files and folders be created for him. He plans to use them for SOP documentation for the Security team. Since he just got host access, we have agreed to set the file & folder structure up for him. If you would like to follow along with the examples below, please feel free. For your practice, we removed the folders and files discussed below so you can take a turn recreating them.**

- First, we are going to start with the folder structure he requested. 
- We are going to make three folders named :
	- `SOPs`
	    - `Physical Sec`
	    - `Cyber Sec`
	    - `Training`
- We will use the `Get-Item`, `Get-ChildItem`, and `New-Item` commands to create our folder structure.
- Let us get started. 
- We first need to determine `where we are` in the host and then move to Mr. Tanaka's `Documents` folder.



### Finding Our Place
```powershell-session
PS C:\htb> Get-Location

Path
----
C:\Users\MTanaka

PS C:\Users\MTanaka> cd Documents
PS C:\Users\MTanaka\Documents>
```
- Now that we are in the correct directory, it's time to get to work. 
- Next, we need to make the SOPs folder.
- The New-Item Cmdlet can be used to accomplish this.
- #### New-Item
```powershell-session
PS C:\Users\MTanaka\Documents>  new-item -name "SOPs" -type directory


    Directory: C:\Users\MTanaka\Documents


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         10/5/2022  12:20 PM                SOPs
```
- Our main directory exists now. Let us create our nested folders `Physical Sec, Cyber Sec, and Training`. 
- We can utilize the same command from last time or the alias `mkdir`. 
- First, we need to move into the `SOPs` Directory.
- #### Making More Directories
```powershell-session
PS C:\Users\MTanaka\Documents> cd SOPs 

PS C:\Users\MTanaka\Documents\SOPs> mkdir "Physical Sec"

    Directory: C:\Users\MTanaka\Documents\SOPs


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         10/5/2022   4:30 PM                Physical Sec

PS C:\Users\MTanaka\Documents\SOPs> mkdir "Cyber Sec"

    Directory: C:\Users\MTanaka\Documents\SOPs


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         10/5/2022   4:30 PM                Cyber Sec

PS C:\Users\MTanaka\Documents\SOPs> mkdir "Training"

    Directory: C:\Users\MTanaka\Documents\SOPs


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         10/5/2022   4:31 PM                Training  

PS C:\Users\MTanaka\Documents\SOPs> Get-ChildItem 

Directory: C:\Users\MTanaka\Documents\SOPs


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        10/5/2022   9:08 AM                Cyber Sec
d-----        11/5/2022   9:09 AM                Physical Sec
d-----        11/5/2022   9:08 AM                Training
```
- Now that we have our directory structure in place. 
- It's time to start populating the files required. 
- Mr. Tanaka asked for a Markdown file in each folder like so:
	- `SOPs` > ReadMe.md
	    - `Physical Sec` > Physical-Sec-draft.md
	    - `Cyber Sec` > Cyber-Sec-draft.md
	    - `Training` > Employee-Training-draft.md
- In each file, he has requested this header at the top:
	- Title: Insert Document Title Here
	- Date: x/x/202x
	- Author: MTanaka
	- Version: 0.1 (Draft)
- We should be able to quickly knock this out using the `New-Item` cmdlet and the `Add-Content` cmdlet.
- #### Making Files
```powershell-session
PS C:\htb> PS C:\Users\MTanaka\Documents\SOPs> new-Item "Readme.md" -ItemType File

    Directory: C:\Users\MTanaka\Documents\SOPs

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        11/10/2022   9:12 AM              0 Readme.md

PS C:\Users\MTanaka\Documents\SOPs> cd '.\Physical Sec\'
PS C:\Users\MTanaka\Documents\SOPs\Physical Sec> ls
PS C:\Users\MTanaka\Documents\SOPs\Physical Sec> new-Item "Physical-Sec-draft.md" -ItemType File

    Directory: C:\Users\MTanaka\Documents\SOPs\Physical Sec

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        11/10/2022   9:14 AM              0 Physical-Sec-draft.md

PS C:\Users\MTanaka\Documents\SOPs\Physical Sec> cd ..
PS C:\Users\MTanaka\Documents\SOPs> cd '.\Cyber Sec\'

PS C:\Users\MTanaka\Documents\SOPs\Cyber Sec> new-Item "Cyber-Sec-draft.md" -ItemType File

    Directory: C:\Users\MTanaka\Documents\SOPs\Cyber Sec

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        11/10/2022   9:14 AM              0 Cyber-Sec-draft.md

PS C:\Users\MTanaka\Documents\SOPs\Cyber Sec> cd ..
PS C:\Users\MTanaka\Documents\SOPs> cd .\Training\
PS C:\Users\MTanaka\Documents\SOPs\Training> ls
PS C:\Users\MTanaka\Documents\SOPs\Training> new-Item "Employee-Training-draft.md" -ItemType File

    Directory: C:\Users\MTanaka\Documents\SOPs\Training

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        11/10/2022   9:15 AM              0 Employee-Training-draft.md

PS C:\Users\MTanaka\Documents\SOPs\Training> cd ..
PS C:\Users\MTanaka\Documents\SOPs> tree /F
Folder PATH listing
Volume serial number is F684-763E
C:.
│   Readme.md
│
├───Cyber Sec
│       Cyber-Sec-draft.md
│
├───Physical Sec
│       Physical-Sec-draft.md
│
└───Training
        Employee-Training-draft.md
```
- Now that we have our files, we need to add content inside them. 
- We can do so with the `Add-Content` cmdlet.
- #### Adding Content
```powershell-session
PS C:\htb> Add-Content .\Readme.md "Title: Insert Document Title Here
>> Date: x/x/202x
>> Author: MTanaka
>> Version: 0.1 (Draft)"  
  
PS C:\Users\MTanaka\Documents\SOPs> cat .\Readme.md
Title: Insert Document Title Here
Date: x/x/202x
Author: MTanaka
Version: 0.1 (Draft)
```
- We would then perform this same process we did for `Readme.md` in every other file we created for Mr. Tanaka. 
- This scenario felt a bit tedious, right? 
- Creating files over and over by hand can get tiresome. 
- This is where automation and scripting come into place. 
- It is a bit out of reach right now, but in a later section in this module, we will discuss how to make a quick PowerShell Module, using variables and writing scripts to make things easier.

> **Scenario Cont.: Mr. Tanaka has asked us to change the name of the file `Cyber-Sec-draft.md` to `Infosec-SOP-draft.md`.**


- We can quickly knock this task out using the `Rename-Item` cmdlet.
- #### Renaming An Object
```powershell-session
PS C:\Users\MTanaka\Documents\SOPs\Cyber Sec> ls

    Directory: C:\Users\MTanaka\Documents\SOPs\Cyber Sec

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        11/10/2022   9:14 AM              0 Cyber-Sec-draft.md

PS C:\Users\MTanaka\Documents\SOPs\Cyber Sec> Rename-Item .\Cyber-Sec-draft.md -NewName Infosec-SOP-draft.md
PS C:\Users\MTanaka\Documents\SOPs\Cyber Sec> ls

    Directory: C:\Users\MTanaka\Documents\SOPs\Cyber Sec

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        11/10/2022   9:14 AM              0 Infosec-SOP-draft.md
```
- All we needed to do above was issue the `Rename-Item` cmdlet, give it the original filename we want to change (`Cyber-Sec-draft.md`), and then tell it our new name with the `-NewName` (`Infosec-SOP-draft.md`) parameter. 
- Seems simple right? 
- We could take this further and rename all files within a directory or change the file type or several different actions. 
- In our example below, we will change the names of all text files in Mr. Tanakas Desktop from `file.txt` to `file.md`.
- #### Files1-5.txt are on MTanaka's Desktop
```powershell-session
PS C:\Users\MTanaka\Desktop> ls

    Directory: C:\Users\MTanaka\Desktop

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        10/13/2022   1:05 PM              0 file-1.txt
-a----        10/13/2022   1:05 PM              0 file-2.txt
-a----        10/13/2022   1:06 PM              0 file-3.txt
-a----        10/13/2022   1:06 PM              0 file-4.txt
-a----        10/13/2022   1:06 PM              0 file-5.txt

PS C:\Users\MTanaka\Desktop> get-childitem -Path *.txt | rename-item -NewName {$_.name -replace ".txt",".md"}
PS C:\Users\MTanaka\Desktop> ls

    Directory: C:\Users\MTanaka\Desktop

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        10/13/2022   1:05 PM              0 file-1.md
-a----        10/13/2022   1:05 PM              0 file-2.md
-a----        10/13/2022   1:06 PM              0 file-3.md
-a----        10/13/2022   1:06 PM              0 file-4.md
-a----        10/13/2022   1:06 PM              0 file-5.md
```
- As we can see above, we had five text files on the Desktop. 
- We changed them to `.md` files using `get-childitem -Path *.txt` to select the objects and used `|` to send those objects to the `rename-item -NewName {$_.name -replace ".txt",".md"}` cmdlet which renames everything from its original name ($_.name) and replaces the `.txt` from name to `.md`. 
- This is a much faster way to interact with files and perform bulk actions. 
- Now that we have completed all of Mr. Tanakas' requests, let us discuss File and Directory permissions for a second.



### What are File & Directory Permissions
- Permissions define who has access to an object and what actions they can perform, enabling granular security control and maintaining a strong security posture.
- Key permission types in Windows include:
    - **Full Control**: Complete access, including changing permissions and ownership.
    - **Modify**: Read, write, and delete files/folders.
    - **List Folder Contents**: View and list folder contents (folders only).
    - **Read and Execute**: View file contents and run executables.
    - **Write**: Create new files/subfolders and modify existing files.
    - **Read**: View files and folders.
    - **Traverse Folder**: Access files in subfolders without accessing higher-level folders.
- NTFS supports inheriting permissions from a parent directory, simplifying permission management. Inheritance can be disabled for specific objects when needed.
- Managing permissions is easier through the Windows GUI but can be complex from the CLI.
- Exploring `find` and `filter` functionalities in the CLI enhances file and directory management.



### Questions
- What Cmdlet has an alias of " cat" ?
	- Get-Content
- What Cmdlet can we use to create new files and folders?
	- New-Item
- Using the skills discussed in this section, practice creating, editing, and removing files and directories on the target host provided. Type COMPLETE as the answer below when you are ready to move on.
	- Complete