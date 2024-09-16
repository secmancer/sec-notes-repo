**User and Group Permissions**:
- **Users**: Each file and directory is associated with a specific user (owner) and a specific group.
- **Groups**: Users can belong to multiple groups, and file permissions can be assigned to these groups.
- **Default Ownership**: New files or directories inherit the group of the user who created them.

**Accessing Directories**:
- To access a directory's contents, users need **execute permissions** on the directory.
- Without execute permissions, users receive a “Permission Denied” error when attempting to access the directory.

#### Permission Types
- **Read (r)**: Allows viewing the contents of a file or directory.
- **Write (w)**: Allows modifying the contents of a file or directory.
- **Execute (x)**: Allows executing a file or traversing a directory.

#### Permission Representation
Permissions are represented using a combination of letters and numbers:
- **File Listing Example**:
```
cry0l1t3@htb[/htb]$ ls -l /etc/passwd
- rwx rw- r--   1 root root 1641 May  4 23:42 /etc/passwd
```
Breakdown:
- **File Type**: `-` (file), `d` (directory)
- **Permissions**:
    - **Owner**: `rwx` (read, write, execute)
    - **Group**: `rw-` (read, write)
    - **Others**: `r--` (read)
- **File Details**: Number of links, owner, group, file size, modification date.

#### Changing Permissions
- **`chmod` Command**:
    - **Syntax**: `chmod [permissions] [file/directory]`
    - **Modify Permissions**:
        - **Add Permissions**: `chmod a+r file` (adds read permission for all users)
        - **Remove Permissions**: `chmod a-x file` (removes execute permission for all users)
        - **Octal Notation**: `chmod 754 file` (sets permissions to `rwxr-xr--`)
    - **Example**:
```
cry0l1t3@htb[/htb]$ chmod 754 shell && ls -l shell
-rwxr-xr--   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

**Binary to Octal Conversion**:
- Binary Representation: `111 | 101 | 100`
- Octal Value: `7 5 4`
- Permission Representation: `rwx | r-x | r--`

#### Changing Ownership
- **`chown` Command**:
    - **Syntax**: `chown <user>:<group> <file/directory>`
    - **Example**:
```
cry0l1t3@htb[/htb]$ chown root:root shell && ls -l shell
-rwxr-xr--   1 root root 0 May  4 22:12 shell
```

#### Special Permissions
- **SUID (Set User ID)**:
    - Allows a program to execute with the privileges of the file's owner.
    - Represented by an `s` in place of the execute bit.
    - Example: `-rwsr-xr-x`
- **SGID (Set Group ID)**:
    - Allows a program to execute with the privileges of the file's group.
    - Represented by an `s` in place of the execute bit.
    - Example: `-rwxr-sr-x`
- **Sticky Bit**:
    - Ensures that only the owner of a file or directory, or the root user, can delete or rename files within a directory.
    - Represented by a `t` (lowercase) or `T` (uppercase) in the execute permission of the directory's permissions.
    - **Example**:
```
cry0l1t3@htb[/htb]$ ls -l
drw-rw-r-t 3 cry0l1t3 cry0l1t3 4096 Jan 12 12:30 scripts
drw-rw-r-T 3 cry0l1t3 cry0l1t3 4096 Jan 12 12:32 reports
```
- **Lowercase `t`**: Execute permission is set for all users.
- **Uppercase `T`**: No execute permission is set for other users.