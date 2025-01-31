### Introduction
- **Objective**: Master file and directory manipulation using Command Prompt.
- **Key Topics**:
  - Creating, deleting, and modifying directories.
  - Viewing, creating, modifying, and deleting files.
  - Using commands like `dir`, `cd`, `md`, `rd`, `move`, `xcopy`, `robocopy`, `type`, `more`, `echo`, `fsutil`, `ren`, `del`, and `erase`.
  - Input/output redirection and piping.



### Directories
- #### Viewing & Listing Directories
	- **Command**: `dir`
	  - Lists contents of the current directory.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> dir
    ```
	- **Command**: `tree`
	  - Displays directory structure in a tree format.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> tree /F
    ```
- #### Creating a New Directory
	- **Commands**: `md` or `mkdir`
	  - Creates a new directory.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> md new-directory
    ```
    ```cmd
    C:\Users\htb\Desktop> mkdir yet-another-dir
    ```
- #### Deleting Directories
	- **Commands**: `rd` or `rmdir`
	  - Deletes directories.
	  - Use `/S` to delete non-empty directories.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> rd /S Git-Pulls
    ```
- #### Modifying Directories
	- **Command**: `move`
	  - Moves directories and their contents.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> move example C:\Users\htb\Documents\example
    ```
	- **Command**: `xcopy`
	  - Copies directories and files, including subdirectories.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> xcopy C:\Users\htb\Documents\example C:\Users\htb\Desktop\ /E
    ```
	- **Command**: `robocopy`
	  - Advanced copying and syncing of directories.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> robocopy C:\Users\htb\Desktop C:\Users\htb\Documents\
    ```



### Files
- #### Viewing File Contents
	- **Command**: `type`
	  - Displays file contents.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> type secrets.txt
    ```
	- **Command**: `more`
	  - Displays file contents one screen at a time.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> more secrets.txt
    ```
- #### Creating and Modifying Files
	- **Command**: `echo`
	  - Creates or appends to a file.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> echo Check out this text > demo.txt
    ```
    ```cmd
    C:\Users\htb\Desktop> echo More text for our demo file >> demo.txt
    ```
	- **Command**: `fsutil`
	  - Creates a new file with a specified size.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> fsutil file createNew for-sure.txt 222
    ```
	- **Command**: `ren` or `rename`
	  - Renames a file.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> ren demo.txt superdemo.txt
    ```
- #### Deleting Files
	- **Commands**: `del` or `erase`
	  - Deletes files.
	  - Use `/A` to delete files based on attributes (e.g., read-only, hidden).
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> del file-1
    ```
    ```cmd
    C:\Users\htb\Desktop> del /A:H *
    ```
- #### Copying and Moving Files
	- **Command**: `copy`
	  - Copies files to a new location.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> copy secrets.txt C:\Users\htb\Downloads\not-secrets.txt
    ```
	- **Command**: `move`
	  - Moves files to a new location.
	  - Example:
    ```cmd
    C:\Users\htb\Desktop> move bio.txt C:\Users\htb\Downloads
    ```



### Input/Output Redirection and Piping
- #### Output Redirection
	- **Symbol**: `>`
	  - Redirects output to a file (overwrites).
	  - Example:
    ```cmd
    C:\Users\htb\Documents> ipconfig /all > details.txt
    ```
	- **Symbol**: `>>`
	  - Appends output to a file.
	  - Example:
    ```cmd
    C:\Users\htb\Documents> echo f g h i j k see how this works now? >> test.txt
    ```
- #### Input Redirection
	- **Symbol**: `<`
	  - Feeds input from a file to a command.
	  - Example:
    ```cmd
    C:\Users\htb\Documents> find /i "see" < test.txt
    ```
- #### Piping
	- **Symbol**: `|`
	  - Sends output of one command as input to another.
	  - Example:
    ```cmd
    C:\Users\htb\Documents> ipconfig /all | find /i "IPV4"
    ```
- #### Command Chaining
	- **Symbol**: `&`
	  - Runs multiple commands sequentially.
	  - Example:
    ```cmd
    C:\Users\htb\Documents> ping 8.8.8.8 & type test.txt
    ```
	- **Symbol**: `&&`
	  - Runs the second command only if the first succeeds.
	  - Example:
    ```cmd
    C:\Users\htb\Documents> cd C:\Users\htb\Documents\Backup && echo 'did this work' > yes.txt
    ```
	- **Symbol**: `||`
	  - Runs the second command only if the first fails.
	  - Example:
    ```cmd
    C:\Users\htb\Documents> cd C:\NonexistentFolder || echo 'Failed to change directory'
    ```



### Summary
- **Directories**:
  - Use `dir`, `tree`, `md`, `rd`, `move`, `xcopy`, and `robocopy` to manage directories.
- **Files**:
  - Use `type`, `more`, `echo`, `fsutil`, `ren`, `del`, `copy`, and `move` to manage files.
- **Input/Output**:
  - Use `>`, `>>`, `<`, `|`, `&`, `&&`, and `||` for redirection and command chaining.



### Questions
- What command can display the contents of a file and redirect the contents of the file into another file or to the console?
	- type
- What command can be used to make the 'apples' directory? (full command as answer, not the alias)
	- m k dir apples