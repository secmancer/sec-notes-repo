**Navigation and File Management**
Navigating through Linux involves understanding and using commands to manage directories and files. Here are some essential commands and their descriptions to help you get started:
#### Basic Commands
- **`pwd`**: Prints the current working directory.
    - _Example_: `cry0l1t3@htb[~]$ pwd`  
        `/home/cry0l1t3`
- **`ls`**: Lists the contents of a directory.
    - _Basic usage_: `cry0l1t3@htb[~]$ ls`  
        `Desktop Documents Downloads Music Pictures Public Templates Videos`
- **`ls -l`**: Lists contents with detailed information.
    - _Example_: `cry0l1t3@htb[~]$ ls -l`
```
total 32
drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 Desktop
drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Documents
```

![[Screenshot_20240912_122634.png]]
Columns:
- `Type and permissions`
- `Number of hard links`
- `Owner`
- `Group owner`
- `Size`
- `Date and time`
- `Name`
- **`ls -la`**: Lists all files, including hidden ones (files starting with a dot).
	- _Example_: `cry0l1t3@htb[~]$ ls -la`
```
total 403188
drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 .bash_history
drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 .bashrc
```
- **`cd`**: Changes the directory.
    - _Example_: `cry0l1t3@htb[~]$ cd /dev/shm`
- **`cd -`**: Returns to the previous directory.
    - _Example_: `cry0l1t3@htb[/dev/shm]$ cd -`  
        `cry0l1t3@htb[~]$`

#### Advanced Navigation
- **Auto-Completion**: Use `[TAB]` to auto-complete directory names.
    - _Example_: `cry0l1t3@htb[~]$ cd /dev/s [TAB 2x]`  
        `shm/ snd/`
- **Navigating Parent Directory**: Use `..` to move to the parent directory.
    - _Example_: `cry0l1t3@htb[/dev/shm]$ cd ..`  
        `cry0l1t3@htb[/dev]$`

#### Terminal Management
- **`clear`**: Clears the terminal screen.
    - _Example_: `cry0l1t3@htb[/dev]$ clear`
- **`[Ctrl] + [L]`**: Shortcut to clear the terminal screen.
- **Arrow Keys**: Use the up and down arrow keys to scroll through command history.
- **`[Ctrl] + [R]`**: Search through command history.
    - _Example_: Press `[Ctrl] + [R]` and type part of a command to find it.

### Practice and Experimentation
- **Experiment**: Practice these commands on a local VM to become familiar with Linux navigation and file management.
- **Create Snapshots**: Always create a snapshot of your VM before making significant changes to recover in case of issues.


### Questions
- What is the name of the hidden "history" file in the htb-user's home directory?
	- .bash_history
- What is the index number of the "sudoers" file in the "/etc" directory?
	- 147627