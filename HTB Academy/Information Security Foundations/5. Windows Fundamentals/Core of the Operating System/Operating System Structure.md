**Root Directory:**
- The root directory is `<drive_letter>:\` (commonly `C:\`).
- It is where the operating system is installed.

**Directory Overview:**
- **Perflogs**: Can hold Windows performance logs but is empty by default.
- **Program Files**: On 32-bit systems, contains all 16-bit and 32-bit programs. On 64-bit systems, contains only 64-bit programs.
- **Program Files (x86)**: On 64-bit systems, this folder contains 32-bit and 16-bit programs.
- **ProgramData**: Hidden folder with data essential for certain programs to run, accessible regardless of the user.
- **Users**: Contains user profiles, including:
    - **Default**: Template for new user profiles.
    - **Public**: Shared files accessible by all users and shared over the network by default.
- **AppData**: Hidden user-specific application data and settings:
    - **Roaming**: Machine-independent data that follows the user's profile (e.g., custom dictionaries).
    - **Local**: Computer-specific data not synchronized across the network.
    - **LocalLow**: Similar to Local but with lower data integrity; used by applications in protected or safe modes.
- **Windows**: Contains the majority of files required for the Windows operating system.
- **System, System32, SysWOW64**: Contains DLLs for core Windows features and API; these folders are searched for DLLs if no absolute path is specified.
- **WinSxS**: Windows Component Store, holding copies of all Windows components, updates, and service packs.

![[Screenshot_20240912_151416.png]]

**Exploring Directories Using Command Line:**
- **`dir` Command**: Lists files and directories in the specified path.
```
C:\htb> dir c:\ /a
```
- **`tree` Command**: Graphically displays the directory structure of a path or disk.
```
C:\htb> tree "c:\Program Files (x86)\VMware"
```
- **`tree` Command with `/f` Option**: Displays all files in the directory, one screen at a time.
```
C:\htb> tree c:\ /f | more
```


### Questions
- Find the non-standard directory in the C drive. Submit the contents of the flag file saved in this directory.
	- c8fe8d977d3a0c655ed7cf81e4d13c75