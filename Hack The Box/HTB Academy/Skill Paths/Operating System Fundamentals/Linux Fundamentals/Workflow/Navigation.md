1. **Navigating Directories:**
    - `pwd` shows the current directory you are in.
    - `ls` lists the files and directories in the current directory.
    - `ls -l` provides detailed information, like permissions, owner, and size.
    - `ls -la` also includes hidden files (those starting with a dot, like `.bashrc`).
    - `cd` changes directories. You can go to a directory using its path, like `cd /dev/shm`, or use `cd -` to return to the previous directory.
    - `TAB` autocomplete helps by completing commands and paths.
    - `..` moves you up to the parent directory.
2. **File Listing:**  
    - The `-l` option with `ls` provides a long listing format, showing details about each file or directory, including permissions, owner, group, and modification time.
    - Hidden files can be listed with `-a`.
3. **Terminal Shortcuts:**
    - `clear` clears the terminal screen, making it easier to read the current session.
    - `Ctrl + L` also clears the terminal screen.
    - `Ctrl + R` allows you to search through your command history.



### Questions
- What is the name of the hidden "history" file in the htb-user's home directory?
	- .bash_history
- What is the index number of the "sudoers" file in the "/etc" directory?
	- 147627