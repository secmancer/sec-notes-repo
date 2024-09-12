**Solaris Overview**
- **Developer**: Originally Sun Microsystems, later acquired by Oracle Corporation.
- **Release**: 1990s.
- **Purpose**: Designed for robustness, scalability, and high-end hardware and software systems.
- **Use Cases**: Enterprise environments for mission-critical applications (e.g., database management, cloud computing, virtualization).

**Key Features**
- **Built-in Hypervisor**: Oracle VM Server for SPARC allows running multiple virtual machines on a single physical server.
- **High Availability**: Built-in features for fault tolerance and system management.
- **Security**: Role-Based Access Control (RBAC), mandatory access controls.
- **Scalability**: Handles large data volumes effectively, suitable for large-scale data centers and cloud environments.

**Solaris vs. Linux Distributions**
1. **Source Code**
    - **Solaris**: Proprietary, source code not publicly available.
    - **Linux**: Open-source, source code is accessible and modifiable.
2. **Filesystem**
    - **Solaris**: Uses Zettabyte File System (ZFS) with features like data compression, snapshots.
    - **Linux**: May use various filesystems; ZFS is available on some distributions.
3. **Service Management**
    - **Solaris**: Service Management Facility (SMF) for managing system services.
    - **Linux**: Uses various systems like systemd or init.d.
4. **Package Management**
    - **Solaris**: Uses Image Packaging System (IPS) and Solaris Package Manager (SPM).
    - **Linux**: Typically uses APT, YUM, or other package managers.
5. **Permission Management**
    - **Solaris**: Uses RBAC for granular permissions; sudo supported since Solaris 11.
    - **Linux**: Uses traditional permission systems with chmod and sudo.
6. **Process Mapping**
    - **Solaris**: `pfiles` command lists files opened by a process.
    - **Linux**: `lsof` command serves a similar function.
7. **System Information**
    - **Solaris**: `showrev` provides detailed system info.
    - **Linux**: `uname -a` provides basic system info.
8. **NFS Configuration**
    - **Solaris**: `share` command for NFS sharing; configuration in `/etc/dfs/dfstab`.
    - **Linux**: Uses `exportfs` for sharing and `/etc/exports` for configuration.
9. **Executable Access**
    - **Solaris**: `truss` for tracing system calls.
    - **Linux**: `strace` for similar functionality.

![[Screenshot_20240912_150431.png]]

**Directory Structure in Solaris**
- `/` : Root directory containing all others.
- `/bin` : Essential system binaries.
- `/boot` : Boot-related files.
- `/dev` : Device files.
- `/etc` : Configuration files.
- `/home` : Users' home directories.
- `/kernel` : Kernel modules and files.
- `/lib` : Libraries for binaries.
- `/lost+found` : Recovered files from file system checks.
- `/mnt` : Temporary file system mounts.
- `/opt` : Optional software packages.
- `/proc` : Process and kernel status.
- `/sbin` : System administration binaries.
- `/tmp` : Temporary files.
- `/usr` : System-wide read-only data and programs.
- `/var` : Variable data (logs, mail, printer spools).

**Notable Differences**
- **Source Code Availability**: Solaris is proprietary; Linux is open-source.
- **Package Management**: Solaris uses IPS; Linux distributions use APT, YUM, etc.
- **Permission Systems**: Solaris uses RBAC; Linux uses traditional permissions with sudo.


**Example Commands**
- **System Information**
    - Solaris: `showrev -a`
    - Linux: `uname -a`
- **Package Installation**
    - Solaris: `pkgadd -d SUNWapchr`
    - Linux: `sudo apt-get install apache2`
- **File Permission Search**
    - Solaris: `find / -perm -4000`
    - Linux: `find / -perm 4000`
- **NFS Sharing**
    - Solaris: `share -F nfs -o rw /export/home`
    - Linux: `exportfs -o rw /export/home`
- **Process File List**
    - Solaris: `pfiles \`pgrep httpd``
    - Linux: `lsof -c apache2`
- **System Call Tracing**
    - Solaris: `truss ls`
    - Linux: `strace -p \`pgrep apache2``