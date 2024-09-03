### Searching With CMD

**Using `where`**

- To find specific files:
    - `where calc.exe`
        - Finds `calc.exe` in the environment path.
    - `where bio.txt`
        - Fails to find `bio.txt` if it is not in the environment path.

**Recursive `where`**

- To search through directories recursively:
    - `where /R C:\Users\student\ bio.txt`
        - Finds `bio.txt` in `C:\Users\student\Downloads`.

**Using Wildcards**

- To search for file types:
    - `where /R C:\Users\student\ *.csv`
        - Finds CSV files within the specified directory.

**Using `find`**

- Basic search for text within a file:
    - `find "password" "C:\Users\student\not-passwords.txt"`

**`find` Modifiers**

- `/V`: Show lines that do not contain the string.
- `/N`: Display line numbers.
- `/I`: Ignore case sensitivity.
    - Example: `find /N /I /V "IP Address" example.txt`

**Using `findstr`**

- For more advanced searches with patterns and regex:
    - `findstr [options] [search_string] [file]`

### Evaluating and Sorting Files

**Using `comp`**

- Compare files byte-by-byte:
    - `comp .\file-1.md .\file-2.md`
    - Shows differences between files.

**Using `fc`**

- Compare files line-by-line:
    - `fc passwords.txt modded.txt /N`
    - Displays line numbers and differences.

**Using `sort`**

- Sort and manage file contents:
    - `sort.exe .\file-1.md /O .\sort-1.md`
        - Sorts `file-1.md` and writes to `sort-1.md`.
    - `/unique`: Returns only unique entries.
        - `sort.exe .\sort-1.md /unique`


### Questions
- What command can be used to search for regular expression strings from command prompt?
	- $findstr$
- Using the skills acquired in this and previous sections, access the target host and search for the file named 'waldo.txt'. Submit the flag found within the file.
	- $RmxhZ3MgYXJlbid0IGhhcmQgdG8gZmluZCBub3csIHJpZ2h0Pw==$