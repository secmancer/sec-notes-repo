### 1. Show all lines that do not contain the `#` character:
- The `#` character is typically used for comments in configuration files, so you’ll want to exclude lines that have it. This can be done with the `-v` option in `grep` to invert the match:
```bash
grep -v "#" /etc/ssh/sshd_config
```
- This command will print all lines that **do not** contain the `#` character.



### 2. Search for all lines that contain a word that starts with `Permit`:
- To search for words that begin with `Permit`, you can use the following regular expression pattern:
```bash
grep -E "\bPermit\w*" /etc/ssh/sshd_config
```
- Explanation:
	- `\b` denotes a word boundary.
	- `Permit` is the literal word you're searching for.
	- `\w*` matches any number of word characters (letters, digits, or underscores).



### 3. Search for all lines that contain a word ending with `Authentication`:
- To find words that end with `Authentication`, use this:
```bash
grep -E "\w*Authentication\b" /etc/ssh/sshd_config
```
- Explanation:
	- `\w*` matches any word characters before "Authentication".
	- `\b` ensures the word ends with `Authentication`.



### 4. Search for all lines containing the word `Key`:
- You can search for the word `Key` anywhere in the lines with:
```bash
grep -E "\bKey\b" /etc/ssh/sshd_config
```
- Explanation:
	- `\b` ensures that you match the whole word "Key" and not part of a longer word (like "PublicKey").



### 5. Search for all lines beginning with `Password` and containing `yes`:
- To match lines that start with `Password` and also contain `yes`, use:
```bash
grep -E "^Password.*yes" /etc/ssh/sshd_config
```
- Explanation:
	- `^Password` ensures the line starts with `Password`.
	- `.*` allows any characters between `Password` and `yes`.
	- `yes` is the literal string you're searching for.



### 6. Search for all lines that end with `yes`:
- To match lines that end with `yes`, you can use:
```bash
grep -E "yes$" /etc/ssh/sshd_config
```
- Explanation:
	- `yes$` matches the string `yes` at the end of a line (`$` is the end-of-line anchor).