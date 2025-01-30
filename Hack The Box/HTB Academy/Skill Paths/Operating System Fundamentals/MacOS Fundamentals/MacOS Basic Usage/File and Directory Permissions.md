### **File and Directory Permissions in macOS - Notes**
- macOS **inherits Unix-style permissions**, making **file and folder management** more secure and structured. Below are the key concepts, commands, and GUI methods for handling permissions in macOS.



### **1. Understanding File Permissions**
- #### **Basic File Permission Structure (`ls -l` Output)**
```bash
secmancer@htb[/htb]$ ls -l  
-rw- r-- r--@  1 htb-user staff 2512910 Aug 30  2019 HTB-Wallpaper-1.png
```
- **Breakdown of Output:**

|**Section**|**Meaning**|
|---|---|
|`-rw- r-- r--`|File type & permissions (User/Group/Others).|
|`1`|Number of **hard links**.|
|`htb-user`|**User Owner** of the file.|
|`staff`|**Group Owner** of the file.|
|`2512910`|File size in bytes.|
|`Aug 30 2019`|**Last modified date**.|
|`HTB-Wallpaper-1.png`|**File name**.|

- ### **Permission Breakdown (`UGO` - User, Group, Others)**

|**Permission**|**Symbol**|**Octal Value**|
|---|---|---|
|**Read**|`r`|`4`|
|**Write**|`w`|`2`|
|**Execute**|`x`|`1`|

- To **calculate permissions**, sum the octal values:
	- `rwx` (Read, Write, Execute) = **7**
	- `rw-` (Read, Write) = **6**
	- `r--` (Read-only) = **4**



### **2. Modifying Permissions in macOS**
- #### **GUI Method (Finder)**
	1. **Right-click** the file/folder.
	2. Select **"Get Info"** (`Command + Option + I` shortcut).
	3. Click the **lock icon** (bottom-right) and **authenticate**.
	4. Under **"Sharing & Permissions"**, modify user permissions.
	5. Click the **"+"** to add a user or **"-"** to remove a user.



### **3. Managing Permissions Using Terminal (`chmod` & `chown`)**
- #### **Change File Permissions (`chmod`)**
- Syntax:
```bash
chmod [mode] [file/folder]
```
- Example:
```bash
chmod 777 HTB-Wallpaper-1.png
```
- **Explanation:**
	- `777` sets **full permissions** (`rwxrwxrwx`) for User, Group, and Others.
	- `644` (default for files) sets **read/write for owner, read-only for others** (`rw-r--r--`).
- To view permission changes:
```bash
ls -l
```



### **Change File Ownership (`chown`)**
- Syntax:
```bash
sudo chown [new_owner] [file/folder]
```
- Example:
```bash
sudo chown htb-student HTB-Wallpaper-1.png
```
- **Before:**
```bash
-rwxrwxrwx@ 1 htb-user staff 2512910 Aug 30 2019 HTB-Wallpaper-1.png
```
- **After:**
```bash
-rwxrwxrwx@ 1 htb-student staff 2512910 Aug 30 2019 HTB-Wallpaper-1.png
```



### **Change File Group Ownership (`chown` & `chgrp`)**
- Syntax:
```bash
sudo chown [user]:[group] [file/folder]
```
- Example:
```bash
sudo chown htb-user:admins HTB-Wallpaper-1.png
```
- OR
```bash
sudo chgrp admins HTB-Wallpaper-1.png
```
- **Before:**
```bash
-rwxrwxrwx@ 1 htb-user staff 2512910 Aug 30 2019 HTB-Wallpaper-1.png
```
- **After:**
```bash
-rwxrwxrwx@ 1 htb-user admins 2512910 Aug 30 2019 HTB-Wallpaper-1.png
```



### **4. Key Takeaways**
- **Permissions are based on User, Group, and Others (`UGO`).**
- **Use Finder’s GUI for simple permission changes** (Right-click → "Get Info").
- **Use `chmod` to modify file permissions** (e.g., `chmod 755 file`).
- **Use `chown` to change file ownership** (`chown user file`).
- **Use `chgrp` or `chown user:group` to change group ownership**.



### Questions
- If a file has a permission set of "rw-rw-rw-" applied, what would that equal in Octal format? (number only)
	- 666