**File System Types**: Linux supports various file systems, including:
- **ext2**: Basic file system; lacks journaling.
- **ext3**: Extends ext2 with journaling.
- **ext4**: Advanced version of ext3 with improved performance and features.
- **XFS**: High-performance file system for large files and volumes.
- **Btrfs**: Offers advanced features like snapshots and data integrity checks.
- **NTFS**: Used for compatibility with Windows systems.
**Selecting a File System**:
- **ext2**: Suitable for simple tasks.
- **Btrfs**: Ideal for advanced features like snapshots and data integrity.
- **NTFS**: Necessary for compatibility with Windows.


#### Linux File System Structure
- **Inode Table**:
    - Contains metadata for files and directories (permissions, size, type, owner).
    - Acts as a database for file management.
- **File Types**:
    - **Regular Files**: Standard files stored in the file system.
    - **Directories**: Containers for files, organizing them hierarchically.
    - **Symbolic Links**: Shortcuts or references to other files or directories.
- **Permissions**:
    - Control access to files and directories (read, write, execute).
    - Permissions apply uniformly across all users.


#### Disk Management
- **Tools**:
    - **fdisk**: Creates, deletes, and manages disk partitions.
    - **gparted**: GUI tool for partition management.
- **Commands**:
```
**List Partitions**:
sudo fdisk -l


**Example Output**:
Disk /dev/vda: 160 GiB, 171798691840 bytes
Device     Boot     Start       End   Sectors  Size Id Type
/dev/vda1  *         2048 158974027 158971980 75.8G 83 Linux
/dev/vda2       158974028 167766794   8792767  4.2G 82 Linux swap / Solaris
```


#### Mounting and Unmounting
- **Mounting**:
    - Attach a drive to a directory in the file system.
    - **Command**:
```
sudo mount /dev/sdb1 /mnt/usb
```

**Unmounting**:
- Detach a drive from the file system.
- **Command**:
```
sudo umount /mnt/usb
```

**Automatic Mounting at Boot**:
- Defined in `/etc/fstab`.
- **Example `/etc/fstab` Entry**:
```
UUID=3d6a020d-...SNIP...-9e085e9c927a /              btrfs   subvol=@,defaults,noatime,nodiratime,nodatacow,space_cache,autodefrag 0 1
UUID=21f7eb94-...SNIP...-d4f58f94e141 swap           swap    defaults,noatime 0 0
/dev/sdb1 /mnt/usb ext4 rw,noauto,user 0 0
```

**Ensure No Active Processes**:
- Use `lsof` to list open files and processes:
```
lsof | grep <mount_point>
```



#### Swap Space
- **Purpose**:
    - Extends physical memory by using disk space.
    - Used for paging and hibernation.
- **Setup Commands**:
```
**Create Swap Space**:
sudo mkswap /dev/sdXn

**Activate Swap Space**:
sudo swapon /dev/sdXn
```
- **Encryption**:
    - Important for securing sensitive data stored in swap space.
- **Hibernation**:
    - Saves the system state to swap space, allowing for power-off and later resumption.


### Questions:
- How many partitions exist in our Pwnbox? (Format: 0)
	- 3