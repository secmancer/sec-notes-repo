### Navigating the Windows Command Prompt

In this section, we'll explore essential commands and techniques to help you navigate the Windows filesystem using the Command Prompt. Whether you're a beginner or someone looking to sharpen your skills, mastering these basics is crucial for effective system navigation and understanding your environment.

---

### Listing a Directory

The first step in exploring a Windows system is listing the contents of the current directory. The `dir` command is your go-to tool for this task. Simply typing `dir` in the Command Prompt will display all files and directories in the current location.

**Example:**
- C:\Users\htb\Desktop> dir
This command lists all the files and directories on the desktop, providing details like the date and time of the last modification and the file size. You can also use `dir /?` to see more options and arguments that enhance the command's functionality.

---

### Finding Your Current Location

Knowing where you are in the filesystem is essential. The `cd` (or `chdir`) command can help with this. By typing `cd` without any arguments, you'll display the current directory path.
**Example**:
- C:\htb> cd
- C:\htb
This command confirms that you are in the `C:\htb` directory.

---

### Moving Around Using `CD` and `CHDIR`

The `cd` command isn't just for checking your current location; it's also used to change directories. You can move to a new directory by specifying its path after the `cd` command. This path can be either absolute (starting from the root) or relative (starting from the current directory).

#### Absolute Path Example:
- C:\htb> cd C:\Users\htb\Pictures
- C:\Users\htb\Pictures>

In this example, the path begins at the root (`C:\`) and navigates through each directory until it reaches `Pictures`.

#### Relative Path Example:
- C:\htb> cd .\Pictures
- C:\Users\htb\Pictures>

Here, the `.` represents the current directory (`C:\htb`), and `.\Pictures` directs the command to move into the `Pictures` folder within it.

You can also move up the directory structure by using `..` in the path.

Example:
- C:\Users\htb\Pictures> cd ..\..\..\
- C:\>

This command moves up three levels, bringing you back to the root directory (`C:\`).

---

### Exploring the File System with `Tree`

Once you're comfortable moving around, you can explore the directory structure more comprehensively using the `tree` command. This command provides a visual representation of the directory hierarchy, showing how directories and files are nested.

Example:
- C:\htb\student\> tree

This command displays a tree view of all directories and subdirectories in `C:\htb\student\`.

For more detailed information, including file names within each directory, use:
- C:\htb\student\> tree /F

**Note:** The output can be extensive, so you might want to use `Ctrl-C` to stop it once you've gathered enough information.

---

### Interesting Directories for Adversaries

Certain directories on a Windows system may be particularly valuable to an attacker. Here are a few examples:

- **C:\Windows\Temp**: Global temporary files accessible by all users. Ideal for attackers to drop files as a low-privilege user.
- **C:\Users\"user"\AppData\Local\Temp**: User-specific temporary files. Full ownership by the local user.
- **C:\Users\Public**: Publicly accessible directory. Less likely to be monitored.
- **C:\Program Files**: Contains 64-bit applications. Useful for checking installed software.
- **C:\Program Files (x86)**: Contains 32-bit applications.

These directories can serve various purposes, from reconnaissance to dropping malicious files, and should be monitored closely.

### Questions
- What command will give us a listing of all files and folders in a specified path?
	- tree /F
- What command will print my current working directory onto the console?
	- cd