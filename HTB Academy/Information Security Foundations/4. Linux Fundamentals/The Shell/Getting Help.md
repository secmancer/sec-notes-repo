#### Man Pages
- **Purpose:** Provides detailed manuals and explanations for commands and tools.
- **Syntax:**
```
man <tool>
```
- **Example:**
```
secmancer@htb[/htb]$ man curl
```
- **Description:** Shows detailed information about the `curl` tool, including options and usage.

#### Help Functions
- **General Help Command:**
    - **Syntax:**
```
<tool> --help
```
- **Example**:
```
secmancer@htb[/htb]$ curl --help
```
- **Description:** Lists available options and usage for the `curl` command.

**Short Help Option:**
- **Syntax:**
```
<tool> -h
```
- **Example:**
```
secmancer@htb[/htb]$ curl -h
```
- **Description:** Displays a brief summary of options and usage, similar to `--help`.

#### Apropos Command
- **Purpose:** Searches manual page descriptions for a given keyword.
- **Syntax:**
```
apropos <keyword>
```
- **Example:**
```
secmancer@htb[/htb]$ apropos sudo
```
- **Description:** Lists manual pages related to `sudo` with a brief description of each.

#### Explainshell
- **Purpose:** Helps understand complex commands by breaking them down.
- **Resource:** [Explainshell](https://explainshell.com/)
- **Description:** Provides explanations of each part of a long command for better understanding.