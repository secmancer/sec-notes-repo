### Key Commands for File and Directory Management
1. **Creating Files and Directories:**    
    - `touch <filename>`: Creates an empty file.
    - `mkdir <dirname>`: Creates a directory.
    - `mkdir -p <path>`: Creates parent directories as needed.
2. **Moving, Renaming, and Copying Files:**
    - `mv <source> <destination>`: Moves or renames files/directories.
    - `cp <source> <destination>`: Copies files/directories.
3. **Viewing Directory Structure:**
    - `tree`: Displays directory contents in a tree-like format, showing files and subdirectories.
4. **Working with Relative and Absolute Paths:**
    - You can create files in specific locations using relative paths (e.g., `./Storage/local/user/userinfo.txt`) or absolute paths (e.g., `/home/user/Storage/`).
    - `.` represents the current directory, and `..` represents the parent directory.



### Optional Exercise (Deleting Files and Directories)
- To delete files and directories, you'd use the following commands:
1. **Deleting Files:**
    - `rm <filename>`: Removes a file.
    - `rm -f <filename>`: Forcefully removes a file, bypassing any confirmation prompts.
2. **Deleting Directories:**
    - `rmdir <dirname>`: Removes an empty directory.
    - `rm -r <dirname>`: Recursively removes a directory and all its contents.
    - `rm -rf <dirname>`: Forcefully removes a directory and its contents without asking for confirmation.



### Redirection and Text Editors
- As you mentioned, redirection and text editors are powerful tools for working with files:
- **Redirection:**
    - `>`: Redirects output to a file (overwrites the file if it exists).
    - `>>`: Appends output to a file.
    - `<`: Redirects input from a file.
    - `2>`: Redirects error output to a file.
- **Text Editors:**
    - **`nano`**: A simple, user-friendly text editor.
    - **`vim`**: A more advanced text editor with a steeper learning curve but highly efficient for those who master it.



### Questions
- What is the name of the last modified file in the "/var/backups" directory?
	- apt.extended_states.0
- What is the inode number of the "shadow.bak" file in the "/var/backups" directory?
	- 265293