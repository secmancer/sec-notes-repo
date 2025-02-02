### **Searching for Files and Directories**
- ##### **Using `where`**
	- `where <filename>` searches for files in system-defined paths.
	- Example:
    ```cmd
    C:\Users\student\Desktop> where calc.exe
    C:\Windows\System32\calc.exe
    ```    
	- If a file is not found, it might not be in the environment path.
- ##### **Recursive Search with `/R`**
	- `/R <directory>` allows searching through subdirectories.
	- Example:
    ```cmd
    C:\Users\student\Desktop> where /R C:\Users\student\ bio.txt
    C:\Users\student\Downloads\bio.txt
    ```
	- Supports wildcards:
    ```cmd
    C:\Users\student\Desktop> where /R C:\Users\student\ *.csv
    C:\Users\student\AppData\Local\live-hosts.csv
    ``` 
- #### **Searching Within Files**
	- ##### **Using `find`**
		- Searches for text within files.
		- Example:    
    ```cmd
    C:\Users\student\Desktop> find "password" "C:\Users\student\not-passwords.txt"
    ```
	- **Modifiers:**
	    - `/V` → Show lines that **do not** contain the string.
	    - `/N` → Display line numbers.
	    - `/I` → Ignore case sensitivity.
	    - Example:        
        ```cmd
        C:\Users\student\Desktop> find /N /I /V "IP Address" example.txt
        ```
- ##### **Using `findstr`**
	- Similar to `find` but supports regex, wildcards, and patterns.
	- Example:
    ```cmd
    C:\Users\student\Desktop> findstr "error" log.txt
    ```
- #### **Comparing Files**
	- ##### **Using `comp`**
		- Compares two files byte by byte.
		- Example:
    ```cmd
    C:\Users\student\Desktop> comp .\file-1.md .\file-2.md
    ```
	- **Modifiers:**
	    - `/A` → Show differences in ASCII.
	    - `/L` → Show line numbers.
- ##### **Using `fc`**
	- Compares files line by line.
	- Example:
    ```cmd
    C:\Users\student\Desktop> fc passwords.txt modded.txt /N
    ```
	- **Modifiers:**
	    - `/A` → Show first and last differing lines.
	    - `/C` → Ignore case.
	    - `/B` → Binary comparison.
- #### **Sorting and Filtering Files**
	- ##### **Using `sort`**
	- Sorts content alphabetically.
	- Example:
    ```cmd
    C:\Users\student\Desktop> sort .\file-1.md /O .\sorted.md
    ```
	- **Unique Sorting:**
    ```cmd
    C:\Users\student\Desktop> sort .\sort-1.md /unique
    ```



### **Key Takeaways**
- `where` locates files in system paths; `/R` makes it recursive.
- `find` and `findstr` help search within files; `findstr` is more powerful.
- `comp` does byte-by-byte comparisons; `fc` compares line-by-line.
- `sort` organizes data, and `/unique` removes duplicates.



### Questions
- What command can be used to search for regular expression strings from command prompt?
	- findstr
- Using the skills acquired in this and previous sections, access the target host and search for the file named 'waldo.txt'. Submit the flag found within the file.
	- RmxhZ3MgYXJlbid0IGhhcmQgdG8gZmluZCBub3csIHJpZ2h0Pw==