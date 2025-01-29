### 1. **`more`** and **`less`**
- These tools allow you to view file contents interactively, one screen at a time.
	- **`more`** allows you to scroll down but offers fewer features than `less`.
	- **`less`** is more advanced and lets you scroll both forwards and backwards.
- For example:
```bash
cat /etc/passwd | more
less /etc/passwd
```



### 2. **`head` and `tail`**
- **`head`**: Prints the first 10 lines of a file.
- **`tail`**: Prints the last 10 lines of a file. You can specify the number of lines with the `-n` option (e.g., `head -n 20`).
- Example:
```bash
head /etc/passwd
tail /etc/passwd
```



### 3. **`sort`**
- The `sort` command sorts lines of text alphabetically or numerically. You can pipe the output of a command into `sort` to organize the results.
- Example:
```bash
cat /etc/passwd | sort
```



### 4. **`grep`**
- The `grep` command is used for searching text using patterns. You can filter content by matching specific patterns or exclude lines with the `-v` option.
- Examples:
```bash
cat /etc/passwd | grep "/bin/bash"
cat /etc/passwd | grep -v "false\|nologin"
```



### 5. **`cut`**
- The `cut` command is useful for extracting specific columns from text. You can define the delimiter with `-d` and the fields you want to display with `-f`.
- Example:
```bash
cat /etc/passwd | cut -d":" -f1
```



### 6. **`tr`**
- The `tr` command is used for replacing or deleting characters in a string.
- Example:
```bash
cat /etc/passwd | tr ":" " "
```



### 7. **`column`**
- This command formats text output into a more readable, columnar form.
- Example:
```bash
cat /etc/passwd | column -t
```



### 8. **`awk`**
- `awk` is a powerful text-processing tool that can handle complex patterns and field-based manipulations. You can use `$1`, `$NF`, etc., to reference specific fields.
- Example:
```bash
cat /etc/passwd | awk '{print $1, $NF}'
```



### 9. **`sed`**
- The `sed` (stream editor) command is used for performing text transformations on an input stream, such as replacing text using regular expressions.
- Example:
```bash
cat /etc/passwd | sed 's/bin/HTB/g'
```



### 10. **`wc`**
- The `wc` command counts the number of lines, words, and characters in a file. You can use `-l` to count lines.
- Example:
```bash
cat /etc/passwd | wc -l
```



### **Exercises to Practice**
- Here are some practice exercises to test your understanding of these commands using the `/etc/passwd` file:
	1. Display a line with the username `cry0l1t3`.
	2. Display all usernames.
	3. Display the username `cry0l1t3` and their UID.
	4. Display the username `cry0l1t3` and their UID separated by a comma.
	5. Display the username `cry0l1t3`, their UID, and their shell separated by a comma.
	6. Display all usernames with their UID and shell, separated by a comma.
	7. Exclude users with `nologin` or `false` shells, and display usernames with their UID and shell, separated by commas.
	8. Count all lines of the filtered output after excluding users with `nologin`.



### Example Solutions
1. `grep "cry0l1t3" /etc/passwd`
2. `cut -d: -f1 /etc/passwd`
3. `grep "cry0l1t3" /etc/passwd | cut -d: -f1,3`
4. `grep "cry0l1t3" /etc/passwd | cut -d: -f1,3 | tr ":" ","`
5. `grep "cry0l1t3" /etc/passwd | cut -d: -f1,3,7 | tr ":" ","`
6. `cut -d: -f1,3,7 /etc/passwd | tr ":" ","`
7. `cut -d: -f1,3,7 /etc/passwd | grep -v "nologin\|false" | tr ":" ","`
8. `cut -d: -f1,3,7 /etc/passwd | grep -v "nologin" | tr ":" "," | wc -l`



### Questions
 - How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)
	 - 7
- Determine what user the ProFTPd server is running under. Submit the username as the answer.
	- proftpd
- Use cURL from your Pwnbox (not the target machine) to obtain the source code of the "https://www.inlanefreight.com" website and filter all unique paths (https://www.inlanefreight.com/directory" or "/another/directory") of that domain. Submit the number of these paths as the answer.
	- 34