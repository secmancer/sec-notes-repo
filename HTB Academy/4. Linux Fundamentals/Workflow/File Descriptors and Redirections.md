**File Descriptors (FDs)** in Unix/Linux are indicators used by the kernel to manage connections for Input/Output (I/O) operations. In Windows, they are referred to as filehandles. They represent connections (typically to files) used for performing I/O operations.

#### Default File Descriptors
1. **STDIN (Standard Input) - FD 0**: Input data stream.
2. **STDOUT (Standard Output) - FD 1**: Output data stream.
3. **STDERR (Standard Error) - FD 2**: Error data stream.

#### Examples of File Descriptors
- **STDIN and STDOUT**
    - **Example**: Using the `cat` command:
        - Input (STDIN - FD 0): "SOME INPUT"
        - Output (STDOUT - FD 1): "SOME INPUT" displayed in the terminal after pressing [ENTER]
- **STDOUT and STDERR**
    - **Example**: Using the `find` command:
        - Command: `find /etc/ -name shadow`
        - Output (STDOUT - FD 1): List of results
        - Error (STDERR - FD 2): "Permission denied"

#### Redirections
1. **Redirect STDERR to /dev/null**
    - Command: `find /etc/ -name shadow 2>/dev/null`
    - Purpose: Discards error messages, showing only standard output.
2. **Redirect STDOUT to a File**
    - Command: `find /etc/ -name shadow 2>/dev/null > results.txt`
    - Purpose: Saves standard output to `results.txt`, excluding errors.
3. **Redirect STDOUT and STDERR to Separate Files**
    - Command: `find /etc/ -name shadow 2> stderr.txt 1> stdout.txt`
    - Purpose: Saves standard errors to `stderr.txt` and standard output to `stdout.txt`.
4. **Redirect STDIN from a File**
    - Command: `cat < stdout.txt`
    - Purpose: Uses the contents of `stdout.txt` as standard input for `cat`.
5. **Redirect STDOUT and Append to a File**
    - Command: `find /etc/ -name passwd >> stdout.txt 2>/dev/null`
    - Purpose: Appends standard output to `stdout.txt`, while errors are discarded.
6. **Redirect STDIN Stream to a File**
    - Command: `cat << EOF > stream.txt`
    - Purpose: Uses stream input to create or overwrite `stream.txt` with data until EOF is encountered.
7. **Pipes**
    - **Usage**: Redirects STDOUT of one command to another command for further processing.
    - **Example**: `find /etc/ -name *.conf 2>/dev/null | grep systemd`
        - Filters `.conf` files in `/etc/` containing "systemd".
    - **Chaining Commands**: `find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l`
        - Counts the number of filtered results.

### Questions
- How many files exist on the system that have the ".log" file extension?
	- 32
- How many total packages are installed on the target system?
	- 737