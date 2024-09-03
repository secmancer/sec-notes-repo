### Mastering Files and Directories in Windows

#### Introduction

- **Goal:** Learn how to effectively manage files and directories in Windows.
- **Note:** There are multiple ways to accomplish file and directory management tasks.

#### Directories

- **Definition:** A directory is a folder structure within the Windows filesystem, containing files and other nested directories.
- **Analogy:**
    - The **Drive** (e.g., C:) is the root directory, akin to a hotel.
    - **Floors** in the hotel represent directories like `Windows`, `Users`, and `Program Files`.
    - **Hallways** represent nested folders within these directories, e.g., `C:\Users\htb`.
    - **Rooms** are individual files within these directories.

#### Viewing & Listing Directories

- **Commands:**
    - `cd`: Display or change the current directory.
    - `dir`: List files and directories within the current directory.
    - `tree`: Display a tree-like structure of all files and folders in a directory.

#### Creating Directories

- **Commands:**
    - `md`: Create a new directory.
    - `mkdir`: Create a new directory (alternative to `md`).
- **Example:**
	- C:\Users\htb\Desktop>md new-directory
	- C:\Users\htb\Desktop>mkdir yet-another-dir

#### Deleting Directories

- **Commands:**
    - `rd`: Remove a directory.
    - `rmdir`: Remove a directory (same as `rd`).
- **Note:** These commands are used for removing directory trees and do not affect individual files.

#### Viewing Directory Contents

- **Command:**
    - `dir`: Lists all files and directories within the current directory, displaying their details.

#### Removing Directories

- **Commands:**
    - `rd` (or `rmdir`): Removes a directory.
    - **Note:** If a directory is not empty, `rd` will not remove it by default.
    - **Example:****
	    - C:\Users\htb\Desktop> rd Git-Pulls
		- The directory is not empty.
	- **Solution:**
		- Use the `/S` switch to remove a directory and all its contents (files and subdirectories).
		- **Example:**
			- C:\Users\htb\Desktop> rd /S Git-Pulls
			- Git-Pulls, Are you sure (Y/N)? Y
#### Modifying Directories

- **Overview:** Modifying a directory involves moving or copying it along with its contents. Several commands can be used to perform these tasks.

#### Moving Directories

- **Command:**
    - `move`: Moves a directory and all its contents from the source path to the destination path.
    - **Syntax:**
	    - move source destination
	- **Example**:
		- C:\Users\htb\Desktop> move example C:\Users\htb\Documents\example
	- **Verification:**
		- Run `dir` on the destination path to ensure the directory was moved.
		- **Example:**
			- C:\Users\htb\Desktop> dir C:\Users\htb\Documents

#### Copying Directories with Xcopy

- **Command:**
    - `xcopy`: Copies directories and files with more options than `move`.
    - **Syntax:**
	    - xcopy source destination options
	- **Example:**
		- Copying a directory and all its contents:
		- C:\Users\htb\Desktop> xcopy C:\Users\htb\Documents\example C:\Users\htb\Desktop\ /E
		- **Note:** The `/E` switch tells `xcopy` to copy all subdirectories, including empty ones.
		- **Attributes:**
		    - Use the `/K` switch to retain file attributes (e.g., read-only, hidden).
		- **Use Case:**
		    - `xcopy` can be used for copying locked or system files, making it useful for both offensive and defensive operations.

### Robocopy Overview

- Robocopy (Robust File Copy) is a powerful tool for copying, moving, and syncing files and directories.
- It retains file data, timestamps, ownership, ACLs, and flags like hidden or read-only.
- Best suited for large directories and drive syncing, but can also handle single files.

### Basic Robocopy Usage

- **Copying a directory**:
    - `robocopy C:\Users\htb\Desktop C:\Users\htb\Documents`
        - This command copies all files from the Desktop to the Documents directory, retaining attributes.

### Handling Permissions with Robocopy

- **Insufficient permissions workaround**:
    - `robocopy /E /MIR /A-:SH C:\Users\htb\Desktop\notes\ C:\Users\htb\Documents\Backup\Files-to-exfil\`
        - `/MIR` mirrors the source to the destination (be cautious as it deletes files in the destination that are not in the source).
        - `/A-:SH` removes system and hidden attributes from copied files.

### Useful Switches

- `/E`: Copies all subdirectories, including empty ones.
- `/MIR`: Mirrors a directory tree (source and destination are identical).
- `/A-:SH`: Removes the system and hidden attributes from files.
- `/L`: "What-if" mode, where the command is simulated without making any actual changes.

### Error Handling

- If you receive errors related to insufficient privileges (e.g., Backup and Restore Files rights), consider avoiding `/B` or `/ZB` unless you have the necessary permissions.

#### List Files & View Their Contents

- **`dir`**: Lists files within a directory with specific information based on the switches used.
- **`tree /F`**: Displays all directories and files within the tree.

To view the contents of a file, you can use the `more`, `openfiles`, and `type` commands.

#### `more`

The `more` command allows you to view the contents of a file or the results of another command one screen at a time. It buffers scrolling text that may otherwise overflow the terminal.

**Example**:

- `C:\Users\htb\Documents\Backup> more secrets.txt`

This will display the contents of `secrets.txt`, showing one screen at a time with a percentage indicator.

If you have a file with a lot of blank space, you can compress that space using the `/S` switch.

**Example**:

- `C:\Users\htb\Documents\Backup> more /S secrets.txt`

You can also pipe the output of a command to `more` to view it one screen at a time.

**Example**:

- `C:\Users\htb\> ipconfig /all | more`

#### `openfiles`

The `openfiles` command allows you to see what files are open on your local PC or a remote host, along with the user who has them open. This command requires administrator privileges and is not enabled by default.

#### `type`

The `type` command displays the contents of text files. It can handle multiple files at once and allows for file redirection.

**Example**:

- `C:\Users\htb\Desktop>type bio.txt`

This will display the contents of `bio.txt`.

You can also use `type` to append the contents of one file to another.

**Example**:

- `C:\Users\htb\Desktop>type passwords.txt >> secrets.txt`
- `C:\Users\htb\Desktop>type secrets.txt`

The first command appends `passwords.txt` to `secrets.txt`, and the second command displays the updated `secrets.txt`.

**Create And Modify A File**

Creating and modifying a file from the command line is relatively easy. We have several options that include `echo`, `fsutil`, `ren`, `rename`, and `replace`.

- **Echo to Create and Append Files**
    
    - `C:\Users\htb\Desktop> echo Check out this text > demo.txt`
    - `C:\Users\htb\Desktop> type demo.txt`
        - Output: `Check out this text`
    - `C:\Users\htb\Desktop> echo More text for our demo file >> demo.txt`
    - `C:\Users\htb\Desktop> type demo.txt`
        - Output:
            - `Check out this text`
            - `More text for our demo file`
- **Fsutil to Create a File**
    
    - `C:\Users\htb\Desktop> fsutil file createNew for-sure.txt 222`
        - Output: `File C:\Users\htb\Desktop\for-sure.txt is created`
    - `C:\Users\htb\Desktop> echo " my super cool text file from fsutil " > for-sure.txt`
    - `C:\Users\htb\Desktop> type for-sure.txt`
        - Output: `" my super cool text file from fsutil "`
- **Ren(ame) A File**
    
    - `C:\Users\htb\Desktop> ren demo.txt superdemo.txt`
    - `C:\Users\htb\Desktop> dir`
        - Output will show `superdemo.txt` instead of `demo.txt`.

**Input / Output**

We have seen this a few times already, but let us take a minute to talk about I/O. We can utilize the `<`, `>`, `|`, and `&` to send input and output from the console and files to where we need them.

- **Output To A File**
    
    - `C:\Users\htb\Documents> dir`
    - `C:\Users\htb\Documents> ipconfig /all > details.txt`
    - `C:\Users\htb\Documents> type details.txt`
        - Output will show the results of `ipconfig /all`.
- **Append to a File**
    
    - `C:\Users\htb\Documents> echo a b c d e > test.txt`
    - `C:\Users\htb\Documents> type test.txt`
        - Output: `a b c d e`
    - `C:\Users\htb\Documents> echo f g h i j k see how this works now? >> test.txt`
    - `C:\Users\htb\Documents> type test.txt`
        - Output:
            - `a b c d e`
            - `f g h i j k see how this works now?`
- **Pass in a Text File to a Command**
    
    - `C:\Users\htb\Documents> find /i "see" < test.txt`
        - Output: `f g h i j k see how this works now?`
- **Pipe Output Between Commands**
    
    - `C:\Users\htb\Documents> ipconfig /all | find /i "IPV4"`
        - Output: `IPv4 Address. . . . . . . . . . . : 172.16.146.5(Preferred)`
- **Run Multiple Commands**
    
    - `command A & command B`
        - This will run `command A` first and then `command B` regardless of the success or failure of `command A`.

---

**Run A Then B**

If you want to run one command and then another, regardless of the success of the first command, use `&`. For example:

C:\Users\htb\Documents>ping 8.8.8.8 & type test.txt

Pinging 8.8.8.8 with 32 bytes of data: Reply from 8.8.8.8: bytes=32 time=22ms TTL=114 Reply from 8.8.8.8: bytes=32 time=19ms TTL=114 Reply from 8.8.8.8: bytes=32 time=17ms TTL=114 Reply from 8.8.8.8: bytes=32 time=16ms TTL=114

Ping statistics for 8.8.8.8: Packets: Sent = 4, Received = 4, Lost = 0 (0% loss), Approximate round trip times in milli-seconds: Minimum = 16ms, Maximum = 22ms, Average = 18ms a b c d e f g h i j k see how this works now?

If you care about the result or state of the commands being run, you can use `&&` to run the second command only if the first one succeeds. This is useful for results-dependent operations.

**State Dependent &&**

C:\Users\student\Documents>cd C:\Users\student\Documents\Backup && echo 'did this work' > yes.txt

C:\Users\student\Documents\Backup>type yes.txt 'did this work'

Here, `cd` changes the directory, and if it succeeds, `echo` writes a string into a file. The success is confirmed by the path change and the file content.

To execute a second command only if the first one fails, use `||`.

**Deleting Files**

To remove files, you can use `del` or `erase`. Both commands function similarly.

- **Delete a Single File**
    
    C:\Users\htb\Desktop\example>del file-1
    
    C:\Users\htb\Desktop\example>dir Volume in drive C has no label. Volume Serial Number is 26E7-9EE4
    
    Directory of C:\Users\htb\Desktop\example
    
    06/16/2021 02:03 PM DIR . 06/16/2021 02:03 PM DIR .. 06/16/2021 02:00 PM 5 file-2 06/16/2021 02:00 PM 5 file-3 06/16/2021 02:00 PM 5 file-4 06/16/2021 02:00 PM 5 file-5 06/16/2021 02:00 PM 5 file-6 06/16/2021 02:00 PM 5 file-66 6 File(s) 30 bytes 2 Dir(s) 38,633,730,048 bytes free
    
- **Delete Multiple Files**
    
    C:\Users\htb\Desktop\example>erase file-3 file-5
    
    C:\Users\htb\Desktop\example>dir Volume in drive C has no label. Volume Serial Number is 26E7-9EE4
    
    Directory of C:\Users\htb\Desktop\example
    
    06/16/2021 02:06 PM DIR . 06/16/2021 02:06 PM DIR .. 06/16/2021 02:00 PM 5 file-2 06/16/2021 02:00 PM 5 file-4 06/16/2021 02:00 PM 5 file-6 06/16/2021 02:00 PM 5 file-66 4 File(s) 20 bytes 2 Dir(s) 38,633,218,048 bytes free
    

**Deleting Files with Attributes**

To delete files based on specific attributes, use `/A:` switch.

- **View Files with a Specific Attribute**
    
    C:\Users\htb\Desktop\example>dir /A
    
    Volume in drive C has no label. Volume Serial Number is 26E7-9EE4
    
    Directory of C:\Users\htb\Desktop\example
    
    06/16/2021 02:00 PM 5 file-66 1 File(s) 5 bytes 0 Dir(s) 38,632,652,800 bytes free
    
- **Delete a Read-only File**
    
    C:\Users\htb\Desktop\example > del /A
    
    *
    
    C:\Users\htb\Desktop\example>dir Volume in drive C has no label. Volume Serial Number is 26E7-9EE4
    
    Directory of C:\Users\htb\Desktop\example
    
    06/16/2021 02:22 PM DIR . 06/16/2021 02:22 PM DIR .. 06/16/2021 02:00 PM 5 file-2 06/16/2021 02:00 PM 5 file-4 06/16/2021 02:00 PM 5 file-6 3 File(s) 15 bytes 2 Dir(s) 38,632,529,920 bytes free
    
- **View Hidden Files**
    
    C:\Users\htb\Desktop\example>dir /A
    
    Volume in drive C has no label. Volume Serial Number is 26E7-9EE4
    
    Directory of C:\Users\htb\Desktop\example
    
    06/16/2021 02:00 PM 5 file-99 1 File(s) 5 bytes 0 Dir(s) 38,632,202,240 bytes free
    
- **Delete Hidden Files**
    
    C:\Users\htb\Desktop\example>del /A
    
    C:\Users\htb\Desktop\example>dir Volume in drive C has no label. Volume Serial Number is 26E7-9EE4
    
    Directory of C:\Users\htb\Desktop\example
    
    06/16/2021 02:28 PM DIR . 06/16/2021 02:28 PM DIR .. 06/16/2021 02:00 PM 5 file-2 06/16/2021 02:00 PM 5 file-4 06/16/2021 02:00 PM 5 file-6 3 File(s) 15 bytes 2 Dir(s) 38,631,997,440 bytes free
    

**Remove a Directory**

To remove a directory with its contents, use `del` followed by `rd` command. If files within have special attributes, use `/F` switch to force delete.

### Copying and Moving Files

**Copying Files** To copy a file from one location to another, use the `copy` command. For example, to copy `secrets.txt` from the `Backup` folder to the `Downloads` folder and rename it to `not-secrets.txt`, you would enter:

`copy secrets.txt C:\Users\student\Downloads\not-secrets.txt`

You can also use the `/V` switch to verify that the files were copied correctly:

`copy calc.exe C:\Users\student\Downloads\copied-calc.exe /V`

**Moving Files** To move a file or directory, use the `move` command. For instance, to move `bio.txt` from the `Desktop` to the `Downloads` folder, enter:

`move C:\Users\student\Desktop\bio.txt C:\Users\student\Downloads`

**Summary:**

- **Copy:** Use `copy` to duplicate a file or directory to a new location.
- **Move:** Use `move` to relocate and optionally rename a file or directory.

### Questions:
- What command can display the contents of a file and redirect the contents of the file into another file or to the console?
	- $type$
-  What command can be used to make the 'apples' directory? (full command as answer, not the alias)
	- "$mkdir$ $apples$"