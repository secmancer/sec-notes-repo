### **Overview of Linux**
- **What is Linux?**  
    Linux is an open-source operating system kernel. It forms the basis for many distributions (distros) that cater to different needs. It's flexible, secure, and powerful, widely used in servers, desktops, and embedded systems.



### **History of Linux**
- **Unix Origins**: The story starts in 1970 with Unix, developed by Ken Thompson and Dennis Ritchie. This eventually led to the Berkeley Software Distribution (BSD) and the GNU project started by Richard Stallman in 1983, aiming to create a free Unix-like OS.
- **Linus Torvalds & the Linux Kernel**: In 1991, Linus Torvalds, a Finnish student, created the first version of the Linux kernel. Over time, it evolved into the robust and widely-used system it is today, licensed under the GNU General Public License (GPL).
- **Linux's Reach**: With over 600 distributions, Linux runs everything from servers to smartphones (Android).



### **Linux Philosophy**
- **Core Principles**:
    - **Everything is a file**: Configuration and data files are text-based.
    - **Small, single-purpose programs**: Tools are designed to perform specific tasks and can be combined to create complex solutions.
    - **Avoid captive UIs**: Linux focuses on command-line interaction, which provides more control.
    - **Configuration via text files**: Configuration files like `/etc/passwd` store user info.
- **Core Components**:
    - **Bootloader**: Manages the OS boot process (e.g., GRUB in Parrot OS).
    - **Kernel**: The heart of the OS, managing hardware resources.
    - **Daemons**: Background services (e.g., cron jobs).
    - **Shell**: Command-line interface for interacting with the OS (e.g., Bash).
    - **Graphics Server**: Manages graphical displays (e.g., X server).
    - **Window Manager**: Manages GUI (e.g., GNOME, KDE).
    - **Utilities**: Software tools that perform specific functions.



### **Linux Architecture**
- Linux operates in a layered structure:
	1. **Hardware**: Physical devices like CPU, RAM, and storage.
	2. **Kernel**: Manages resources, providing isolation between processes.
	3. **Shell**: Command-line interface for user input.
	4. **System Utility**: Provides system functionality to users.



### **File System Hierarchy (FHS)**
- The Linux file system is hierarchical and follows the FHS, structured as:
	- **`/`**: Root directory (all files stem from here).
	- **`/bin`**: Essential command binaries.
	- **`/boot`**: Files needed to boot the OS.
	- **`/dev`**: Device files (e.g., hard drives, printers).
	- **`/etc`**: Configuration files for the system.
	- **`/home`**: User home directories.
	- **`/lib`**: Shared libraries needed for system boot.
	- **`/media`**: Mounted removable media.
	- **`/mnt`**: Temporary mount points.
	- **`/opt`**: Optional software packages.
	- **`/root`**: Root user's home directory.
	- **`/sbin`**: System administration binaries.
	- **`/tmp`**: Temporary files.
	- **`/usr`**: User programs and libraries.
	- **`/var`**: Variable data files (logs, emails, etc.)