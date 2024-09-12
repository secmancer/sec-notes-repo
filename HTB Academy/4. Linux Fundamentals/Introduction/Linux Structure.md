- **Unix Operating System (1970)**
    - Released by Ken Thompson and Dennis Ritchie at AT&T.
- **Berkeley Software Distribution (BSD) (1977)**
    - Released but limited by a lawsuit due to Unix code ownership.
- **GNU Project (1983)**
    - Started by Richard Stallman to create a free Unix-like OS.
    - Resulted in the creation of the GNU General Public License (GPL).
- **Linux Kernel (1991)**
	- Personal project by Linus Torvalds, aiming to create a free OS kernel.
	- Evolved from a small project to over 23 million lines of code.
	- Licensed under GNU General Public License v2.
### Linux Distributions
- **Examples of Popular Distributions:**
    - Ubuntu
    - Debian
    - Fedora
    - OpenSUSE
    - elementary OS
    - Manjaro
    - Gentoo Linux
    - RedHat
    - Linux Mint

![[Screenshot_20240912_120418.png]]
### Key Characteristics
- **Security:** Generally considered more secure than other OSes, less susceptible to malware.
- **Updates:** Frequently updated, stable, and high-performance.
- **Difficulty:** Can be challenging for beginners; fewer hardware drivers compared to Windows.
- **Flexibility:** Free and open-source; source code can be modified and distributed.

![[Screenshot_20240912_120427.png]]

![[Screenshot_20240912_120435.png]]
### Linux Architecture
- **Bootloader:** Guides the booting process (e.g., GRUB Bootloader in Parrot Linux).
- **OS Kernel:** Manages system resources and hardware (e.g., Linux kernel).
- **Daemons:** Background services for key functions (e.g., scheduling, printing).
- **OS Shell:** Interface for user commands (e.g., Bash, Tcsh/Csh, Ksh, Zsh, Fish).
- **Graphics Server:** Provides graphical subsystem (e.g., X-server).
- **Window Manager:** GUI options like GNOME, KDE, MATE, Unity, Cinnamon.
- **Utilities:** Programs performing specific functions.

### Linux Layers
1. **Hardware:** System's peripherals (RAM, hard drive, CPU).
2. **Kernel:** Core component managing resources and processes.
3. **Shell:** Command-line interface for user commands.
4. **System Utility:** Provides OS functionality to the user.

![[Screenshot_20240912_120445.png]]
![[Screenshot_20240912_120516.png]]

### File System Hierarchy
- **/** (Root): Top-level directory containing all system files and mounted filesystems.
- **/bin:** Essential command binaries.
- **/boot:** Static bootloader, kernel executable, and boot files.
- **/dev:** Device files for hardware access.
- **/etc:** Local system configuration files.
- **/home:** User home directories.
- **/lib:** Shared library files required for system boot.
- **/media:** Mount point for external removable media.
- **/mnt:** Temporary mount point for filesystems.
- **/opt:** Optional files, third-party tools.
- **/root:** Home directory for the root user.
- **/sbin:** System administration executables.
- **/tmp:** Temporary files, cleared upon boot.
- **/usr:** Executables, libraries, man files.
- **/var:** Variable data files (logs, email, web files).