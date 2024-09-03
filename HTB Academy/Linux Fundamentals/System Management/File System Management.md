File system management on Linux involves organizing and maintaining data on storage devices. Linux supports various file systems such as ext2, ext3, ext4, XFS, Btrfs, and NTFS. The choice of file system depends on specific needs:

- **ext2/ext3/ext4**: Commonly used, with ext4 offering journaling and improved performance.
- **XFS**: Known for high performance with large files.
- **Btrfs**: Provides advanced features like snapshots and data integrity.
- **NTFS**: Useful for compatibility with Windows systems.

**File System Hierarchy**

The Linux file system is hierarchical and based on the Unix file system. It is organized as follows:

- **Inodes**: Metadata structures that store information about files and directories, including permissions, size, and ownership.
- **Regular Files**: Standard files stored in directories.
- **Directories**: Containers for files and other directories.
- **Symbolic Links**: References to other files or directories.

**File System Permissions**

Permissions control access to files and directories. Each file or directory has read, write, and execute permissions that apply to the owner, group, and others.

**Disk Management**

Disk management involves handling physical storage devices and their partitions. Tools for disk management include:

- **fdisk**: Creates, deletes, and manages partitions.
- **gparted**: A graphical partition editor.
- **GParted**: A graphical partition manager.

Commands:

- **List Partitions**: `sudo fdisk -l`

**Mounting and Unmounting**

Mounting attaches a file system to a directory, making it accessible. Unmounting detaches it.

- **Mounting**: `sudo mount /dev/sdb1 /mnt/usb`
- **Unmounting**: `sudo umount /mnt/usb`

To view mounted file systems, use:

- `mount`

The `/etc/fstab` file lists file systems to be mounted at boot time.

**Automatic Mounting**

To mount file systems automatically at boot, entries are made in `/etc/fstab`. For example:\
	- /dev/sda1 / ext4 defaults 0 0
	- /dev/sda2 /home ext4 defaults 0 0
	- /dev/sdb1 /mnt/usb ext4 rw,noauto,user 0 0

**Swap Space**

Swap space extends physical memory by providing additional virtual memory. It helps manage memory when physical RAM is exhausted and can be used for hibernation.

Commands:

- **Create Swap Space**: `mkswap /dev/sdX`
- **Activate Swap Space**: `swapon /dev/sdX`
- **View Swap Usage**: `swapon --show`

Swap space should be placed on a dedicated partition or file, and encrypting swap space can enhance security.

**Conclusion**

Proper file system management ensures efficient and secure data handling on Linux systems. By choosing the right file system and effectively managing disks, mounting, and swap space, you can optimize your Linux environment.