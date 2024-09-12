#### **Nano Editor**
**Overview**: Nano is a user-friendly text editor that's simpler to use compared to Vim. It provides a straightforward interface and is a good starting point for beginners.
- **Create a New File**:
    - _Command_: `nano <filename>`
    - _Example_: `secmancer@htb[/htb]$ nano notes.txt`
- **Editing in Nano**:
    - **Interface**: After opening Nano, you will see a pager where you can type and edit text directly.
    - **Keyboard Shortcuts**:
        - `^G` Get Help
        - `^O` Write Out (Save)
        - `^W` Where Is (Search)
        - `^K` Cut Text
        - `^U` Uncut Text
        - `^X` Exit
- **Search and Replace**:
    - To search for text: Press `[CTRL + W]`, type the search term, and press `[ENTER]`.
    - To jump to the next match: Press `[CTRL + W]` again and press `[ENTER]`.
- **Saving and Exiting**:
    - Save the file: Press `[CTRL + O]`, then confirm with `[ENTER]`.
    - Exit Nano: Press `[CTRL + X]`.
- **View File Contents**:
    - _Command_: `cat <filename>`
    - _Example_: `secmancer@htb[/htb]$ cat notes.txt`

#### **Vim Editor**

**Overview**: Vim is a powerful and efficient text editor that supports various modes and advanced editing features. It's an enhanced version of the older Vi editor.
- **Open Vim**:
    - _Command_: `vim`
    - _Example_: `secmancer@htb[/htb]$ vim`

![[Screenshot_20240912_123311.png]]

- **Modes in Vim**:
    - **Normal Mode**: Default mode for navigating and issuing commands.
    - **Insert Mode**: For inserting text. Enter Insert mode by pressing `i`.
    - **Visual Mode**: For selecting text. Enter Visual mode by pressing `v`.
    - **Command Mode**: For executing commands. Enter Command mode by pressing `:`.
- **Basic Commands**:
    - Exit Vim: Type `:q` in Command mode.
    - Save and Exit: Type `:wq` in Command mode.
    - Save File: Type `:w` in Command mode.
    - Search Text: Type `:/<search_term>` in Command mode.
    - Replace Text: Type `:s/<old_text>/<new_text>/` in Command mode.
- **Practice with Vim**:
    - Use `vimtutor` for a guided introduction to Vim.
    - _Command_: `vimtutor`
    - Follow the tutor to get familiar with Vim’s commands and capabilities.