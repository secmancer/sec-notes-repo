**File Systems:**
1. **FAT12**: Outdated; no longer used in modern Windows systems.
2. **FAT16**: Outdated; no longer used in modern Windows systems.
3. **FAT32 (File Allocation Table 32)**:
    - **Usage**: Common on USB sticks, SD cards, and some hard drives.
    - **Advantages**:
        - Broad compatibility with various devices (computers, cameras, consoles, smartphones).
        - Supported by Windows (from Windows 95), macOS, and Linux.
    - **Disadvantages**:
        - File size limit of 4GB.
        - No built-in data protection or compression.
        - Requires third-party tools for file encryption.


**NTFS (New Technology File System)**:
- **Usage**: Default file system for Windows since Windows NT 3.1.
- **Advantages**:
    - Reliable with system failure recovery.
    - Granular file and folder permissions.
    - Supports very large partitions.
    - Built-in journaling for file modifications.
- **Disadvantages**:
    - Limited support on mobile and older media devices.


**exFAT (Extended File Allocation Table)**:
- **Usage**: Designed for flash drives and SD cards with large file sizes and no journaling.

![[Screenshot_20240912_151656.png]]

**NTFS Permissions:**
- **Permission Types**:
    - **Full Control**: Read, write, change, and delete files/folders.
    - **Modify**: Read, write, and delete files/folders.
    - **List Folder Contents**: View and list folder contents; applies to folders only.
    - **Read and Execute**: View and list files/folders; execute files.
    - **Write**: Add files and write to files.
    - **Read**: View and list folders/files.
    - **Traverse Folder**: Move through folders to reach other files/folders without listing contents.
- **Inheritance**: Files and folders inherit permissions from their parent folder. Explicit permissions can be set by disabling inheritance.


**Managing Permissions with `icacls`:**
- **Listing Permissions**:
```
C:\htb> icacls c:\windows
```
- **Output**: Displays NTFS permissions for the directory and inheritance settings.
- **Adding Permissions**:
```
C:\htb> icacls c:\users /grant joe:f
```
- Grants full control to user `joe` over the `c:\users` directory.
- **Removing Permissions**:
```
C:\htb> icacls c:\users /remove joe
```
- **Inheritance Settings**:
	- **(CI)**: Container inherit
	- **(OI)**: Object inherit
	- **(IO)**: Inherit only
	- **(NP)**: Do not propagate inherit
	- **(I)**: Inherited from parent container

**Notes on `icacls` Usage**:
- Useful for setting, modifying, and revoking permissions from the command line.
- Detailed documentation and command-line arguments can be found in `icacls` help.


### Questions
- What system user has full control over the c:\users directory?
	- bob.smith