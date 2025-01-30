### Overview of Linux File Systems
- **Purpose**: Organize, store, and maintain data on storage devices.
- **Supported File Systems**:
  - **ext2**: Older, no journaling (e.g., USB drives).
  - **ext3/ext4**: Journaling, reliable, default for modern Linux systems.
  - **Btrfs**: Advanced features like snapshots and data integrity checks.
  - **XFS**: High performance, ideal for large files and high I/O environments.
  - **NTFS**: Compatibility with Windows systems.



### Key Components of Linux File Systems
1. **Inodes**:
   - **Purpose**: Store metadata about files (permissions, ownership, size, timestamps).
   - **Inode Table**: Database of inodes used by the kernel to manage files.
   - **Analogy**: Like index cards in a library catalog.
2. **File Types**:
   - **Regular Files**: Contain text or binary data.
   - **Directories**: Containers for files and subdirectories.
   - **Symbolic Links (Symlinks)**: Shortcuts to files or directories.



### Disk and Partition Management
- **Tools**:
  - **fdisk**: Create, delete, and manage partitions.
  - **gparted**: Graphical tool for disk partitioning.
- **Commands**:
  - List partitions:
    ```bash
    sudo fdisk -l
    ```
  - Create partitions:
    ```bash
    sudo fdisk /dev/sdX
    ```
  - Format partitions:
    ```bash
    sudo mkfs.ext4 /dev/sdX1
    ```



### Mounting File Systems
- **Purpose**: Link partitions or drives to directories in the file system hierarchy.
- **Commands**:
  - Mount a file system:
    ```bash
    sudo mount /dev/sdX1 /mnt/mount_point
    ```
  - Unmount a file system:
    ```bash
    sudo umount /mnt/mount_point
    ```
  - List mounted file systems:
    ```bash
    mount
    ```
- **Automount at Boot**:
  - Edit `/etc/fstab`:
    ```bash
    /dev/sdX1 /mnt/mount_point ext4 defaults 0 0
    ```



### Swap Space Management
- **Purpose**: Extend RAM by moving inactive memory pages to disk.
- **Commands**:
  - Create swap space:
    ```bash
    sudo mkswap /dev/sdX2
    ```
  - Enable swap space:
    ```bash
    sudo swapon /dev/sdX2
    ```
  - Disable swap space:
    ```bash
    sudo swapoff /dev/sdX2
    ```
- **Hibernation**: Swap space stores system state for power-saving.



### Practical Examples
1. **Mounting a USB Drive**:
   - Identify the USB device:
     ```bash
     sudo fdisk -l
     ```
   - Mount the USB drive:
     ```bash
     sudo mount /dev/sdb1 /mnt/usb
     ```
   - Unmount the USB drive:
     ```bash
     sudo umount /mnt/usb
     ```

2. **Checking Open Files**:
   - List open files on a mount point:
     ```bash
     lsof | grep /mnt/usb
     ```

3. **Automating Mounts**:
   - Add to `/etc/fstab`:
     ```bash
     /dev/sdb1 /mnt/usb ext4 rw,noauto,user 0 0
     ```



### Summary
- **File Systems**: Choose based on performance, reliability, and use case.
- **Inodes**: Manage file metadata efficiently.
- **Disk Management**: Use tools like `fdisk` and `gparted` for partitioning.
- **Mounting**: Link partitions to directories for access.
- **Swap Space**: Extend RAM and support hibernation.



### Questions
- How many partitions exist in our Pwnbox? (Format: 0)
	- 3