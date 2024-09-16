**Purpose**: Understand how to search for specific files and directories using CMD, why enumeration is crucial, and what to look out for during enumeration.


**Importance**: Enumeration is vital for gaining insights into the system's structure, finding hidden or critical files, and efficiently gathering necessary information.


**Searching with CMD**
- **Using `where`**:
    - **Basic Usage**:
        - Example: `where calc.exe`
            - Output: `C:\Windows\System32\calc.exe`
            - Success because `System32` is in the environment variable path.
        - Example: `where bio.txt`
            - Output: `INFO: Could not find files for the given pattern(s).`
            - Failure due to the file not being in the environment path.
    - **Recursive Search**:
        - Example: `where /R C:\Users\student\ bio.txt`
            - Output: `C:\Users\student\Downloads\bio.txt`
            - `/R` switch forces a recursive search through directories.
        - Example: `where /R C:\Users\student\ *.csv`
            - Output: `C:\Users\student\AppData\Local\live-hosts.csv`
            - Finds all `.csv` files in the specified directory and subdirectories.


**Using `find`**:
    - **Basic Usage**:
        - Example: `find "password" "C:\Users\student\not-passwords.txt"`
            - Searches for the text "password" within the specified file.
    - **Modifiers**:
        - `/V`: Excludes lines containing the search string.
        - `/N`: Shows line numbers.
        - `/I`: Ignores case sensitivity.
        - Example: `find /N /I /V "IP Address" example.txt`
            - Displays lines that do not contain "IP Address", with line numbers, ignoring case sensitivity.

**Using `findstr`**:
- **Purpose**: More advanced search capabilities compared to `find`.
- **Capabilities**:
    - Searches for patterns, regex values, wildcards, etc.
    - Comparable to `grep` in Linux for pattern-based searches.
- **Example Usage**:
    - `findstr` command usage details not provided but generally follows similar principles for searching and pattern matching.


**Purpose**: Learn how to evaluate and compare files using `comp`, `fc`, and `sort` commands in CMD, and understand how these tools are useful in both system administration and penetration testing.


**Comparing Files**
- **Using `comp`**:
    - **Function**: Compares each byte in two files to find differences.
    - **Default Output**: Differences are shown in decimal format.
    - **Modifiers**:
        - `/A`: Displays differences in ASCII format.
        - `/L`: Provides line numbers for differences.
    - **Examples**:
        - **Files are the same**:
            - Command: `comp .\file-1.md .\file-2.md`
            - Output: `Files compare OK`
        - **Files are different**:
            - Command: `comp .\file-1.md .\file-2.md /A`
            - Output: `Compare error at OFFSET 2`, showing specific character differences.


**Using `fc`**:
- **Function**: Compares files line-by-line and displays differences with more detailed output.
- **Options**:
    - `/A`: Shows only first and last lines of differences.
    - `/B`: Performs binary comparison.
    - `/C`: Ignores case sensitivity.
    - `/L`: Compares files as ASCII text.
    - `/N`: Displays line numbers.
    - `/U`: Compares as UNICODE text files.
    - `/W`: Compresses whitespace for comparison.
    - `/LBn`: Sets maximum consecutive mismatches.
**Examples**:
- **Basic Comparison**:
    - Command: `fc passwords.txt modded.txt /N`
    - Output: Shows line-by-line differences with line numbers and content from both files.


**Sorting Files**
- **Using `sort`**:
    - **Function**: Sorts input data from console, pipeline, or files and outputs results to the console or another file.
    - **Modifiers**:
        - `/O`: Specifies output file for sorted results.
        - `/unique`: Returns only unique entries.
    - **Examples**:
        - **Sorting a File**:
            - Command: `sort.exe .\file-1.md /O .\sort-1.md`
            - Output: Creates `sort-1.md` with sorted contents.
        - **Removing Duplicates**:
            - Command: `sort.exe .\sort-1.md /unique`
            - Output: Shows unique entries only, removing duplicates from `sort-1.md`.


## Questions
- What command can be used to search for regular expression strings from command prompt?
	- findstr
- Using the skills acquired in this and previous sections, access the target host and search for the file named 'waldo.txt'. Submit the flag found within the file.
	- RmxhZ3MgYXJlbid0IGhhcmQgdG8gZmluZCBub3csIHJpZ2h0Pw==