### Introduction
- **Linux File System Management**: Involves organizing and maintaining data on storage devices, supporting various file systems like ext2, ext3, ext4, XFS, Btrfs, and NTFS.
- **File System Choice**: The selection depends on specific needs; e.g., ext2 is simple, Btrfs offers data integrity and snapshots, and NTFS is used for Windows compatibility.
- **Unix-Based Structure**: The Linux file system follows a hierarchical structure with the inode table at the top, containing metadata about each file and directory (e.g., permissions, size, owner).
- **File Types**: Files are stored as regular files or directories. Directories are used to organize files, and symbolic links allow access to files from different locations.
- **Permissions**: Files and directories have permissions that control who can read, write, and execute them. Changes to permissions affect all users.
```shell-session
secmancer@htb[/htb]$ ls -il

total 0
10678872 -rw-r--r--  1 cry0l1t3  htb  234123 Feb 14 19:30 myscript.py
10678869 -rw-r--r--  1 cry0l1t3  htb   43230 Feb 14 11:52 notes.txt
```



### Disks & Drives
- Disk management on Linux involves managing physical storage devices, including hard drives, solid-state drives, and removable storage devices. 
- The main tool for disk management on Linux is the `fdisk`, which allows us to create, delete, and manage partitions on a drive. 
- It can also display information about the partition table, including the size and type of each partition. 
- Partitioning a drive on Linux involves dividing the physical storage space into separate, logical sections. 
- Each partition can then be formatted with a specific file system, such as ext4, NTFS, or FAT32, and can be mounted as a separate file system. 
- The most common partitioning tool on Linux is also `fdisk`, `gpart`, and `GParted`.
- #### Fdisk
```shell-session
secmancer@htb[/htb]$ sudo fdisk -l

Disk /dev/vda: 160 GiB, 171798691840 bytes, 335544320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x5223435f

Device     Boot     Start       End   Sectors  Size Id Type
/dev/vda1  *         2048 158974027 158971980 75.8G 83 Linux
/dev/vda2       158974028 167766794   8792767  4.2G 82 Linux swap / Solaris

Disk /dev/vdb: 452 KiB, 462848 bytes, 904 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```



### Mounting
- Each logical partition or drive needs to be assigned to a specific directory on Linux. 
- This process is called mounting.
- Mounting involves attaching a drive to a specific directory, making it accessible to the file system hierarchy. 
- Once a drive is mounted, it can be accessed and manipulated just like any other directory on the system. 
- The `mount` tool is used to mount file systems on Linux, and the `/etc/fstab` file is used to define the default file systems that are mounted at boot time.
- #### Mounted File systems at Boot
```shell-session
secmancer@htb[/htb]$ cat /etc/fstab

# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a device; this may
# be used with UUID= as a more robust way to name devices that works even if
# disks are added and removed. See fstab(5).
#
# <file system>                      <mount point>  <type>  <options>  <dump>  <pass>
UUID=3d6a020d-...SNIP...-9e085e9c927a /              btrfs   subvol=@,defaults,noatime,nodiratime,nodatacow,space_cache,autodefrag 0 1
UUID=3d6a020d-...SNIP...-9e085e9c927a /home          btrfs   subvol=@home,defaults,noatime,nodiratime,nodatacow,space_cache,autodefrag 0 2
UUID=21f7eb94-...SNIP...-d4f58f94e141 swap           swap    defaults,noatime 0 0
```
- To view the currently mounted file systems, we can use the "mount" command without any arguments.
- The output will show a list of all the currently mounted file systems, including the device name, file system type, mount point, and options.
- #### List Mounted Drives
```shell-session
secmancer@htb[/htb]$ mount

sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,relatime,size=4035812k,nr_inodes=1008953,mode=755,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,noexec,relatime,size=814580k,mode=755,inode64)
/dev/vda1 on / type btrfs (rw,noatime,nodiratime,nodatasum,nodatacow,space_cache,autodefrag,subvolid=257,subvol=/@)
```
- To mount a file system, we can use the `mount` command followed by the device name and the mount point. 
- For example, to mount a USB drive with the device name `/dev/sdb1` to the directory `/mnt/usb`, we would use the following command.
- #### Mount a USB drive
```shell-session
secmancer@htb[/htb]$ sudo mount /dev/sdb1 /mnt/usb
secmancer@htb[/htb]$ cd /mnt/usb && ls -l

total 32
drwxr-xr-x 1 root root   18 Oct 14  2021 'Account Takeover'
drwxr-xr-x 1 root root   18 Oct 14  2021 'API Key Leaks'
drwxr-xr-x 1 root root   18 Oct 14  2021 'AWS Amazon Bucket S3'
drwxr-xr-x 1 root root   34 Oct 14  2021 'Command Injection'
drwxr-xr-x 1 root root   18 Oct 14  2021 'CORS Misconfiguration'
drwxr-xr-x 1 root root   52 Oct 14  2021 'CRLF Injection'
drwxr-xr-x 1 root root   30 Oct 14  2021 'CSRF Injection'
drwxr-xr-x 1 root root   18 Oct 14  2021 'CSV Injection'
drwxr-xr-x 1 root root 1166 Oct 14  2021 'CVE Exploits'
...SNIP...
```
- To unmount a file system in Linux, we can use the `umount` command followed by the mount point of the file system we want to unmount.
- The mount point is the location in the file system where the file system is mounted and is accessible to us. 
- For example, to unmount the USB drive that was previously mounted to the directory `/mnt/usb`, we would use the following command:
- #### Unmount
```shell-session
secmancer@htb[/htb]$ sudo umount /mnt/usb
```
- It is important to note that we must have sufficient permissions to unmount a file system. 
- We also cannot unmount a file system that is in use by a running process. 
- To ensure that there are no running processes that are using the file system, we can use the `lsof` command to list the open files on the file system.
```shell-session
cry0l1t3@htb:~$ lsof | grep cry0l1t3

vncserver 6006        cry0l1t3  mem       REG      0,24       402274 /usr/bin/perl (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24      1554101 /usr/lib/locale/aa_DJ.utf8/LC_COLLATE (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24       402326 /usr/lib/x86_64-linux-gnu/perl-base/auto/POSIX/POSIX.so (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24       402059 /usr/lib/x86_64-linux-gnu/perl/5.32.1/auto/Time/HiRes/HiRes.so (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24      1444250 /usr/lib/x86_64-linux-gnu/libnss_files-2.31.so (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24       402327 /usr/lib/x86_64-linux-gnu/perl-base/auto/Socket/Socket.so (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24       402324 /usr/lib/x86_64-linux-gnu/perl-base/auto/IO/IO.so (path dev=0,26)
...SNIP...
```
- If we find any processes that are using the file system, we need to stop them before we can unmount the file system. 
- Additionally, we can also unmount a file system automatically when the system is shut down by adding an entry to the `/etc/fstab` file. 
- The `/etc/fstab` file contains information about all the file systems that are mounted on the system, including the options for automatic mounting at boot time and other mount options.
- To unmount a file system automatically at shutdown, we need to add the `noauto` option to the entry in the `/etc/fstab` file for that file system.
- This would look like, for example, the following below is an example of that.
- #### Fstab File
```txt
/dev/sda1 / ext4 defaults 0 0
/dev/sda2 /home ext4 defaults 0 0
/dev/sdb1 /mnt/usb ext4 rw,noauto,user 0 0
192.168.1.100:/nfs /mnt/nfs nfs defaults 0 0
```



### SWAP
- **Swap Space in Linux**: Used for memory management when physical memory is exhausted, transferring inactive memory pages to free up space for active processes.
- **Creating and Activating Swap**: Use `mkswap` to set up swap space and `swapon` to activate it. Swap space can be created during installation or afterward.
- **Size and Placement**: The size depends on physical memory and usage needs. Swap should be on a dedicated partition or file to avoid fragmentation.
- **Security**: Swap space should be encrypted to protect sensitive data temporarily stored there.
- **Hibernation**: Swap space can also be used for hibernation, allowing the system to save its state to disk and restore it when powered on.



### Questions
- How many partitions exist in our Pwnbox? (Format: 0)
	- 3