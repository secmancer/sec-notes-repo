### Understanding the Help Functionality in Command Prompt
In the previous section, we introduced the Command Prompt and how to access it. Now, we'll delve deeper into one of its most valuable features: the help functionality. This built-in feature is essential for anyone looking to efficiently navigate and use the Command Prompt, especially in environments where internet access is limited or unavailable.

#### How to Utilize the Help Functionality
When faced with a blank Command Prompt screen, you might wonder what commands are available and how to use them. Fortunately, the Command Prompt includes a `help` function that provides detailed information about the available commands on your system.

To begin, simply type `help` at the prompt and press Enter. This command will display a list of built-in commands along with a brief description of each. Here’s an example:
```
C:\htb> help

For more information on a specific command, type HELP command-name
ASSOC          Displays or modifies file extension associations.
ATTRIB         Displays or changes file attributes.
BREAK          Sets or clears extended CTRL+C checking.
BCDEDIT        Sets properties in boot database to control boot loading.
CACLS          Displays or modifies access control lists (ACLs) of files.
...

```

This output gives you a quick overview of the commands available and their basic functions. If you need more detailed information about a specific command, you can type `help <command name>`. For example:

```
C:\htb> help time

Displays or sets the system time.

TIME [/T | time]

Type TIME with no parameters to display the current time setting and a prompt
for a new one. Press ENTER to keep the same time.

If Command Extensions are enabled, the TIME command supports
the /T switch which tells the command to just output the
current time, without prompting for a new time.

```

This more detailed output can guide you through the proper usage of the command, including any available parameters or switches.

#### Why Utilizing the Help Functionality is Essential
The help functionality is more than just a convenience—it's a crucial tool, especially when working in restricted environments. Consider the following scenario:

**Example Scenario**: You’re working on an internal network with no internet access and need to use a specific command for system enumeration. Without access to external resources, you might feel stuck. However, by using the help functionality built into the Command Prompt, you can quickly find the syntax and usage information needed to proceed.

In environments where network access is limited or nonexistent, relying on built-in help functions becomes essential. The `help` command serves as an offline manual, ensuring that you can still perform your tasks efficiently even when external resources are unavailable.

#### Additional External Resources for Help
While the built-in `help` function is invaluable, there are also numerous online resources you can use when you have internet access. These resources can provide more comprehensive information and examples for using Command Prompt:

- **Microsoft Documentation**: This official resource provides detailed explanations and usage instructions for all commands available in the Command Prompt.
- **SS64**: A quick reference guide for command-line tools, including Command Prompt, PowerShell, and others.

These resources can help deepen your understanding of the Command Prompt and offer additional tips and tricks that you might not find through the built-in help.

#### Tips and Tricks for Command Prompt
Now that you understand how to access help and where to find additional resources, let’s explore some tips and tricks that can improve your efficiency when working with the Command Prompt.

1. **Clearing the Screen**:
    - As you execute commands, your screen can become cluttered with output. To clear the screen, use the `cls` command:
```
C:\htb> cls
```
- This command gives you a clean slate, making it easier to focus on new tasks.
- **Command History**:
    - The Command Prompt keeps a history of the commands you’ve executed during the current session. You can navigate this history using the arrow keys, or view the entire history by typing `doskey /history`:
```
C:\htb> doskey /history
systeminfo
ipconfig /all
cls
...
```
- Command history is particularly useful when you need to re-execute previous commands without retyping them.
- **Exiting a Running Process**:
    - If you need to stop a running command, use `Ctrl+C`. This is helpful when a command is taking too long to execute or you realize you need to interrupt it.
```
C:\htb> ping 8.8.8.8
Reply from 8.8.8.8: bytes=32 time=22ms TTL=114
^C
```

By mastering these basics, you'll be well-equipped to navigate the Command Prompt with confidence and efficiency, even in challenging environments.

### Questions:
- If I wanted to view the help documentation for 'ipconfig', what command and/or modifier would I use? (full command string)
	- ipconfig /?

- What CLI equivalent "Help utility" exists on Linux hosts? (one word)
	- man

- Which CMD hotkey will open an interactive list of the previous commands we have ran?
	- F7