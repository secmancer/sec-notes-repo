### Regular Permissions:
- **Read (r)**: Allows viewing the content of a file or directory.
- **Write (w)**: Allows modifying the content of a file or directory.
- **Execute (x)**: For files, allows running the file as a program. For directories, it grants permission to access or "traverse" the directory.
- Each file and directory has permissions assigned for three types of users:
- **Owner** (user who owns the file)
- **Group** (the group associated with the file)
- **Others** (everyone else)
- These permissions are represented using either symbolic notation (rwx) or numeric (octal) representation (e.g., `755`).



### Changing Permissions (`chmod`):
- You can change the permissions of a file or directory using the `chmod` command:
    - **Symbolic**: `chmod u+x file` (adds execute permission for the owner).
    - **Numeric/Octal**: `chmod 755 file` (sets rwx for owner, rx for group and others).



### Changing Ownership (`chown`):
- Ownership can be changed with the `chown` command. For example:
    - `chown root:root file` (changes ownership to `root` and group to `root`).



### Special Permissions:
1. **SUID (Set User ID)**:
    - Allows a user to execute a file with the permissions of the file’s owner, usually root.
    - Indicated by an `s` in the execute position for the owner (e.g., `rwsr-xr-x`).
    - **Risk**: SUID on vulnerable programs can allow users to escalate privileges.
2. **SGID (Set Group ID)**:
    - Allows a user to execute a file with the permissions of the file’s group.
    - Indicated by an `s` in the execute position for the group (e.g., `rwxr-sr-x`).
    - For directories, it makes newly created files inherit the group of the directory, not the user’s group.
3. **Sticky Bit**:
    - When set on a directory, it allows only the file’s owner, the directory’s owner, or root to delete or rename files within that directory.
    - Indicated by a `t` (lowercase) or `T` (uppercase) in the execute position for others:
        - `t` means sticky bit is set and execute permissions are granted.
        - `T` means sticky bit is set but execute permissions are not granted.



### Examples:
- **SUID example**:
    - You might see something like this: `rwsr-xr-x`, where the file is executable by all, but when executed, it runs with the privileges of the file's owner (e.g., root).
- **SGID example**:
    - A file might look like `rwxr-sr-x`, where it runs with the group’s privileges.
- **Sticky Bit example**:
    - A directory with the sticky bit set may appear as `drwxrwxrwt`. This ensures that only the file owner, root, or the directory owner can delete or rename files within the directory.



### Practical Use Cases:
- **SUID**: Common for commands that need elevated privileges, such as `passwd`, which requires root access but allows normal users to change their passwords.
- **SGID**: Often used for shared directories where files should inherit the group of the directory, ensuring group collaboration.
- **Sticky Bit**: Typically applied to directories like `/tmp`, where multiple users can write files, but only the file owner can delete their files, preventing accidental or malicious file deletion.