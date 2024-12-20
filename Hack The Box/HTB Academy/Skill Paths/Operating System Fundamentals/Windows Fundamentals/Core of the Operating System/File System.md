### Introduction
- **Types of Windows File Systems:**
    - Five types: FAT12, FAT16, FAT32, NTFS, and exFAT. FAT12 and FAT16 are outdated.
    - Focus will be on **FAT32** and **NTFS**.
- **FAT32:**
    - Common on USB drives and SD cards; also used for hard drives.
    - **Pros:**
        - Highly compatible with devices (computers, cameras, smartphones, etc.).
        - Works on Windows, macOS, and Linux.
    - **Cons:**
        - Limited to files smaller than 4GB.
        - No built-in data protection or file compression.
        - Requires third-party tools for encryption.
- **NTFS:**
    - Default file system for Windows since NT 3.1, offering better performance and metadata support.
    - **Pros:**
        - Reliable with built-in recovery features after system failure.
        - Supports detailed permissions for files and folders.
        - Handles large partitions and has journaling.
    - **Cons:**
        - Not widely supported on mobile and older media devices (e.g., TVs, cameras).



### Permissions
- The NTFS file system has many basic and advanced permissions. 
- Some of the key permission types are shown below.
![[Screenshot_20241109_113730.png]]
- Files and folders inherit the NTFS permissions of their parent folder for ease of administration, so administrators do not need to explicitly set permissions for each file and folder, as this would be extremely time-consuming.
- If permissions do need to be set explicitly, an administrator can disable permissions inheritance for the necessary files and folders and then set the permissions directly on each.



### Integrity Control Access Control List (icacls)
- NTFS permissions on files and folders in Windows can be managed using the File Explorer GUI under the security tab. 
- Apart from the GUI, we can also achieve a fine level of granularity over NTFS file permissions in Windows from the command line using the icacls utility.
- We can list out the NTFS permissions on a specific directory by running either `icacls` from within the working directory or `icacls C:\Windows` against a directory not currently in.
```cmd-session
C:\htb> icacls c:\windows
c:\windows NT SERVICE\TrustedInstaller:(F)
           NT SERVICE\TrustedInstaller:(CI)(IO)(F)
           NT AUTHORITY\SYSTEM:(M)
           NT AUTHORITY\SYSTEM:(OI)(CI)(IO)(F)
           BUILTIN\Administrators:(M)
           BUILTIN\Administrators:(OI)(CI)(IO)(F)
           BUILTIN\Users:(RX)
           BUILTIN\Users:(OI)(CI)(IO)(GR,GE)
           CREATOR OWNER:(OI)(CI)(IO)(F)
           APPLICATION PACKAGE AUTHORITY\ALL APPLICATION PACKAGES:(RX)
           APPLICATION PACKAGE AUTHORITY\ALL APPLICATION PACKAGES:(OI)(CI)(IO)(GR,GE)
           APPLICATION PACKAGE AUTHORITY\ALL RESTRICTED APPLICATION PACKAGES:(RX)
           APPLICATION PACKAGE AUTHORITY\ALL RESTRICTED APPLICATION PACKAGES:(OI)(CI)(IO)(GR,GE)

Successfully processed 1 files; Failed processing 0 files
```
- The resource access level is listed after each user in the output. 
- The possible inheritance settings are:
	- `(CI)`: container inherit
	- `(OI)`: object inherit
	- `(IO)`: inherit only
	- `(NP)`: do not propagate inherit
	- `(I)`: permission inherited from parent container
- In the above example, the `NT AUTHORITY\SYSTEM` account has object inherit, container inherit, inherit only, and full access permissions. 
- This means that this account has full control over all file system objects in this directory and subdirectories.
- Basic access permissions are as follows:
	- `F` : full access
	- `D` :  delete access
	- `N` :  no access
	- `M` :  modify access
	- `RX` :  read and execute access
	- `R` :  read-only access
	- `W` :  write-only access
- We can add and remove permissions via the command line using `icacls`. 
- Here we are executing `icacls` in the context of a local administrator account showing the `C:\users` directory where the `joe` user does not have any write permissions.
```cmd-session
C:\htb> icacls c:\Users
c:\Users NT AUTHORITY\SYSTEM:(OI)(CI)(F)
         BUILTIN\Administrators:(OI)(CI)(F)
         BUILTIN\Users:(RX)
         BUILTIN\Users:(OI)(CI)(IO)(GR,GE)
         Everyone:(RX)
         Everyone:(OI)(CI)(IO)(GR,GE)

Successfully processed 1 files; Failed processing 0 files
```
- Using the command `icacls c:\users /grant joe:f` we can grant the joe user full control over the directory, but given that `(oi)` and `(ci)` were not included in the command, the joe user will only have rights over the `c:\users` folder but not over the user subdirectories and files contained within them.
```cmd-session
C:\htb> icacls c:\users /grant joe:f
processed file: c:\users
Successfully processed 1 files; Failed processing 0 files
```
```cmd-session
C:\htb> >icacls c:\users
c:\users WS01\joe:(F)
         NT AUTHORITY\SYSTEM:(OI)(CI)(F)
         BUILTIN\Administrators:(OI)(CI)(F)
         BUILTIN\Users:(RX)
         BUILTIN\Users:(OI)(CI)(IO)(GR,GE)
         Everyone:(RX)
         Everyone:(OI)(CI)(IO)(GR,GE)

Successfully processed 1 files; Failed processing 0 files
```
- These permissions can be revoked using the command `icacls c:\users /remove joe`.
- `icacls` is very powerful and can be used in a domain setting to give certain users or groups specific permissions over a file or folder, explicitly deny access, enable or disable inheritance permissions, and change directory/file ownership.
- A full listing of `icacls` command-line arguments and detailed permission settings can be found [here](https://ss64.com/nt/icacls.html).



### Questions
- What system user has full control over the c:\users directory?
	- bob.smith