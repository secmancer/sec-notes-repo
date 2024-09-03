#### Types of Windows File Systems
1. **FAT12** and **FAT16**: These are outdated file systems and are not used in modern Windows operating systems.

1. **FAT32 (File Allocation Table 32)**
    - **Usage**: Commonly used for USB memory sticks, SD cards, and sometimes hard drives.
    - **"32"**: Refers to the use of 32 bits for identifying data clusters.
    - **Pros**:
        - High device compatibility (computers, cameras, gaming consoles, etc.).
        - Supported by all Windows versions from Windows 95, as well as MacOS and Linux.
    - **Cons**:
        - File size limit of 4GB.
        - No built-in data protection or compression.
        - Requires third-party tools for encryption.

1. **NTFS (New Technology File System)**
    - **Usage**: Default file system for Windows since Windows NT 3.1.
    - **Pros**:
        - Reliable with file system recovery and consistency restoration.
        - Supports granular permissions and extensive security.
        - Handles large partitions and files.
        - Built-in journaling for file modifications.
    - **Cons**:
        - Limited support on mobile devices and older media devices.

1. **exFAT (Extended File Allocation Table)**
    - **Usage**: Designed for flash drives and external drives, providing a better solution for larger files and storage capacities compared to FAT32.
    - **Pros**:
        - Supports very large files and volumes.
        - More suitable for modern storage needs compared to FAT32.
    - **Cons**:
        - Limited support in older operating systems.

### NTFS Permissions
NTFS allows for detailed permission settings on files and folders. Permissions can be managed through File Explorer or the `icacls` command-line utility.

#### Key Permissions
1. **Full Control (F)**: Allows reading, writing, modifying, and deleting files/folders.

1. **Modify (M)**: Allows reading, writing, and deleting files/folders.

1. **List Folder Contents (L)**: Allows viewing and listing folder contents and executing files.

1. **Read and Execute (RX)**: Allows viewing, listing files, and executing files.

1. **Write (W)**: Allows adding files to folders and writing to files.

1. **Read (R)**: Allows viewing and listing folder contents and viewing files.

1. **Traverse Folder (T)**: Allows navigating through folders without needing to list contents.

#### Permissions Inheritance
Permissions can be inherited from parent folders, simplifying administration:
- **(CI)**: Container Inherit
- **(OI)**: Object Inherit
- **(IO)**: Inherit Only
- **(NP)**: Do Not Propagate Inherit
- **(I)**: Inherited from Parent Container

### Managing NTFS Permissions with `icacls`
The `icacls` utility allows for advanced NTFS permission management from the command line.

#### Listing Permissions
- **Command:** icacls c:\windows

Example Output:
![[Screenshot_20240813_113224.png]]
#### Granting Permissions
- **Command:** icacls c:\users /grant joe:f
- Grants user `joe` full control over `c:\users`, but not recursively to subdirectories unless specified.

#### Revoking Permissions
- **Command:** icacls c:\users /remove joe
- Removes permissions for user `joe` on `c:\users`.

`icacls` allows for granular control over permissions, inheritance, and ownership in a domain setting, making it a powerful tool for administrators.

For a full list of `icacls` command-line arguments and options, you can refer to the official documentation or run: icacls /?

### Questions
- What system user has full control over the c:\users directory?
	- bob.smith