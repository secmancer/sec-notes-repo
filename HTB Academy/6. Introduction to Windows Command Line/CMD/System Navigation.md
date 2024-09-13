#### Goals:
- Successfully navigate and move around the system.
- Cover:
    - Listing directories
    - Finding the current location
    - Moving between directories using `cd`
    - Exploring the file system

#### 1. **Listing a Directory**
- Command: `dir`
    - Displays contents of the current directory.
    - Example:
```
C:\Users\htb\Desktop> dir
Directory of C:\Users\htb\Desktop
06/11/2021  11:57 PM    0 file1.txt
06/11/2021  11:57 PM    0 file2.txt
06/11/2021  11:57 PM    0 file3.txt
```
- Use `/?` for a full list of arguments and features.


#### 2. **Finding the Current Location**
- Commands: `cd` or `chdir`
    - Displays the current directory if no arguments are provided.
    - Example:
```
C:\htb> cd
C:\htb
```


#### 3. **Moving Around Using `cd`/`chdir`**
- `cd [path]`: Moves to the specified directory.
    - **Absolute Path**:
        - Example: `cd C:\Users\htb\Pictures` (moves to the Pictures directory from root).
    - **Relative Path**:
        - Example: `cd .\Pictures` (moves to Pictures relative to the current directory).
- **Moving up directories**:
    - Use `cd ..` to move up one level.
    - Example: `cd ..\..\..\` moves three levels up to the root.


#### 4. **Exploring the File System**
- Command: `tree`
    - Displays directory structure in a tree-like format.
    - Example:
```
C:\htb\student\> tree
C:.
├───Documents
├───Downloads
├───Pictures
```
- Use `tree /F` to display all files within the directories.


#### 5. **Interesting Directories for Attackers**

| Name                | Location                          | Description                                                                        |
| ------------------- | --------------------------------- | ---------------------------------------------------------------------------------- |
| %SYSTEMROOT%\Temp   | C:\Windows\Temp                   | Global temp folder, accessible by all users for dropping files.                    |
| %TEMP%              | C:\Users<user>\AppData\Local\Temp | User-specific temp folder, accessible by the local user.                           |
| %PUBLIC%            | C:\Users\Public                   | Publicly accessible folder for all users to read/write/execute files.              |
| %ProgramFiles%      | C:\Program Files                  | Contains installed 64-bit applications, useful for identifying installed software. |
| %ProgramFiles(x86)% | C:\Program Files (x86)            | Contains installed 32-bit applications, useful for identifying installed software. |

![[Screenshot_20240913_095758.png]]


## Questions
- What command will give us a listing of all files and folders in a specified path?
	- tree /F
- What command will print my current working directory onto the console?
	- cd