In Linux, managing files and directories can be more efficient than using a graphical interface because you can use terminal commands to directly access, edit, and manipulate files. Below are the key commands and practices for working with files and directories:

#### Creating Files and Directories
- **Create an Empty File**:
    - _Syntax_: `touch <name>`
    - _Example_: `secmancer@htb[/htb]$ touch info.txt`
- **Create a Directory**:
    - _Syntax_: `mkdir <name>`
    - _Example_: `secmancer@htb[/htb]$ mkdir Storage`
- **Create Parent Directories**:
    - Use the `-p` option to create parent directories along with the specified directory.
    - _Syntax_: `mkdir -p <path>`
    - _Example_: `secmancer@htb[/htb]$ mkdir -p Storage/local/user/documents`
- **Create a File in a Specific Directory**:
    - Specify the path to the directory.
    - _Syntax_: `touch <path/filename>`
    - _Example_: `secmancer@htb[/htb]$ touch ./Storage/local/user/userinfo.txt`

#### Moving and Renaming Files and Directories
- **Move or Rename Files/Directories**:
    - _Syntax_: `mv <source> <destination>`
    - _Example_:
        - Rename file: `secmancer@htb[/htb]$ mv info.txt information.txt`
        - Move file: `secmancer@htb[/htb]$ mv information.txt readme.txt Storage/`

#### Copying Files and Directories
- **Copy Files**:
    - _Syntax_: `cp <source> <destination>`
    - _Example_: `secmancer@htb[/htb]$ cp Storage/readme.txt Storage/local/`

#### Viewing Directory Structure
- **Tree Command**:
    - Shows the directory structure in a tree-like format.
    - _Example_: `secmancer@htb[/htb]$ tree .`
```
.
├── info.txt
└── Storage
    └── local
        └── user
            ├── documents
            └── userinfo.txt
```

#### Terminal Efficiency
- **Editing Files**: You can edit files directly using commands and regular expressions without needing a text editor.
- **Simultaneous Commands**: Run multiple commands at once and redirect output to files, saving time and effort.

#### Optional Exercise
- **Delete Files and Directories**: Use `rm` to delete files and `rm -r` to delete directories. Experiment with these commands to understand their usage and implications.

### Questions
- What is the name of the last modified file in the "/var/backups" directory?
	- apt.extended_states.0
- What is the inode number of the "shadow.bak" file in the "/var/backups" directory?
	- 265293