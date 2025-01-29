### **Solaris Overview**
- **Developer:** Sun Microsystems (acquired by Oracle)
- **Type:** Unix-based OS
- **Key Features:**
    - **Robustness** and **scalability**: Designed for enterprise environments handling large-scale data and mission-critical applications.
    - **Support for high-end hardware**: Used in complex network infrastructures and large data centers.
    - **Built-in hypervisor**: Oracle VM Server for SPARC for running multiple virtual machines.
    - **Security**: Role-Based Access Control (RBAC) and mandatory access controls for better system protection.
    - **Package Management**: Uses **Image Packaging System (IPS)** for managing packages and updates.
    - **Fault tolerance** and **high availability** for mission-critical applications.
- **Usage:** Widely adopted in sectors like banking, finance, government, and large data centers. 



### **Solaris vs. Linux Distributions**
1. **Ownership**:
    - Solaris is proprietary (owned by Oracle).
    - Linux distributions are open-source.
2. **File Systems**:
    - **Solaris** uses **ZFS** for advanced file system features.
    - **Linux** distributions commonly use ext4 or other file systems.
3. **Service Management**:
    - **Solaris** has the **Service Management Facility (SMF)** for improved service management.
    - **Linux** uses **systemd** (in most distributions).
4. **Package Management**:
    - **Solaris** uses **pkgadd** and **Image Packaging System (IPS)**.
    - **Linux** uses package managers like **apt** (for Debian-based) or **yum/dnf** (for Red Hat-based).
5. **Security**:
    - **Solaris** includes advanced security tools like **RBAC** and mandatory access controls.
    - **Linux** has AppArmor and SELinux.



### **Solaris Directory Structure**

| **Directory** | **Description**                                    |
| ------------- | -------------------------------------------------- |
| `/`           | Root directory, contains all other files.          |
| `/bin`        | Essential system binaries.                         |
| `/boot`       | Boot-related files.                                |
| `/dev`        | Device files for physical and logical devices.     |
| `/etc`        | System configuration files.                        |
| `/home`       | User home directories.                             |
| `/kernel`     | Kernel-related files.                              |
| `/lib`        | System libraries.                                  |
| `/lost+found` | Recovered files after a file system check.         |
| `/mnt`        | Temporary mount points for file systems.           |
| `/opt`        | Optional software packages.                        |
| `/proc`       | Process and kernel status information.             |
| `/sbin`       | System binaries for administration.                |
| `/tmp`        | Temporary files.                                   |
| `/usr`        | System-wide read-only data (programs, libraries).  |
| `/var`        | Variable data like logs, mail, and printer spools. |



### **Solaris Administration Tools & Commands**
1. **System Info**:
    - `showrev -a`: Displays detailed system info (e.g., Solaris version, hardware).
    - Example output: `Kernel version: SunOS 5.10 Generic_139555-08`
2. **Package Management**:
    - `pkgadd -d SUNWapchr`: Install packages in Solaris.
3. **Permissions**:
    - `chmod 700 filename`: Change file permissions.
    - `find / -perm 4000`: Find files with the SUID bit set (Linux).
    - `find / -perm -4000`: Same for Solaris (use `-` before permissions).
4. **NFS**:
    - Share directory: `share -F nfs -o rw /export/home`
    - Mount NFS: `mount -F nfs 10.129.15.122:/nfs_share /mnt/local`
    - NFS config: `/etc/dfs/dfstab`
5. **Process Management**:
    - `pfiles`: List files opened by a process in Solaris (like `lsof` in Linux).
6. **System Call Tracing**:
    - **Solaris**: `truss` (for tracing system calls).
    - **Linux**: `strace` (for tracing system calls).