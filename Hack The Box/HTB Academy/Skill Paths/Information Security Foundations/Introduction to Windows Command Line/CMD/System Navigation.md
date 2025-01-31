### Introduction
- **Objective**: Learn to navigate and explore the Windows file system using Command Prompt.
- **Key Topics**:
  - Listing directory contents.
  - Finding the current working directory.
  - Moving between directories using `cd` and `chdir`.
  - Exploring the file system with `tree`.
  - Identifying interesting directories for attackers.



### Listing a Directory
- **Command**: `dir`
  - Lists the contents of the current directory.
  - Example:
    ```cmd
    C:\Users\htb\Desktop> dir
    ```
    Output:
    ```
    Volume in drive C has no label.
    Volume Serial Number is DAE9-5896

    Directory of C:\Users\htb\Desktop

    06/11/2021  11:59 PM    <DIR>          .
    06/11/2021  11:59 PM    <DIR>          ..
    06/11/2021  11:57 PM                 0 file1.txt
    06/11/2021  11:57 PM                 0 file2.txt
    06/11/2021  11:57 PM                 0 file3.txt
    04/13/2021  11:24 AM             2,391 Microsoft Teams.lnk
    06/11/2021  11:57 PM                 0 super-secret-sauce.txt
    06/11/2021  11:59 PM                 0 write-secrets.ps1
                   6 File(s)          2,391 bytes
                   2 Dir(s)  35,102,117,888 bytes free
    ```
  - **Use Case**: Quickly view files and subdirectories in the current directory.



### Finding the Current Working Directory
- **Command**: `cd` or `chdir` (without arguments)
  - Displays the current directory.
  - Example:
    ```cmd
    C:\htb> cd
    ```
    Output:
    ```
    C:\htb
    ```
  - **Use Case**: Determine your location in the file system before performing operations.



### Moving Around Using `cd`/`chdir`
- **Absolute Path**:
  - Starts from the root directory (e.g., `C:\`).
  - Example:
    ```cmd
    C:\htb> cd C:\Users\htb\Pictures
    ```
    Output:
    ```
    C:\Users\htb\Pictures>
    ```
- **Relative Path**:
  - Starts from the current directory.
  - Example:
    ```cmd
    C:\htb> cd .\Pictures
    ```
    Output:
    ```
    C:\Users\htb\Pictures>
    ```
- **Moving Up the Directory Structure**:
  - Use `..` to move up one level.
  - Example:
    ```cmd
    C:\Users\htb\Pictures> cd ..\..\..\
    ```
    Output:
    ```
    C:\>
    ```
  - **Use Case**: Efficiently navigate the file system without retyping full paths.



### Exploring the File System
- **Command**: `tree`
  - Displays the directory structure in a tree format.
  - Example:
    ```cmd
    C:\htb\student> tree
    ```
    Output:
    ```
    Folder PATH listing
    Volume serial number is 26E7-9EE4
    C:.
    ├───3D Objects
    ├───Contacts
    ├───Desktop
    ├───Documents
    ├───Downloads
    ├───Favorites
    │   └───Links
    ├───Links
    ├───Music
    ├───OneDrive
    ├───Pictures
    │   ├───Camera Roll
    │   └───Saved Pictures
    ├───Saved Games
    ├───Searches
    └───Videos
        └───Captures
    ```
- **Listing Files and Directories**:
  - Use `tree /F` to include files in the output.
  - Example:
    ```cmd
    C:\htb\student> tree /F
    ```
    Output:
    ```
    Folder PATH listing
    Volume serial number is 26E7-9EE4
    C:.
    ├───3D Objects
    ├───Contacts
    ├───Desktop
    │       passwords.txt.txt
    │       Project plans.txt
    │       secrets.txt
    ├───Documents
    ├───Downloads
    ├───Favorites
    │   │   Bing.URL
    │   └───Links
    ├───Links
    │       Desktop.lnk
    │       Downloads.lnk
    ├───Music
    ├───OneDrive
    ├───Pictures
    │   ├───Camera Roll
    │   └───Saved Pictures
    ├───Saved Games
    ├───Searches
    │       winrt--{S-1-5-21-1588464669-3682530959-1994202445-1000}-.searchconnector-ms
    └───Videos
        └───Captures
    ```
  - **Use Case**: Quickly identify files and directories of interest.



### Interesting Directories for Attackers
- **Key Directories**:
  | **Name**               | **Location**                          | **Description**                                                                 |
  |-------------------------|---------------------------------------|---------------------------------------------------------------------------------|
  | `%SYSTEMROOT%\Temp`     | `C:\Windows\Temp`                     | Global temporary files directory. Accessible to all users. Useful for dropping files. |
  | `%TEMP%`                | `C:\Users\<user>\AppData\Local\Temp`  | User-specific temporary files directory. Useful for low-privilege file drops.   |
  | `%PUBLIC%`              | `C:\Users\Public`                     | Publicly accessible directory. Less likely to be monitored.                    |
  | `%ProgramFiles%`        | `C:\Program Files`                    | Contains 64-bit applications. Useful for reconnaissance.                       |
  | `%ProgramFiles(x86)%`   | `C:\Program Files (x86)`              | Contains 32-bit applications. Useful for reconnaissance.                       |
- **Use Case**: Identify directories for dropping files, reconnaissance, and attack surface mapping.



### Summary
- **Key Commands**:
  - `dir`: Lists directory contents.
  - `cd`/`chdir`: Displays or changes the current directory.
  - `tree`: Displays directory structure in a tree format.
- **Navigation**:
  - Use absolute paths (e.g., `C:\Users\htb\Pictures`) or relative paths (e.g., `.\Pictures`).
  - Move up the directory structure using `..`.
- **Exploration**:
  - Use `tree /F` to list files and directories recursively.
- **Interesting Directories**:
  - Focus on directories like `%SYSTEMROOT%\Temp`, `%TEMP%`, and `%PUBLIC%` for reconnaissance and file drops.



### Questions
- What command will give us a listing of all files and folders in a specified path?
	- tree /F
- What command will print my current working directory onto the console?
	- cd