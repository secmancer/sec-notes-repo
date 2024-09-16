#### Understanding the Bash Prompt
- **Purpose:** Displays information and indicates that the system is ready for user input.
- **Default Format:** Typically includes:
    - Current user
    - Hostname
    - Current working directory
    - Example:
```
<username>@<hostname><current working directory>$
```

#### Prompt Customization
- **Home Directory:** Marked with a tilde (`~`). Example:
```
<username>@<hostname>[~]$
```
**User vs. Root Prompt:**
- **User Prompt:** Ends with `$`
- **Root Prompt:** Ends with `#`
- Example:
    - **Unprivileged User:** `$`
    - **Privileged Root:** `#`
- **Customizing Prompt Information:**
	- Display additional information like IP address, date, time, exit status of last command.
	- Example: Full path of the current directory or target’s IP address.

#### Customization with Special Characters and Variables
- **Configuration File:** `.bashrc` (for Bash shell)
- **Special Characters and Variables:**
    - `\u`: Current username
    - `\h`: Hostname
    - `\w`: Full path of the current working directory
    - `\d`: Date (Mon Feb 6)
    - `\D{%Y-%m-%d}`: Date (YYYY-MM-DD)
    - `\H`: Full hostname
    - `\j`: Number of jobs managed by the shell
    - `\n`: Newline
    - `\r`: Carriage return
    - `\s`: Name of the shell
    - `\t`: Current time (24-hour format, HH:MM)
    - `\T`: Current time (12-hour format, HH:MM)
    - `\@`: Current time

![[Screenshot_20240912_121431.png]]

#### Customizing Terminal Environment
- **Appearance:** Customize color schemes, fonts, and other settings for a more visually appealing and user-friendly environment.
- **Tools:** Use tools like `bash-prompt-generator` and `powerline` to adapt the prompt to personal needs.