### **macOS System Hierarchy - Notes**
-  macOS follows a **Unix-based filesystem structure**, dividing files into different **domains and directories** for security and organization.



### **1. macOS Domains**
- Files are grouped into **domains**, each with different privileges and access controls.

|**Domain**|**Description**|
|---|---|
|**Local Domain**|Apps/resources shared by all users on the Mac.|
|**System Domain**|System software installed by Apple.|
|**User Domain**|User-specific files and settings (Home directory).|
|**Network Domain**|Files shared over a local network.|



### **2. macOS File System Structure**
- #### **/Applications (App Installations)**

|**Domain**|**Location**|**Purpose**|
|---|---|---|
|**User**|`/Users/username/Applications`|Apps installed for a specific user.|
|**Local**|`/Applications`|Apps installed for all users.|
|**System**|`/System/Applications`|System apps (installed by Apple).|

- #### **/Users (User Data)**
	- Contains **user accounts and personal data**.
	- Each user has a **separate home directory**:
    ```bash
    /Users/htb-student
    /Users/htb-dev
    ```
	- Users **cannot access each other's home folders**.
- #### **/Library (Application Support & Configurations)**

|**Domain**|**Location**|**Purpose**|
|---|---|---|
|**User**|`/Users/username/Library`|Stores user-specific app settings.|
|**Local**|`/Library`|Shared app settings across all users.|
|**System**|`/System/Library`|System-related libraries (not user-modifiable).|

- **Important Subdirectories in /Library:**
	- `/Library/Application Support` – App-specific support & config files.
	- `/Library/Caches` – Temporary app data caches.
	- `/Library/Frameworks` – Libraries for app development.
	- `/Library/Preferences` – App preferences/settings.
- #### **/Network (Shared Network Resources)**
	- Contains **files shared over a local network**.
	- Lists connected **Macs and shared resources**.
- #### **/System (Core macOS Files)**
	- **Stores critical system files & OS components.**
	- Files here **should not be modified manually**.



### **3. Unix-Specific Directories in macOS**

|**Directory**|**Purpose**|
|---|---|
|**`/` (Root)**|Contains everything needed for the OS to function.|
|**`/bin`**|Stores essential system binaries (commands like `ls`, `cp`).|
|**`/dev`**|Contains device files (e.g., USB, disks).|
|**`/etc`**|Stores **system configuration files**.|
|**`/sbin`**|Contains **administrative binaries** (e.g., `shutdown`, `fsck`).|
|**`/tmp`**|Stores **temporary files**, cleared on reboot.|
|**`/usr`**|Contains **user applications, libraries, and system utilities**.|
|**`/var`**|Stores **system logs, web server files, backups**.|
|**`/private`**|Contains **critical system files and caches** (hidden by default).|
|**`/opt`**|Stores **third-party software and packages**.|
|**`/cores`**|Stores **core dumps for debugging**.|
|**`/home`**|Stores **user home directories** (alternative to `/Users`).|



### **4. Exploring macOS Directories**
- Use `ls` to list files:
    ```bash
    ls /
    ```
- Use `cd` to navigate:
    ```bash
    cd /Users
    ```
- Use `man hier` to get more information about the directory structure.



### **Key Takeaways**
- **macOS follows a Unix-like file system** with **User, Local, System, and Network Domains**.
- **Important directories** include `/Applications`, `/Users`, `/Library`, `/System`, `/var`, and `/etc`.
- **System files should not be modified manually** (especially in `/System` and `/private`).
- **Use `man hier`** for more details on Unix directory structure.



### Questions
- Where are the Applications related to the system stored at?
	- /System/Applications