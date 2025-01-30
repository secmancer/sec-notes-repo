### **1. Windows File Systems**
- There are **five** types of Windows file systems, but only **FAT32, exFAT, and NTFS** are commonly used today.



### **FAT32 (File Allocation Table 32)**
- **Pros:**
    - **Highly compatible** – Works on Windows, macOS, Linux, game consoles, and cameras.
    - **Supports external devices** – USB drives, SD cards.
- **Cons:**
    - **File size limit:** Maximum **4GB per file**.
    - **Lacks security features** (no encryption, no granular permissions).
    - **No journaling**, making data recovery harder after crashes.



### **NTFS (New Technology File System)**
- **Pros:**
    - **More reliable** – Auto-repairs after system crashes.
    - **Granular file/folder permissions** for security.
    - **Supports large partitions** and file sizes.
    - **Journaling system** logs all file changes.
- **Cons:**
    - **Not fully supported by mobile devices and older hardware**.



### **2. NTFS Permissions**

|**Permission Type**|**Description**|
|---|---|
|**Full Control**|Read, write, modify, delete files/folders.|
|**Modify**|Read, write, and delete files/folders.|
|**List Folder Contents**|View folder contents (folders only).|
|**Read & Execute**|View/list files, execute files.|
|**Write**|Add files/folders, edit files.|
|**Read**|View files and folders.|
|**Traverse Folder**|Allows users to access files inside folders they don't have explicit permissions for.|

- **Inheritance:**
    - Files/folders inherit NTFS permissions from their **parent directory**.
    - **Admins can disable inheritance** to manually set permissions.



### **3. Managing NTFS Permissions via `icacls`**
- **`icacls`** is a command-line tool for viewing, modifying, and managing NTFS permissions.



### **Viewing NTFS Permissions**
```cmd
icacls C:\Windows
```
- **Example Output:**
```txt
C:\Windows NT SERVICE\TrustedInstaller:(F)
           NT AUTHORITY\SYSTEM:(M)
           BUILTIN\Administrators:(M)
           BUILTIN\Users:(RX)
```
- **Inheritance Flags:**
    - `(CI)` – Container Inherit (affects subfolders).
    - `(OI)` – Object Inherit (affects files).
    - `(IO)` – Inherit Only (applies only to child objects).
- **Basic Access Permissions:**
    - `F` – Full Control
    - `M` – Modify
    - `RX` – Read & Execute
    - `R` – Read-only
    - `W` – Write



### **4. Modifying NTFS Permissions**
- #### **Grant Full Control to a User**
```cmd
icacls C:\Users /grant joe:F
```
- **Gives "joe" full control** over `C:\Users` (but not its subdirectories).
- #### **Revoke Permissions from a User**
```cmd
icacls C:\Users /remove joe
```
- #### **Grant Full Control with Inheritance**
```cmd
icacls C:\Users /grant joe:(OI)(CI)F
```
- **(OI) & (CI) ensure permissions apply to all subfolders and files.**



### **Key Takeaways**
-  **FAT32 is widely compatible** but lacks security features.  
- **NTFS is the default Windows file system** with **granular permissions and journaling**.  
- **`icacls`** is a powerful command for **modifying NTFS permissions** via the command line.  
- **Permissions can be inherited**, but admins can **disable inheritance** for stricter control.



### Questions
- What system user has full control over the c:\users directory?
	- bob.smith