- **Directories Overview:**
    - A directory is essentially a folder structure within the Windows filesystem.
    - Files are nested within this folder structure.
    - Commands like `cd` (change directory) and `dir` (list directory contents) are used to navigate the system.

- **Filesystem as a Hotel Analogy:**
    - **Root Directory (C: Drive)**: The entire drive is the "hotel," serving as the starting point.
    - **Main Directories (Windows, Users, Program Files, etc.)**: These are like the different floors of the hotel, each containing multiple halls (subdirectories).
    - **Nested Folders**: Each hallway represents a directory. For example, `C:\Users\htb` is several layers deep.
    - **Files**: Represented as doors within these hallways, containing the actual data or documents.


- **Viewing the Current Directory**:
    - Use the `cd` command to see which directory you are currently in.
    - Use `dir` to list files and subdirectories within the current directory.
    - The `tree` command provides a complete hierarchical view of all files and directories within a specified path.


- **Changing Directories**:
    - The `cd` or `chdir` command allows you to navigate between directories.


- **Creating Directories**:
    - Use `md` or `mkdir` to create new directories.
    - Both commands achieve the same goal; you can use either based on preference.
    Example:
    - `md new-directory` creates a directory called "new-directory".
    - `mkdir another-directory` creates another directory named "another-directory".



- **Deleting Directories**:
    - **Basic Removal**: Use `rd` or `rmdir` to remove directories.
    - If the directory is not empty, use the `/S` switch to delete the directory and its contents.
    - Example: `rd /S directory-name` removes a non-empty directory.


- **Helpful Tips**:
    - If you encounter a "directory not empty" error, use the `/S` switch with `rd` or `rmdir` to forcefully remove the directory and its contents.
    - Both `rd` and `rmdir` function similarly, so you can choose either command based on preference.


**Moving Directories**
- Moving a directory is more complex than moving files as directories contain multiple files and subdirectories.
- To move a directory, the `move` command is used with this syntax:
    - `move source_directory destination_directory`
    - Example:
        - `move example C:\Users\htb\Documents\example`
    - This moves the entire `example` directory from the Desktop to the Documents folder, including all files.


**Using `xcopy`**
- `xcopy` copies directories and files, and can handle specific tasks like removing the read-only attribute.
- Syntax: `xcopy source destination [options]`
    - Example:
        - `xcopy C:\Users\htb\Documents\example C:\Users\htb\Desktop\ /E`
        - The `/E` option copies all files and subdirectories, including empty directories.
    - Use `/K` to retain file attributes such as read-only.


**3. Using `robocopy`**
- `robocopy` (Robust File Copy) is a more advanced tool that handles larger directories, copying files locally, between drives, and across networks.
- Syntax: `robocopy source destination [options]`
    - Example:
        - `robocopy C:\Users\htb\Desktop C:\Users\htb\Documents\`
    - It retains file attributes, timestamps, ownership, and ACLs.
    - Example with mirroring:
        - `robocopy /E /MIR /A-:SH C:\Users\htb\Desktop\notes\ C:\Users\htb\Documents\Backup\Files-to-exfil\`
        - `/MIR` mirrors directories and deletes any extra files at the destination.

In Windows, we can use various built-in tools to work with files. These commands allow us to list, view, and manipulate files efficiently, offering numerous capabilities that are crucial for system administration or security work.


#### Listing Files and Viewing Their Contents
- **`dir`**: Lists all files within a directory. You can customize the output using switches.
- **`tree /F`**: Displays a directory tree, including both files and directories.


#### Viewing File Contents
To view the contents of a file, we can use the following commands:
1. **`more`**:
    - Displays file contents one screen at a time, preventing terminal overflow.
    - Shows the percentage of the file being viewed at the bottom.
    - **Example**:
        - `C:\> more secrets.txt`
        - `C:\> more /S secrets.txt` (Compresses blank lines)
2. **`openfiles`**:
    - Displays files that are open on the system, either locally or remotely, along with the users accessing them.
    - Requires administrative privileges.
3. **`type`**:
    - Displays the contents of one or more text files. It can also append file content using redirection.
    - Does not lock files during viewing.
    - **Examples**:
        - `C:\> type bio.txt` (Displays the content of a file)
        - `C:\> type passwords.txt >> secrets.txt` (Appends the content of passwords.txt to secrets.txt)

#### Piping Output
You can also combine commands to control the output:
- **`ipconfig /all | more`**:
    - The `| more` pipe allows you to slow down large outputs, such as the results of commands like `ipconfig`.


#### Key Takeaways
- **`more`**: Scroll through large text one screen at a time.
- **`openfiles`**: View files currently in use on the system (requires admin privileges).
- **`type`**: Display or append file contents without locking them.
- **Redirection**: Use `>>` to append contents from one file to another.

#### **Creating and Modifying Files via Echo**
- The `echo` command with output redirection can create or modify files.
    - Single `>` creates or overwrites a file.
    - Double `>>` appends to an existing file.
    **Example:**
    - Create or overwrite a file:
        - `echo Check out this text > demo.txt`
        - `type demo.txt` will show: `Check out this text`
    - Append more content to the file:
        - `echo More text for our demo file >> demo.txt`
        - `type demo.txt` will show:
```
Check out this text
More text for our demo file
```


#### **Creating Files Using Fsutil**
- The `fsutil` command can create files with a specified size (in bytes).
    **Example:**
    - Create a 222-byte file:
        - `fsutil file createNew for-sure.txt 222`
    - Add content to the file:
        - `echo "my super cool text file from fsutil" > for-sure.txt`
        - `type for-sure.txt` will display the text.

#### **Renaming Files with Ren/Rename**
- The `ren` or `rename` command can change a file's name.
    **Example:**
    - Rename a file:
        - `ren demo.txt superdemo.txt`
    - Use `dir` to confirm the file name change.


#### Redirecting Output to a File
- Use `>` to push the output of a command into a file, overwriting the file if it exists.
- Example:
    - `ipconfig /all > details.txt`: Outputs the result of the `ipconfig /all` command into `details.txt`.


#### Appending Output to a File
- Use `>>` to append the output of a command to an existing file, without overwriting it.
- Example:
    - `echo f g h i j k see how this works now? >> test.txt`: Appends the string to `test.txt`.


#### Redirecting Input to a Command
- Use `<` to pass the contents of a file as input to a command.
- Example:
    - `find /i "see" < test.txt`: Feeds the content of `test.txt` to the `find` command, searching for the string "see."


#### Piping Output Between Commands
- Use `|` to send the output of one command as input to another.
- Example:
    - `ipconfig /all | find /i "IPV4"`: Sends the output of `ipconfig /all` to `find`, searching for "IPV4."


#### Running Multiple Commands
- Use `&` to run two commands in succession, regardless of success or failure.
- Example:
    - `ping 8.8.8.8 & type test.txt`: Runs `ping` first, then displays the contents of `test.txt`.


#### Conditional Command Execution
- Use `&&` to run a second command only if the first one succeeds.
- Example:
    - `cd Backup && echo 'did this work' > yes.txt`: Changes directory to `Backup`, and if successful, writes "did this work" to `yes.txt`.


#### Handling Command Failure
- Use `||` to run a second command only if the first one fails.


#### Dynamic Use of `Del` and `Erase`
- `del` and `erase` commands are interchangeable and can delete files.
- You can specify a **filename**, **directory**, or a **list of files** for deletion.


#### Example: Deleting a Single File
- To delete `file-1` from the current directory:
    - `del file-1`


#### Example: Deleting Multiple Files
- You can delete a list of files in one command:
    - `erase file-3 file-5`


#### Using Attributes to Delete Files
- Files can have specific attributes like **Read-only** or **Hidden**.
- The `/A` switch allows targeting files by their attributes.
    - **R**: Read-only files
    - **H**: Hidden files


#### Deleting Read-only Files
1. Identify Read-only files in the directory:
    - `dir /A:R`
2. Delete all Read-only files:
    - `del /A:R *`


#### Deleting Hidden Files
1. List hidden files in the directory:
    - `dir /A:H`
2. Delete all hidden files:
    - `del /A:H *`


#### Other Useful Switches for `Del` and `Erase`
- `/P`: Prompts for confirmation before deleting each file.
- `/F`: Force deletes Read-only files.
- `/S`: Deletes files from all subdirectories.
- `/Q`: Quiet mode, no confirmation prompt when using wildcards.


#### Removing Directories
- After deleting files within a directory, the **rd** (remove directory) command can delete the directory structure:
    - `rd directory_name`


**Copying Files**
- **`copy`** is used to duplicate files. You can copy files within the same directory or to a different directory.
- Syntax for copying and renaming a file:
    - Example:
        - Command:  _`C:\Users\student\Documents\Backup>copy secrets.txt C:\Users\student\Downloads\not-secrets.txt`_
        - Outcome: `secrets.txt` is copied to the `Downloads` folder and renamed to `not-secrets.txt`.


**Copy Validation**:
- Use the `/V` switch to verify if the files are copied correctly.
- Example:
    - Command:  
        _`copy calc.exe C:\Users\student\Downloads\copied-calc.exe /V`_
    - Result: Verifies that `calc.exe` was copied successfully.


 **Moving Files**
- **`move`** is used to move files from one location to another and can also rename them during the move.
    - Syntax for moving files:
        - Example:
            - Command:  
                _`C:\Users\student\Desktop>move C:\Users\student\Desktop\bio.txt C:\Users\student\Downloads`_
            - Outcome: `bio.txt` is moved from the `Desktop` to the `Downloads` folder.

**Key Differences**:
- `copy` creates a duplicate file, while `move` transfers the original file to the new location, removing it from the source.


## Questions
- What command can display the contents of a file and redirect the contents of the file into another file or to the console?
	- type
- What command can be used to make the 'apples' directory? (full command as answer, not the alias)
	- mkdir apples