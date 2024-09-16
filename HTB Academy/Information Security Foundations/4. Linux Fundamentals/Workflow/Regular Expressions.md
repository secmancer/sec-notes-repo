Regular expressions (RegEx) are a powerful tool for searching, manipulating, and analyzing text based on patterns. They are used across various programming languages and tools to handle tasks like searching, replacing, and validating data.

#### Basic Concepts
- **Metacharacters**: Symbols in RegEx that define search patterns rather than having literal meanings. They are used to create complex search patterns.

![[Screenshot_20240912_124447.png]]
#### Grouping Operators
1. **Round Brackets `(a)`**:
    - Used to group parts of a regex together. Patterns within the brackets are treated as a unit.
2. **Square Brackets `[a-z]`**:
    - Define character classes. Inside the brackets, a list of characters is specified, and the regex matches any one of these characters.
3. **Curly Brackets `{1,10}`**:
    - Define quantifiers. Specifies how many times a previous pattern should be repeated. For example, `{1,10}` means between 1 and 10 times.
4. **Pipe Symbol `|`**:
    - Acts as an OR operator, matching either of the expressions separated by it.
5. **Dot `.`**:
    - Matches any single character except newline characters.

#### Examples
- **OR Operator**: Searches for lines containing either of the terms.
```
grep -E "(my|false)" /etc/passwd
```
Output:
```
lxd:x:105:65534::/var/lib/lxd/:/bin/false
pollinate:x:109:1::/var/cache/pollinate:/bin/false
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```
- **AND Operator**: Requires both terms to be present in the same line.
```
grep -E "(my.*false)" /etc/passwd
```
Output:
```
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```
Alternatively, you can use `grep` twice:
```
grep -E "my" /etc/passwd | grep -E "false"
```
Output:
```
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```

#### Practice Exercises

Using the `/etc/ssh/sshd_config` file, try the following tasks to practice RegEx:
- **Show all lines that do not contain the `#` character**:
```
grep -v "#" /etc/ssh/sshd_config
```
- **Search for all lines that contain a word starting with `Permit`**:
```
grep -E "\bPermit\w*" /etc/ssh/sshd_config
```
- **Search for all lines that contain a word ending with `Authentication`**:
```
grep -E "\w*Authentication\b" /etc/ssh/sshd_config
```
- **Search for all lines containing the word `Key`**:
```
grep -E "Key" /etc/ssh/sshd_config
```
- **Search for all lines beginning with `Password` and containing `yes`**:
```
grep -E "^Password.*yes" /etc/ssh/sshd_config
```
- **Search for all lines that end with `yes`**:
```
grep -E "yes$" /etc/ssh/sshd_config
```

![[Screenshot_20240912_124458.png]]