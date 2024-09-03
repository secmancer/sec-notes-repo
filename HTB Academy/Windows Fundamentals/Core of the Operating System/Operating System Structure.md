### Windows Directory Structure
#### Root Directory
- **`<drive_letter>:\`** (commonly `C:\`): The root directory where the operating system is installed. Other physical and virtual drives are assigned different letters.

#### Key Directories and Their Functions:
1. **`Perflogs`**
    - Contains Windows performance logs. Typically empty by default.

1. **`Program Files`**
    - On 32-bit systems: Contains 16-bit and 32-bit programs.
    - On 64-bit systems: Contains 64-bit programs.

1. **`Program Files (x86)`**
    - On 64-bit systems: Contains 32-bit and 16-bit programs.

1. **`ProgramData`**
    - A hidden folder containing essential data for installed programs, accessible by the program regardless of the user.

1. **`Users`**
    - Contains user profiles, including:
        - **`Default`**: Template profile for new users.
        - **`Public`**: Shared files accessible to all users by default.

1. **`AppData`**
    - **`Roaming`**: Contains data that follows the user profile (e.g., custom dictionaries).
    - **`Local`**: Machine-specific data not synchronized across networks.
    - **`LocalLow`**: Similar to Local but with lower data integrity levels.

1. **`Windows`**
    - Contains most of the files required for the Windows operating system.

1. **`System`, `System32`, `SysWOW64`**
    - **`System32`**: Contains core DLLs required for Windows features.
    - **`SysWOW64`**: Contains 32-bit DLLs on 64-bit systems.
    - **`WinSxS`**: Windows Component Store with copies of all Windows components and updates.

### Exploring Directories Using Command Line
#### Using `dir` Command
The `dir` command displays the contents of a directory.
- **Basic Command:** dir c:\ /a
- Lists all files and directories in the root directory of `C:\`, including hidden and system files.

Example Output:
![[Screenshot_20240813_105759.png]]

#### Using `tree` Command
The `tree` command graphically displays the directory structure of a path or disk.
- **Basic Command:** tree "c:\Program Files (x86)\VMware"
- Displays the directory tree of `C:\Program Files (x86)\VMware`.

Example Output:
![[Screenshot_20240813_105907.png]]
#### Detailed View with `tree` and `more`
To view the directory structure with detailed file listings, you can use:
- **Command: tree c:\ /f | more
	- - **`/f`**: Displays files in addition to directories.
	- **`| more`**: Allows viewing the output one screen at a time.

### Questions
- Find the non-standard directory in the C drive. Submit the contents of the flag file saved in this directory.
	- c8fe8d977d3a0c655ed7cf81e4d13c75