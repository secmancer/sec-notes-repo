### **1. Windows File System Overview**
	- **Root Directory**: `<drive_letter>:\` (e.g., `C:\`).
	- **Boot Partition**: Where the OS is installed.
	- Other drives: **Physical & virtual** (e.g., `E:\` for data storage).
- #### **Key Directories in Windows**

|**Directory**|**Function**|
|---|---|
|**Perflogs**|Stores Windows performance logs (empty by default).|
|**Program Files**|Stores 64-bit applications on 64-bit systems; 32-bit apps on 32-bit systems.|
|**Program Files (x86)**|Stores **32-bit applications** on 64-bit systems.|
|**ProgramData**|Hidden folder containing essential application data (accessible to all users).|
|**Users**|Stores user profiles (`C:\Users\`), including `Public` and `Default` folders.|
|**Default**|Template for newly created user profiles.|
|**Public**|Shared folder accessible to all users (network-shared by default).|
|**AppData**|Stores per-user application data (`C:\Users\<user>\AppData`). Contains:|
|**AppData\Roaming**|**Machine-independent** data (e.g., browser settings, custom dictionaries).|
|**AppData\Local**|**Machine-specific** data (not synced across the network).|
|**AppData\LocalLow**|Similar to `Local`, but **lower integrity level** (e.g., for protected browser mode).|
|**Windows**|Contains core OS files.|
|**System, System32, SysWOW64**|Stores DLLs for Windows core features & API.|
|**WinSxS**|Windows Component Store (contains OS updates, service packs, and backup copies of system files).|



### **2. Exploring Directories via Command Line**
- #### **Listing Files & Directories (`dir`)**
```cmd
dir C:\ /a
```
- **Example Output:**
```txt
 Volume in drive C has no label.
 Volume Serial Number is F416-77BE

 Directory of C:\

08/16/2020  10:33 AM    <DIR>          $Recycle.Bin
08/24/2020  10:38 AM    <DIR>          Program Files
07/09/2020  06:08 PM    <DIR>          Program Files (x86)
08/24/2020  10:41 AM    <DIR>          ProgramData
08/16/2020  10:33 AM    <DIR>          Users
08/17/2020  11:38 PM    <DIR>          Windows
               7 File(s) 51,190,943,590 bytes
              13 Dir(s)  261,310,697,472 bytes free
```



### **3. Displaying Directory Structure (`tree`)**
- #### **Basic Usage**
```cmd
tree "C:\Program Files (x86)\VMware"
```
- **Example Output (Partial):**
```txt
C:\PROGRAM FILES (X86)\VMWARE
├───VMware VIX
│   ├───doc
│   ├───samples
│   └───Workstation-15.0.0
│       ├───32bit
│       └───64bit
└───VMware Workstation
    ├───env
    ├───hostd
    ├───messages
    ├───OVFTool
    ├───Resources
    ├───tools-upgraders
    └───x64
```



### **Display Full File Structure**
```cmd
tree C:\ /f | more
```
- **`/f`** → Includes files in the directory structure.
- **`| more`** → Displays results **one screen at a time**.



### **Key Takeaways**
- Windows **file system structure** is critical for **navigation & security assessments**.  
- `dir` and `tree` commands **help explore directories efficiently**.  
- Understanding **system folders** helps locate **user data, application logs, and OS files**.



### Questions
- Find the non-standard directory in the C drive. Submit the contents of the flag file saved in this directory.
	- c8fe8d977d3a0c655ed7cf81e4d13c75