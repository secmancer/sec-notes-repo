User management is a key aspect of Linux administration. It involves creating, modifying, and deleting users and groups, as well as executing commands with different user privileges.

#### Executing Commands as a Different User
- **Example**:
```
Attempt to access a restricted file:

secmancer@htb[/htb]$ cat /etc/shadow
cat: /etc/shadow: Permission denied


Using `sudo` to gain elevated privileges:

secmancer@htb[/htb]$ sudo cat /etc/shadow
root:<SNIP>:18395:0:99999:7:::
daemon:*:17737:0:99999:7:::
bin:*:17737:0:99999:7:::
<SNIP>
```

#### Key Commands for User Management
- **`sudo`**:
    - **Description**: Execute commands with the privileges of another user, typically root.
    - **Usage**: `sudo [command]`
- **`su`**:
    - **Description**: Switch to a different user account. The default is the superuser (root). Requests user credentials and starts a shell.
    - **Usage**: `su [username]`
- **`useradd`**:
    - **Description**: Create a new user or update default new user information.
    - **Usage**: `useradd [options] [username]`
- **`userdel`**:
    - **Description**: Delete a user account and related files.
    - **Usage**: `userdel [options] [username]`
- **`usermod`**:
    - **Description**: Modify an existing user account.
    - **Usage**: `usermod [options] [username]`
- **`addgroup`**:
    - **Description**: Add a new group to the system.
    - **Usage**: `addgroup [groupname]`
- **`delgroup`**:
    - **Description**: Remove a group from the system.
    - **Usage**: `delgroup [groupname]`
- **`passwd`**:
    - **Description**: Change a user’s password.
    - **Usage**: `passwd [username]`

![[Screenshot_20240912_134631.png]]
#### Practical Tips
- **Experiment with Commands**: To get comfortable with user management, practice using the commands with different options and scenarios.
- **Understand Privilege Levels**: Knowing when to use `sudo` versus `su` can help you manage permissions and execute commands securely.
- **User and Group Maintenance**: Regularly review and update user and group information to maintain system security and functionality.

### Questions
- Which option needs to be set to create a home directory for a new user using "useradd" command?
	- -m
- Which option needs to be set to lock a user account using the "usermod" command? (long version of the option)
	- --lock
- Which option needs to be set to execute a command as a different user using the "su" command? (long version of the option)
	- --command